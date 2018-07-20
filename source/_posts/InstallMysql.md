---
title: 远程安装Mysql
date: 2018-07-20 14:58:22
tags: [dvlp123456,2018,Mysql,技术]
categories: 技术
description: 远程安装Mysql
---

## 1.写在前面  

外地朋友机器安装Mysql出现问题，需要我协助安装下。     

<!--more-->

## 2.概述  

朋友是在外地的，所以需要进行远程协助，可以qq或者TeamViewer远程控制，此次选择TeamViewer进行远程控制朋友的电脑。  
电脑都是可以连接外网的。  

## 3.Mysql过程  

通过TeamViewer连接朋友电脑，检查到朋友机器没有目前没有安装mysql，而且没有安装包。把我本机的mysql-installer-community-5.6.12.2.msi传送到朋友的机器上，直接安装，发现无法安装上去，如下图：  

![](/img/InstallMysql1.jpg)    

此安装包在我本机上是可以正常安装的，机器配置也和朋友都是差不多的，都是64位win 10机器。一时间不知道原因。  
现在去Mysql官网下载一个最新的Mysql安装包：8.0.11的msi包，直接安装，还是和之前的安装情况一样。  
一时间找不到解决的办法。  
下载下其它的安装包尝试下...   
下载一个Mysql的zip包，执行bin文件夹里面的mysqld.exe  

![](/img/InstallMysql2.jpg)    

此时报无法找到dll文件，同时360也弹出修复的建议，也报了错误的原因：  

![](/img/InstallMysql3.jpg)

![](/img/InstallMysql4.jpg)        

因为朋友上次卸载Mysql时参照网上教程，操作了微软系统的注册表，导致一些类库被删除，所以msi包无法正常安装。  
让360帮忙修复：  

![](/img/InstallMysql5.jpg)

![](/img/InstallMysql6.jpg)      

![](/img/InstallMysql7.jpg)      

此时再去执行最新的Mysql安装包msi文件，最终安装成功：  

![](/img/InstallMysql8.jpg)      

![](/img/InstallMysql9.jpg)      

安装包会自动下载对应的安装包和安装。最终在“程序”中检查是否安装成功，并且启动Mysql和Mysql自带的client，检查全部正常：  

![](/img/InstallMysql10.jpg)      

## 4.第三方连接工具  

朋友想使用第三方连接工具Navicat，简单，把本机的Navicat传送到朋友机器上，直接连接，发现报以下错误:  

![](/img/InstallMysql11.png)      

我本机上的ok的，想着可能是Mysql不同版本导致的，搜索下此错误，关键字：navicat 1251，得到以下说明：https://blog.csdn.net/qq_36068954/article/details/80175755<font col="white">，参照方法参照，问题解决！</font>