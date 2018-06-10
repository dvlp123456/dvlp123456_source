---
title: 阿里云服务器ecs安装(搭建)Tomcat
date: 2018-06-09 11:28:15
tags: [dvlp123456,2018,技术]
categories: 技术
description: 阿里云服务器ecs安装(搭建)Tomcat
---

## 前因后果  

个人在阿里购买了云服务器ecs，前面已经结合hexo+github+jenkins实现了可多人合作的自动部署的静态博客了，想着能不能做更多的事情，所以想试着在ecs里面安装Tomcat，试着搭建动态的服务器。  

本次的目标是:**安装Tomcat**。   

<!--more-->  

## 马上动手做  

网上搜索了一份较全的资料，地址是：https://www.jianshu.com/p/2604e53a7f6a?from=singlemessage  
可以参考下这篇文章，当然了，每个人安装都会遇到不一样的问题，我记录的就是我自己的情况。  

### 安装java和Tomcat  

我的Linux环境已经安装了java jdk8：  

![](/img/ecsinstalltomcat1.png)  

所以我只需安装Tomcat即可，在Windows环境下下载Tomcat，去到Tomcat官网下载，如图：  

![](/img/ecsinstalltomcat2.png)  

![](/img/ecsinstalltomcat3.png)    

打开xshell，连接到ecs，“窗口”-->“传输新建文件”，把Tomcat放置到ecs对应位置：  

![](/img/ecsinstalltomcat4.png)  

解压：tar -zcvf xxxx.tar.gz  
Tomcat的配置文件以及日志文件位置等文件在bin同目录下：  

![](/img/ecsinstalltomcat5.png)  

**启动Tomcat：在bin目录下，命令：./startup.sh，除了查看打印出来的信息，此时必须到日志出查看日志是否有错，没有错误表明启动成功；  
停止Tomcat：在bin目录下，命令：./shutdown.sh，除了查看打印出来的信息，同时也必须看日志，是否有错误；**  

此时ecs必须开启对应端口，Tomcat默认端口是8080，我的Linux中已经被jenkins服务占用，必须改变端口，配置文件位置：xxxx/conf/server.xml  
下面截图是解决了出现8080端口被占用的问题：  

![](/img/ecsinstalltomcat6.png)  

![](/img/ecsinstalltomcat7.png)  

![](/img/ecsinstalltomcat8.png)  

![](/img/ecsinstalltomcat9.png)  

![](/img/ecsinstalltomcat10.png)  

关于Tomcat其它问题都可以搜索网上的资料，如配置文件位置，日志位置，启动错误等，很多相关资料的。  

## 相关Linux命令导航  
java -version  
javac -version  
which java/javac  
tar -zcvf xxxx.tar.gz  
kill -9 3213
ps -ef|grep tomcat







   