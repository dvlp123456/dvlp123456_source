---
title: erlang编译报错问题和linux源码安装erlang
date: 2018-06-30 23:04:00
tags: [dvlp123456,2018,erlang,linux,技术]
categories: 技术
description: erlang编译报错问题和linux源码安装erlang
---

## 1.前言  

这段时间重温了erlang的一些基础，遇到一些基础问题，在此记录下   

<!--more-->

## 2.列表  

- 1.编译ezwebframe遇到erlang版本低问题  

![](/img/erlang-compile-install1.png)  

![](/img/erlang-compile-install2.png)  

![](/img/erlang-compile-install3.png)  

- 2.erlang管理工具rebar编译问题  

erlang常用管理工具有：rebar，make.file。  
rebar版本有：以前版本（[https://]github.com/basho/rebar），rebar3版本（[https://]github.com/erlang）。这两个版本差别很大。  
Windows环境使用rebar的一个介绍文章：https://www.cnblogs.com/autumnwhisper/p/4914726.html。  

踩过的坑：rebar3无法顺利的编译通过，rebar以前版本可以顺利编译通过并且正常使用（具体原因未去深究）  

![](/img/erlang-compile-install4.png)  

- 3.编译cowboy遇到erlang版本低问题  

![](/img/erlang-compile-install5.png)  

既然linux环境下erlang版本低，那么我们就来安装一个更高版本erlang吧：  

https://blog.csdn.net/li775085737/article/details/77825217  
https://jingyan.baidu.com/article/19020a0a2eb81b529d28429a.html  

安装步骤过程：

1. 下载源码包（当然还有rpm包和预编译包安装等方式）；  
2. 配置：./configure --prefix=/usr/local/servers/erlang --without-javac --with-ssl=/usr/local/ssl/,需要查看--with-ssl意思，configure --help即可，使用ssl，一般安装地址是/bin/local/ssl，查看安装的位置：rpm -ql openssl ；  
3. 编译：make，安装：make install，建议给管理权限去操作；  
4. 配置erl路径：  
   mv /usr/bin/erl /usr/bin/erl.bak  
   mv /usr/bin/erlc /usr/bin/erlc.bak  
   ln -s /usr/local/servers/erlang/bin/erl /usr/bin/erl  
   ln -s /usr/local/servers/erlang/bin/erlc /usr/bin/erlc  
5. 验证：  
   输入erl查看版本  
6. linux安装erlang在configure时会检查所有配置，可能遇到依赖问题，一下是列表：  

![](/img/erlang-compile-install6.png)  


