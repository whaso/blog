---
title: oracle常用命令
date: 2021-12-09 16:05:29
tags:
---

### 和MySQL对比

- 大小写: **oracle** 本身不区分大小写 (会把关键字全部转为大写再执行),但是对引号里的字符区分大小写。

- 主键自增: **oracle** 没有自带的主键自增, 需要先创建一个序列, 再创建一个触发器, 来实现主键自增



#### 相关命令

```shell
# 查看当前用户所有序列
select * from user_objects where object_type='SEQUENCE';

# 查看表的所有触发器
select * from all_triggers where table_name='表名'; 

# 创建序列
create sequence 序列名称(一般是表名_SEQ)
start with 1  # 开始数字
minvalue 1 # 最小值
maxvalue   # 最大值
cycle    # 是否循环 cycle / nocycle
increment by 1  # 增长数字
nocache # 不使用缓存

# 删除序列
DROP SEQUENCE 序列名;

# 创建触发器
create or replace trigger 触发器名
        before insert on 表名
        referencing old as old new as new
        for each row
      begin
        select 序列名.nextval
          into :new.ID
          from dual;
      end 触发器名;

# 删除触发器
drop trigger 触发器名;


```



### 基操

```shell
# 查版本
select * from v$version;

# sqlalchemy_URI  注: 不用指定数据库
oracle+cx_oracle://{账号}:{密码}@10.168.199.21:1521/?service_name={服务名}




```



### **Docker Alpine安装oracle客户端**

1. 进入docker容器
```shell
docker run -it --name=容器名 镜像名:latest /bin/sh       由镜像创建容器并进入(只有镜像无容器)
或
docker exec -it 容器名 /bin/sh                          直接进入运行中的容器
```

2. 安装必要包

```shell
apk add libaio, libnsl, unzip
```

3. 下载解压oracle basic包

> 需要对应服务器版本, 命令`select * from v$version;`
>
> 各版本下载地址(32位): https://www.oracle.com/database/technologies/instant-client/linux-x86-32-downloads.html
>
> 各版本下载地址(64位): https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html
```shell
# 下载basic免安装zip包, 需要登录验证, 所以下载链接不能复用, 要在上面链接中找对应版本下载

# 弄个单独目录存
cd /usr/local
mkdir oracle
cd oracle

# wget -c 支持断点续传
wget -c https://download.oracle.com/otn/linux/instantclient/11204/instantclient-basic-linux.x64-11.2.0.4.0.zip
?AuthParam=1644827926_6725c450378f19288cb3dc5d040b8a18

# unzip 解压
unzip instantclient-basic-linux.x64-11.2.0.4.0.zip?AuthParam\=1644827926_6725c450378f19288cb3dc5d040b8a18

# 整理下文件
mv ./instantclient_11_2/* ./
rmdir instantclient_11_2
```
> unzip End-of-central-directory signature not found: 多半是下载的文件有问题, 重新下载就可以

4. 添加环境变量

```shell
# 通过查看 /etc/profile 可以看到会加载 /etc/profile.d/目录下的 .sh结尾的文件

# 弄个单独的环境变量配置文件
vi /etc/profile.d/oracle.sh
 
export ORACLE_HOME=/usr/local/oracle
export NLS_LANG=AMERICAN_AMERICA.AL32UTF8
export LD_LIBRARY_PATH=$ORACLE_HOME
export PATH=$ORACLE_HOME:$PATH

# 测试下加上没有
source /etc/profile
echo $PATH

# 退出容器
exit
```
> 注: 这里会有很多奇怪的报错, 以下为作者碰到的
>
> 报错1. Error loading shared library /usr/local/oracle/lib/libclntsh.so: No such file or directory
>
> (一开始是打算用软链接的, 但是没用, 直接复制就可以了, 不知道为什么)
>
> ```shell
> mkdir /usr/local/oracle/lib
> cp /usr/local/oracle/libclntsh.so.11.1 /usr/local/oracle/lib/libclntsh.so
> ```
> 如果经过以上操作扔有此报错, 且是用supervisor启动的, 可能是因为supervisor没读到环境变量, 需要在supervisor配置文件中添加
>
> ```shell
> environment=ORACLE_HOME="/usr/local/oracle",NLS_LANG="AMERICAN_AMERICA.AL32UTF8",LD_LIBRARY_PATH="/usr/local/oracle"
> 
> ```
>
> 注: supervisor添加环境变量时, 多个变量以`,`分隔, 单个变量多个值以`:`分隔
>
> 报错2. 
> Error loading shared library libnsl.so.1: No such file or directory (needed by /usr/local/oracle/lib/libclntsh.so
> (libnsl.so.1  或 libnsl.so) 建对应软链接
>
> ```shell
> ln -s /usr/lib/libnsl.so.2.0.0 /usr/lib/libnsl.so.1
> ln -s /usr/lib/libnsl.so.2.0.0 /usr/lib/libnsl.so
> ```
>
> 报错3: cx_Oracle.DatabaseError: ORA-21561: OID generation faile
>
> 这是hosts文件有问题
>
> ```shell
> hostname  # 查看当前hostname
> 把当前hostname加入到 /etc/hosts 文件的 127.0.0.1 即可
> ```
>
> 

5. 提交镜像

```shell
docker commit -a 'laowang' 容器名 镜像名:1.0.0
```

6. 换docker启动用的镜像版本号

> 注: 最后会发现环境变量没有加载, 原因未知
>
> 绕路解决方法: 
>
> -  通过DockerFile直接运行容器的项目: 修改`Dockerfile`文件,  例: `CMD source /etc/profile && gunicorn ....`
> - 通过DockerCompose启动的项目:  修改`docker-compose.yml`文件 例: `command: /bin/sh -c "source /etc/profile && gunicorn ...."`
>
> **python 直连测试代码**
>
> import cx_Oracle
> conn = cx_Oracle.connect("user/passwd@host/instance")



### 报错

- 报错ORA-00904: 后查到是数据库字段写错了, 和模型类的不一致

- 索引失效(partition of such index is in unusable state):

  - ```sql
    select index_name,status from user_indexes;  # 查失效索引
    
    alter index SYS_C00164313 rebuild;  # 重建索引
    ```

    
