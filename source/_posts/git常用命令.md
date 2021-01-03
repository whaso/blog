---
title: git常用命令
date: 2021-01-03 17:07:59
tags:
---

### 注意
### sublime
```
command shift L 列选择
```



#### MySQL
- 入库的数据类型和库表的数据类型要一致, 出现问题是: int 类型 入库到 varchar 类型的字段时不会更新数据也不会报错 我日!

### 常用命令
```
echo $环境变量  --查看环境变量
tail -100f xxx.log | grep '关键词'
git branch -D feature-sfsfsf 删除分支
df  --查看所有磁盘空间 (类似Windows的 CDEF盘)
du  --查看当前目录 
git push origin -d feature-dev 删除远程分支
git branch -D feature-dev 删除本地分支
docker exec -it -u root container_name /bin/sh  用管理员权限进入docker
docker run container
docker container ls -as
docker ps -as -- -as列出所有容器 包括没运行的
mysql输出按指定字段值排序:order by field(key, value, value...)
chown -R appuser:appuser file_name -- R是路径下全部的意思, 用户组:用户
json.dumps(ensure_ascii=False) 这样转化json字符串就不会把中文编码为unicode
```

### 网络问题
```
ping ip 看本机与服务器网络是否通
telnet ip port 看服务器是否开放对应端口
```
#### Git
- 冲突: dev 低于 issue分支版本导致冲突
``` 
git diff
git reset --hard origin/issue-expireinhours  回退分支版本
git log


git checkout develop
git pull
git checkout develop
git merge issue-expireinhours 
git add .
git commit -m '合并issue-expireinhours'
git push 
```

### 查服务器有没有安装nginx服务
```
su
find / -name "nginx*"
ps aux | grep nginx
lsof -i:80
cd /etc
ls
```

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

### Git备份版本
```
git checkout master
git pull
====备份====
git tag -a msg_bak -m '测试短信前备份'
git push origin msg_bak
## git merge feature-cancelmsg  手动合并
## git push origin master 
====回退====
git show mag_bak
git reset --hard id
git push origin master -f

git reset --hard /origin/master  # 在项目服务器 强制回滚, 以远程库分支为准
```

wc -l 统计行数 cat abc.txt | wc -l


### 数据库查重
```mysql
select * from people  where peopleId in (select peopleId from people group by peopleId having count(peopleId) > 1)  
select * from Users where UserId in (select UserId from Users  group by UserId having count(UserId) > 1)  
-- 不过在数据量过大的时候查询的速度会非常慢


select count(peopleId) from people 
select count(distinct peopleId) from people  
可以用上面两条语句的结果进行对比判断是否存在重复数据
```

### nginx 502 错误
- nginx 配置文件默认目录 /etc/nginx/nginx.conf
- 配置文件中有 include * 为包含的配置文件
- access_log off 为关闭日志, 开启后为 access_log /var/www/ccd.log
- 如果在日志文件中能看到请求说明与nginx无关, 是项目的问题
- nginx -s reload
- nginx -t 检查配置文件语法是否正确
- lsof -i:port1 检查端口使用 CLOSE_WAIT 时看 port1 -> port2 是port2出了问题 
- 

### Win10激活
```
HWIDGEN
```

### nginx配置
- root 实际路径会加上路由
- alias 实际路径不会加上路由
- 

### mac切换root
- sudo -s