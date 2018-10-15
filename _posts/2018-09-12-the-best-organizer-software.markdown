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
{% highlight java linenos %}
	@Test
    public void dynamicForeach3Test() {
        SqlSession session = Util.getSqlSessionFactory().openSession();
         BlogMapper blogMapper = session.getMapper(BlogMapper.class);
          final List ids = new ArrayList();
          ids.add(1);
          ids.add(2);
          ids.add(3);
          ids.add(6);
          ids.add(7);
          ids.add(9);
         Map params = new HashMap();
         params.put("ids", ids);
         params.put("title", "中国");
        List blogs = blogMapper.dynamicForeach3Test(params);
         for (Blog blog : blogs)
             System.out.println(blog);
         session.close();
     }

{% endhighlight %}


