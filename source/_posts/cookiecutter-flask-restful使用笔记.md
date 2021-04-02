---
title: cookiecutter-flask-restful使用笔记
date: 2021-04-02 17:40:17
tags:
---

[TOC]

# flask-cookiecutter-restful 使用



## 一. 本地开发准备



### 1. 源码安装python-3.7.10

```shell
wget -c https://www.python.org/ftp/python/3.7.10/Python-3.7.10.tar.xz
tar -zxvf Python-3.7.10.tar.xz
cd Python-3.7.10/Modules
vim Setup.dist
```

搜索:

```shell
:/ssl
```
将以下内容取消注释:

```shell 
# Socket module helper for socket(2)
#_socket socketmodule.c
# Socket module helper for SSL support; you must comment out the other
# socket line above, and possibly edit the SSL variable:
#SSL=/usr/local/ssl
#_ssl _ssl.c \
# -DUSE_SSL -I$(SSL)/include -I$(SSL)/include/openssl \
# -L$(SSL)/lib -lssl -lcrypto
```

取消注释如下：

```shell
# Socket module helper for socket(2)
_socket socketmodule.c
# Socket module helper for SSL support; you must comment out the other
# socket line above, and possibly edit the SSL variable:
#SSL=/usr/local/ssl
_ssl _ssl.c \
-DUSE_SSL -I$(SSL)/include -I$(SSL)/include/openssl \
-L$(SSL)/lib -lssl -lcrypto
```

返回Python源码根目录编译安装：

```
cd ../
./configure --prefix=/usr/local/python3.7.10 --enable-loadable-sqlite-extensions
make
make install
```

将 /usr/local/python3.6/bin 加入 PATH， 在`/etc/profile`文件后追加：

```
vim /etc/profile
```

追回内容如下：

```
export PATH=/usr/local/python3.7/bin:$PATH
```

设置python, pip别名：

```
vim ~/.bashrc
```

内容如下：

```
alias python3.7=/usr/local/python3.7.10/bin/python3
alias pip3.7=/usr/local/python3.7.10/bin/pip3
```



### 2. 使用cookiecutter创建项目

```shell
pip install cookiecutter

cookiecutter https://github.com/karec/cookiecutter-flask-restful
```



### 3. pipenv 创建虚拟环境

```shell
# 安装
pip install pipenv

# 更新
pip install --user --upgrade pipenv

# 指定Python版本创建虚拟环境
pipenv --python 3.7

# 进入虚拟环境
pipenv shell

# 安装包
pipenv install
# 或
pipenv install -r requirements.txt
```

### 4. 数据库
```shell
# 本地创建相关库
CREATE DATABASE `aipms` /*!40100 DEFAULT CHARACTER SET utf8mb4 */

# 项目配置数据库, 修改.env
DATABASE_URI=mysql+pymysql://root:123456@localhost:3306/aipms?charset=utf8mb4

# 进虚拟环境
pipenv shell

# 生成迁移文件
flask db migrate -m 'init migration'

# 更新到数据库
flask db upgrate
```

### 5. 接口测试

- 注册
```shell
curl --location --request POST 'http://127.0.0.1:5002/auth/register' \
--header 'Content-Type: application/json' \
--data-raw '{
    "username": "admin",
    "password": "admin"
}'
```

- 登录
```shell
curl --location --request POST 'http://127.0.0.1:5002/auth/login' \
--header 'Content-Type: application/json' \
--data-raw '{
    "username": "admin",
    "password": "admin"
}'
```


### 6. git

```shell
# git初始化
git init

# 添加源
git remote add origin git@*****

# 拉取代码, 有冲突解决冲突
git pull

# 切换新分支
git checkout -b feature-init

# add 所有
git add .

# commit
git commit -m 'init'

# 分支推送到远程库
git push --set-upstream origin feature-init
```



## 二. 部署

### 1. gunicorn

```shell
pipenv install gunicorn
```



### 2. docker

- 安docker

```shell
brew install docker
```

- 安docker-compose

```shell
python3 -m pip install docker-compose
```

- 登录docker
```shell
docker login
```

- 拉取基础Image
```shell
docker pull python:3.7.10-alpine
```

- 创建容器并进入
```shell
docker run -it --name=container_name python:3.7.10-alpine /bin/sh
```

- 配置dockerfile
```shell

```

- 从dockerfile启动项目
```shell
docker build -t container_name ./Dockerfile
```

