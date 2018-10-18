---
layout: post
title: Spring Boot 配置文件数据源加密
date: 2018-10-18 11:36:00 +0300
description: Spring Boot项目中application.yml加密配置源
img: we-in-rest.jpg # Add image post (optional)
tags: [java,springboot] # add tag
---


# 概述

开发的同学们都知道，例如项目依赖的信息，数据库信息一般是保存在配置文件中，而且都是明文，因此需要进行加密处理，今天在这里介绍下jasypt集成springboot加密的配置

1. 第一步：pom文件加入依赖

   ```xml
   <dependency>
       <groupId>com.github.ulisesbocchio</groupId>
       <artifactId>jasypt-spring-boot-starter</artifactId>
       <version>2.1.0</version>
   </dependency>
   ```
------

2. 第二步：生成密钥(在windows下命令生成加密密文)

   找到你的maven仓库路径 ====G:\maven\repository\org\jasypt\jasypt\1.9.2\====，替换下面的路径。

   参数说明:

   input = 数据库链接密码

   password = 加密字段，随意设置你要加密的字符!

   algorithm = 算法

   algorithm = 加密算法（默认就行）

   ```
   java -cp G:\maven\repository\org\jasypt\jasypt\1.9.2\jasypt-1.9.2.jar org.jasypt.intf.cli.JasyptPBEStringEncryptionCLI input="admin" password=saltnewfor algorithm=PBEWithMD5AndDES
   ```

   执行后有以下输出：

   ```
   ----ENVIRONMENT-----------------
    
   Runtime: Oracle Corporation Java HotSpot(TM) 64-Bit Server VM 25.131-b11 
    
   ----ARGUMENTS-------------------
    
   algorithm: PBEWithMD5AndDES
   input: admin
   password: saltnewfor
    
   ----OUTPUT----------------------
    
   UK61bS+W/BskHl0N0ViAQcrPAmZLZZwO
   
   ```
------

3. 第三步：在application.yml文件中配置

   注意格式要写在  ENC(加密字符)    （）里面为生成的加密字符

   ```yaml
   jasypt:
     encryptor:
       password: saltnewfor
   spring:    
     datasource:
       driver-class-name: com.mysql.jdbc.Driver
       url:  
       username: ENC(UK61bS+W/BskHl0N0ViAQcrPAmZLZZwO)
       password: ENC(Z0W0OKw1+Dfi5KY8Q5lqvA==)
   ```

重启项目 大功告成啦！