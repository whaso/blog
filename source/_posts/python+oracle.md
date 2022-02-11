---
title: oracle常用命令
date: 2021-12-09 16:05:29
tags:
---

### 和MySQL对比

#### 大小写

- **oracle**本身不区分大小写 (会把关键字全部转为大写再执行),但是对引号里的字符区分大小写。

#### 主键自增

- oracle没有自带的主键自增, 需要先创建一个序列, 再创建一个触发器, 来实现主键自增







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
# sqlalchemy_URI  注: 不用指定数据库
oracle+cx_oracle://{账号}:{密码}@10.168.199.21:1521/?service_name={服务名}




```

**安装oracle19c客户端** (后发现连接不上远程数据库, 提示连接超时, 重新安装11.2.0.4版本客户端并开通了rac ip访问后可以正常连接)

> 各版本下载地址: https://www.oracle.com/database/technologies/instant-client/linux-x86-32-downloads.html

```
# 安装依赖包, 不然rpm安装时会提示缺少 (root)
yum install libnsl

wget https://download.oracle.com/otn_software/linux/instantclient/1913000/oracle-instantclient19.13-basic-19.13.0.0.0-2.x86_64.rpm

wget https://download.oracle.com/otn_software/linux/instantclient/1913000/oracle-instantclient19.13-sqlplus-19.13.0.0.0-2.x86_64.rpm

rpm -ivh oracle-instantclient19.13-basic-19.13.0.0.0-2.x86_64.rpm

rpm -ivh oracle-instantclient19.13-sqlplus-19.13.0.0.0-2.x86_64.rpm

cd /usr/lib/oracle/19.13/client64
vi tnsnames.ora
hiup =
　　　　(DESCRIPTION =
　　　　　　(ADDRESS_LIST =
　　　　　　　　(ADDRESS = (PROTOCOL = TCP)(HOST = 192.168.17.154)(PORT = 1521))
　　　　)
　　　　　　(CONNECT_DATA =
　　　　　　　　(SERVER = DEDICATED)
　　　　　　(SERVICE_NAME = hiup)
　　　　　　)
　　　　)
```

### 报错

- 报错ORA-00904: 后查到是数据库字段写错了, 和模型类的不一致
- unzip End-of-central-directory signature not found: 是文件有问题, 重新下载就可以
