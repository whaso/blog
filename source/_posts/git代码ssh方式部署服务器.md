---
title: git代码ssh方式部署linux服务器
date: 2021-09-29 10:30:47
tags:
---

## 1. 创建用户

```shell
# 创建用户, -m 创建用户家目录
useradd -m 用户名

# 修改密码(在root用户下操作)
passwd 用户名
```

## 2. 在git项目服务器添加ssh公钥

## 3. 在部署服务器用户家目录添加ssh密钥

```shell
mkdir ~/.ssh/
vi id_rsa  # 添加公钥
vi id_rsa.pub  # 添加私钥

# 如果提示权限644不对(Permissions 0644 for '~/.ssh/id_rsa' are too open) 执行以下命令修改权限
chmod 755 ~/.ssh/
chmod 600 ~/.ssh/id_rsa ~/.ssh/id_rsa.pub
chmod 644 ~/.ssh/known_hosts
```

