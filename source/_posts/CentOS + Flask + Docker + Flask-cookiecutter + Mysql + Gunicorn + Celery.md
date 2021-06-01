# CentOS + Flask + Docker + Flask-cookiecutter + Mysql + Gunicorn + Celery

> 服务器是阿里云买的CentOS系统.
>
> DNF包管理器克服了YUM包管理器的一些瓶颈，提升了包括用户体验，内存占用，依赖分析，运行速度等多方面的内容。

# 1. 安装docker

> yum install docker

安装完执行`docker`, 提示`Emulate Docker CLI using podman.` 上网查发现是

>  CentOS8 以上的版本默认已经安装一个等同于 Docker的容器解决方案，这个就是Podman.

> 简单理解 `alias docker = podman`

 

## 2. 安装MySQL

- 安装: `dnf install @mysql`

- 启动: `systemctl start mysqld`
- 查看运行状态: `systemctl status mysqld`