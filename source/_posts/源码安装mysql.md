---
title: 源码安装mysql
date: 2021-07-26 10:46:45
tags:
---

# 源码安装Mysql

> 系统: CentOS 8

## 1. 下载

**官网找指定版本下载源码包**   

>  https://downloads.mysql.com/archives/community/

```shell
wget https://downloads.mysql.com/archives/get/p/23/file/mysql-boost-5.7.34.tar.gz
```



## 2. 解压编译

```shell

# 解压
tar -zvxf mysql-boost-5.7.34.tar.gz
cd mysql-5.7.34

# 安装cmake
yum install cmake

# 编译
cmake .

```

编译时命令 `cmake .` 报错汇总

```shell
# 报错: undefined symbol: archive_write_add_filter_zstd
yum install libarchive

# 报错: No CMAKE_CXX_COMPILER could be found.
yum install gcc-c++

# 报错: CMake Error at cmake/boost.cmake:88, 根据提示命令增加额外安装boost目录
# (也可自行下载安装Boost C++ 下载地址: https://sourceforge.net/projects/boost/files/boost/)
# 注意 只能是1.59.0版本的boost
mkdir -p /usr/local/boost

cmake -DDOWNLOAD_BOOST=1 -DWITH_BOOST=/usr/local/boost .
# 或
cd /usr/local/boost
wget https://udomain.dl.sourceforge.net/project/boost/boost/1.59.0/boost_1_59_0.tar.gz
tar -zvxf boost_1_59_0.tar.gz
cmake . -DDOWNLOAD_BOOST=1 -DWITH_BOOST=/usr/local/boost/boost_1_59_0

# 报错: CMake Error at cmake/ssl.cmake:63 (MESSAGE): Please install the appropriate openssl developer package
gg


```



# 二进制安装

## 1. 下载

> https://downloads.mysql.com/archives/community/
>
> Operating System: Linux-Generic
>
> OS Version: Linux-Generic(glibc 2.12) (x86, 64-bit)

```shell
wget https://downloads.mysql.com/archives/get/p/23/file/mysql-5.7.34-linux-glibc2.12-x86_64.tar.gz
```



## 2. 安装

> 先查看下系统磁盘绑定情况, 再决定mysql data目录
>
> 命令: df -h

### 2.1. 创建用户, 用户组, 数据目录

```shell
groupadd mysql
useradd -g mysql -d /home/mysql mysql
mkdir /home/mysql/data
```

### 2.2. 下载, 解压

```shell
cd /home/mysql
wget https://downloads.mysql.com/archives/get/p/23/file/mysql-5.7.34-linux-glibc2.12-x86_64.tar.gz
tar -zvxf mysql-5.7.34-linux-glibc2.12-x86_64.tar.gz
```

### 2.3. 配置启动

```shell 
# 初始化配置
./mysqld --user=mysql --basedir=/home/mysql --datadir=/home/mysql/data --initialize

# 修改basedir, datadir
vim support-files/mysql.server
--------------------------
...
basedir=/home/mysql
datadir=/home/mysql/data
...
--------------------------

# 创建软链接使命令可全局使用
ln -s /home/mysql/bin/mysql /usr/bin/mysql

# 创建配置文件
vi /etc/my.cnf
--------------------------
...
[mysqld]

basedir = /home/mysql
datadir = /home/mysql/data

character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
init_connect = 'SET NAMES utf8mb4'

[mysql]
default-character-set = utf8mb4

[client]
default-character-set=utf8mb4
...
--------------------------

# 添加开机启动
cp /home/mysql/support-files/mysql.server /etc/init.d/mysqld

# 增加可执行权限
chmod 755 /etc/init.d/mysqld

# 查看开机启动列表是否有mysqld, 没有就根据提示添加
chkconfig --list mysqld
chkconfig --add mysqld 

# 启动mysql
./support-files/mysql.server start

# 首次进入mysql 并修改root密码
mysql -uroot -p
> alter user user() identified by "修改的密码";

# 查看默认编码集
show variables where variable_name like '%char%' or variable_name like 'collation%';
+--------------------------+-----------------------------+
| Variable_name            | Value                       |
+--------------------------+-----------------------------+
| character_set_client     | utf8mb4                     |
| character_set_connection | utf8mb4                     |
| character_set_database   | utf8mb4                     |
| character_set_filesystem | binary                      |
| character_set_results    | utf8mb4                     |
| character_set_server     | utf8mb4                     |
| character_set_system     | utf8                        |
| character_sets_dir       | /home/mysql/share/charsets/ |
| collation_connection     | utf8mb4_unicode_ci          |
| collation_database       | utf8mb4_unicode_ci          |
| collation_server         | utf8mb4_unicode_ci          |
+--------------------------+-----------------------------+

# systemctl 显示mysqld退出但实际没退出时
systemctl daemon-reload
```

<font color="red">启动mysql可能出现的错误:</font>

```shell
# error while loading shared libraries: libncurses.so.5 
# error while loading shared libraries: libtinfo.so.5
# 提示缺少依赖libncurses.so.5 和 libtinfo.so.5
# 但在 /usr/lib64 目录下是有 libtinfo.so.6.1 和 libncurses.so.6.1包的
# 所以只需创建个软链接让mysql启动时去找到 *.5的包但实际是调用 *.6.1的包即可

sudo ln -s /usr/lib64/libncurses.so.6.1 /usr/lib64/libncurses.so.5
sudo ln -s /usr/lib64/libtinfo.so.6.1 /usr/lib64/libtinfo.so.5
```



















