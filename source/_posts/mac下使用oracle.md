---
title: mac下使用oracle.md
date: 2021-06-01 09:56:00
tags:
---

> Oracle 字符串只能用单引号

### mac安装通过docker安装使用oracle
> https://github.com/MaksymBilenko/docker-oracle-12c
```shell
# 拉取镜像
docker pull quay.io/maksymbilenko/oracle-12c

# 创建容器并运行
docker run -d -p 8080:8080 -p 1521:1521 --name=oracle quay.io/maksymbilenko/oracle-12c

# 连接配置
hostname: localhost
port: 1521
sid: xe
service name: xe
username: system
password: oracle
```

### 基操

- 查看数据库版本: `select * from v$version;`

#### 用户

- 创建用户:  `create user 用户名 identified by 密码`
  -   例: `create user test identified by test`

> 第一次创建`create user 'root' identified by '123456'` 
>
> 提示 missing user or role name 是因为此处用户名不需要引号
>
> 修改后提示无效密码, 同样密码也不需要引号

- 修改密码: `alter user 用户名 identified by 新密码`

#### 角色

> oracle为兼容以前版本，提供三种标准角色（role）:connect, resource和dba.

1. connect role(连接角色)

--临时用户，特指不需要建表的用户，通常只赋予他们connect role. 

--connect是使用oracle简单权限，这种权限只对其他用户的表有访问权限，包括select/insert/update和delete等。

--拥有connect role 的用户还能够创建表、视图、序列（sequence）、簇（cluster）、同义词(synonym)、回话（session）和其他 数据的链（link）

 

2. resource role(资源角色)

--更可靠和正式的数据库用户可以授予resource role。

--resource提供给用户另外的权限以创建他们自己的表、序列、过程(procedure)、触发器(trigger)、索引(index)和簇(cluster)。



3. dba role(数据库管理员角色)

--dba role拥有所有的系统权限

--包括无限制的空间限额和给其他用户授予各种权限的能力。system由dba用户拥有



除了前面三种系统角色----connect、resource和dba，用户还可以在oracle创建自己的role。

用户创建的role可以由表或系统权限或两者的组合构成。

为了创建role，用户必须具有create role系统权限。

1. 创建角色: `create role 角色名;`

2. 授权角色:  `grant select on 表名 to 角色名;`

3. 删除角色: `drop role 角色名;`

#### 权限

- 授权: `grant connect, resource to 用户名;`
- 撤消:  `revoke connect, resource from 用户名;`

### 库表

> 创建表时提示:  `no privileges on tablespace USERS`
>
> 执行: `alter user 库名 quota unlimited on users;`



- 创建数据库: `create tablespace 表间名 datafile '数据文件名' size 表空间大小;`
  - 例: `create tablespace TEST datafile 'test' size 20M;`
- 查看建表语句: `select dbms_metadata.get_ddl('TABLE','USERINFO') from dual;`





