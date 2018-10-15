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


