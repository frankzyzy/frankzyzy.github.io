---
layout: post
title: nginx常用命令和基本操作及问题解决
date: 2018-10-12 10:00:00 +0300
description: nginx入门的那些坑，整理出来了，还有可能会遇到的问题# Add post description (optional)
img: software.jpg # Add image post (optional)
tags: [Productivity, Software] # add tag
---


nginx常用命令：
 启动nginx
./usr/local/nginx/sbin/nginx
停止nginx
nginx -s stop
重启nginx
./sbin/nginx -s reload
nginx -s reload
查看进程
ps aux | grep nginx
验证配置是否正确: nginx -t
查看Nginx的版本号：nginx -V
启动Nginx：start nginx
快速停止或关闭Nginx：nginx -s stop
正常停止或关闭Nginx：nginx -s quit
配置文件修改重装载命令：nginx -s reload

解决nginx加tomcat的8080端口开放问题
server {  
        listen       80;  
        server_name  localhost;  
        #charset koi8-r;  
        #access_log  logs/host.access.log  main;  
        location / {  
		   proxy_pass http://localhost:8080 ;  
           proxy_set_header Host $host:80;  
        proxy_set_header X-Real-IP $remote_addr;  
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  
        proxy_set_header Via "nginx";  
        port_in_redirect off;  
        }  
	} 

nginx: [error] CreateFile() "E:\nginx\nginx-1.9.3/logs/nginx.pid" failed
nginx: [error] Open() "E:\nginx\nginx-1.9.3/logs/nginx.pid" failed
解决方法:
使用命令创建/logs/nginx.pid文件:
nginx -c conf/nginx.conf

Configuring Locations

下面的配置将匹配以 /some/path/开头的URIs，例如：/some/path/document.html
location /some/path/ {
...
}

正则表达式能通过 ~ 符号 和 ~* 这两个符号表示，分别指正则表达式区分大小写和不区分大小写，以下例子表示匹配URIs中包含.html 或者.htm 的访问路径：
location ~ \.html? {
...
}
nginx会匹配最准确的路径，会先匹配相对路径，如果不匹配，再跟正则表达式进行匹配

以下例子中，第一个路径/images/的文件目录是/data，第二个路径表明nginx作为代理的角色将会把请求转给后端www.example.com的机器上
server {
location /images/ {
root /data;
}

location / {
proxy_pass http://www.example.com;
}
}
如果这样配置，那么除了/image/开头的URIs，其他的URIs将会以代理的方式传到后端机器

root 指令
root指令能指定那个目录作为根目录用于文件的检索，这个指令能用于http,server,location这些块中
下面的例子指定了virtual server文件检索的根目录：
server {
root /www/data;

location / {
}

location /images/ {
}

location ~ \.(mp3|mp4) {
root /www/media;
}
}
当一个URI以/image/开头，那么将会在 /www/data/images/这个目录下进行检索；当URI以 .mp3或.mp4结尾时，nginx将会在/www/media目录下检索资源

当一个请求以 / 结尾时，nginx会尝试在该目录下找到该请求的索引文件（index file）。默认的索引文件为index.html。
例如 如果URI为/images/some/path/，那么nginx会尝试查找/www/data/images/some/path/index.html文件，如果这个文件不存在，那么将默认返回404。
可以通过 autoindex指令来配置nginx自动生成目录文件列表，而不是返回index.html
location /images/ {
autoindex on;
}

如果想让nginx查找更多指定类型的索引文件，可以通过Index指令指定，如：
location / {
index index.$geo.html index.htm index.html;
}

try_files 指令
try_files指令会在原请求不存在时，重定向到指定的URI，并返回结果。例如：
server {
root /www/data;

location /images/ {
try_files $uri /images/default.gif;
}
}
/www/data/images/index.html不存在时，将会返回/www/data/images/default.gif文件

另外一种情况是返回状态码：
location / {
try_files $uri $uri/ $uri.html =404;
}
location  = / {
  # 精确匹配 / ，主机名后面不能带任何字符串
  [ configuration A ] 
}

location  / {
  # 因为所有的地址都以 / 开头，所以这条规则将匹配到所有请求
  # 但是正则和最长字符串会优先匹配
  [ configuration B ] 
}

location /documents/ {
  # 匹配任何以 /documents/ 开头的地址，匹配符合以后，还要继续往下搜索
  # 只有后面的正则表达式没有匹配到时，这一条才会采用这一条
  [ configuration C ] 
}

location ~ /documents/Abc {
  # 匹配任何以 /documents/ 开头的地址，匹配符合以后，还要继续往下搜索
  # 只有后面的正则表达式没有匹配到时，这一条才会采用这一条
  [ configuration CC ] 
}

location ^~ /images/ {
  # 匹配任何以 /images/ 开头的地址，匹配符合以后，停止往下搜索正则，采用这一条。
  [ configuration D ] 
}

location ~* \.(gif|jpg|jpeg)$ {
  # 匹配所有以 gif,jpg或jpeg 结尾的请求
  # 然而，所有请求 /images/ 下的图片会被 config D 处理，因为 ^~ 到达不了这一条正则
  [ configuration E ] 
}

location /images/ {
  # 字符匹配到 /images/，继续往下，会发现 ^~ 存在
  [ configuration F ] 
}

location /images/abc {
  # 最长字符匹配到 /images/abc，继续往下，会发现 ^~ 存在
  # F与G的放置顺序是没有关系的
  [ configuration G ] 
}

location ~ /images/abc/ {
  # 只有去掉 config D 才有效：先最长匹配 config G 开头的地址，继续往下搜索，匹配到这一条正则，采用
    [ configuration H ] 
}

location ~* /js/.*/\.js

顺序 no优先级：
(location =) > (location 完整路径) > (location ^~ 路径) > (location ~,~* 正则顺序) > (location 部分起始路径) > (/)
按照上面的location写法，以下的匹配示例成立：
/ -> config A
精确完全匹配，即使/index.html也匹配不了
/downloads/download.html -> config B
匹配B以后，往下没有任何匹配，采用B
/images/1.gif -> configuration D
匹配到F，往下匹配到D，停止往下
/images/abc/def -> config D
最长匹配到G，往下匹配D，停止往下
你可以看到 任何以/images/开头的都会匹配到D并停止，FG写在这里是没有任何意义的，H是永远轮不到的，这里只是为了说明匹配顺序
/documents/document.html -> config C
匹配到C，往下没有任何匹配，采用C
/documents/1.jpg -> configuration E
匹配到C，往下正则匹配到E
/documents/Abc.jpg -> config CC
最长匹配到C，往下正则顺序匹配到CC，不会往下到E

所以实际使用中，个人觉得至少有三个匹配规则定义，如下：
#直接匹配网站根，通过域名访问网站首页比较频繁，使用这个会加速处理，官网如是说。
#这里是直接转发给后端应用服务器了，也可以是一个静态首页
# 第一个必选规则
location = / {
    proxy_pass http://tomcat:8080/index
}
# 第二个必选规则是处理静态文件请求，这是nginx作为http服务器的强项
# 有两种配置模式，目录匹配或后缀匹配,任选其一或搭配使用
location ^~ /static/ {
    root /webroot/static/;
}
location ~* \.(gif|jpg|jpeg|png|css|js|ico)$ {
    root /webroot/res/;
}
#第三个规则就是通用规则，用来转发动态请求到后端应用服务器
#非静态文件请求就默认是动态请求，自己根据实际把握
#毕竟目前的一些框架的流行，带.php,.jsp后缀的情况很少了
location / {
    proxy_pass http://tomcat:8080/
}
