---
title: nginx相关
date: 2021-03-18 17:05:06
tags:
---
### nginx服务更新证书
```
nginx配置文件: /etc/nginx/sites_enabled
server {
    listen  443;
    server_name djdeveloper.cn *.djdeveloper.cn;
    root    /var/www/djdeveloper.cn;
    autoindex   off;
    ssl on;
    ssl_certificate /etc/nginx/ssl/djdeveloper.full.crt;
    ssl_certificate_key  /etc/nginx/ssl/djdeveloper.key;

    ssl_session_cache       shared:SSL:1m;
    ssl_session_timeout     5m;
}

nginx证书: /etc/nginx/ssl

cp **.full.crt **.full.crt.bak
cp **.key **.key.bak

vim **.full.crt cp
vim **.key cp

nginx -s reload
```

### 配置跨域:

```shell
位置: http{这里, server{}}

add_header 'Access-Control-Allow-Origin' '*';
add_header 'Access-Control-Allow-Credentials' 'true';
```

### nginx 502 错误初步排查
- nginx 配置文件默认目录 /etc/nginx/nginx.conf
- 配置文件中有 include * 为包含的配置文件
- access_log off 为关闭日志, 开启后为 access_log /var/www/ccd.log
- 如果在日志文件中能看到请求说明与nginx无关, 是项目的问题
- nginx -s reload
- nginx -t 检查配置文件语法是否正确
- lsof -i:port1 检查端口使用 CLOSE_WAIT 时看 port1 -> port2 是port2出了问题

