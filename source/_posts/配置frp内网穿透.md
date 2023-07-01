---
title: 配置frp内网穿透
date: 2021-06-03 09:34:18
tags:
---

### 1. 下载对应包

> https://github.com/fatedier/frp/releases

在git上找到对应自己系统版本的链接, 并下载到服务器

例:

`wget https://github.com/fatedier/frp/releases/download/v0.37.0/frp_0.37.0_linux_386.tar.gz`



### 2. 解压缩

`tar -zvxf frp_0.37.0_linux_386.tar.gz`

### 3. 修改服务器配置

> 后台运行: `nohup ./frps -c frps.ini >/dev/null 2>&1 &`
>
> bind_port FRP使用端口
>
> v_host_http_port 外部访问端口(可配置nginx proxy_pass转发)

- `vi frps.ini`

```shell
[common]
bind_port = 7000
token = 12345678
vhost_http_port = 80
```

- 启动: `./frps -c frps.ini`

### 4. 修改客户端配置

> 客户端下载同服务端

- `vi frpc.ini`

```shell
[common]
server_addr = 106.14.30.129
server_port = 7000
token = 12345678
tls_enable = true

[krkdwc]
type = http
custom_domains = dev.bogwang.cn
local_port = 5000
```

- 启动: `./frpc -c frpc.ini`

