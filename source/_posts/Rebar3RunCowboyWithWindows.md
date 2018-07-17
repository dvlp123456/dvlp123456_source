---
title: 在Windows环境下使用rebar3运行cowboy例子
date: 2018-07-1 20:14:23
tags: [dvlp123456,2018,erlang,rebar3,cowboy,技术]
categories: 技术
description: 在Windows环境下使用rebar3运行cowboy例子
---

## 1.说明  

此篇文章目标如题。   

<!--more-->

## 2.环境  

- <font color="BlueViolet">Windows10</font>  
- <font color="BlueViolet">rebar3</font>  
- <font color="BlueViolet">cowboy</font>  

## 3.rebar3执行文件的生成  

github上下载rebar3，地址：https://github.com/erlang<font color="white">，然后执行里面的bootstrap.bat文件，得到：rebar3和rebar3.cmd文件，复制到任何想要执行rebar3的地方。rebar前面的版本好像有问题，无法成功的执行bootstrap.bat文件，自然无法得到对应的rebar3和rebar3.cmd文件。</font>  

本机上有三个版本的erlang，分别是：Erlang/OTP R15B03，Erlang/OTP 18，Erlang/OTP 19.2，默认使用，Erlang/OTP R15B03  

## 4.使用rebar3  

参考文章：https://my.oschina.net/shadowolf/blog/1593767  

### 1.把rebar3和rebar3.cmd文件放到当前目录下，创建工程：  

``` erlang
C:\Users\danz\erl\1>rebar3 new app test_cowboy
Hi,I am .erlang file.

=ERROR REPORT==== 17-Jul-2018::16:36:58 ===
beam/beam_load.c(1670): Error loading module bbmus	tache:
  This BEAM file was compiled for a later version of the run-time system than R15B03.
  To fix this, please recompile this module with an R15B03 compiler.
  (Use of opcode 156; this emulator supports only up to 153.)


=ERROR REPORT==== 17-Jul-2018::16:36:58 ===
Loading of c:/Users/danz/erl/1/rebar3/bbmustache/ebin/bbmustache.beam failed: badfile
===> Uncaught error in rebar_core. Run with DEBUG=1 to see stacktrace or consult rebar3.crashdump
===> When submitting a bug report, please include the output of `rebar3 report "your command"`
```   

默认使用erlang版本：Erlang/OTP R15B03，改为使用Erlang/OTP 18，erlang版本：  

``` erlang
C:\Users\danz\erl\1>rebar3 new app test_cowboy
Hi,I am .erlang file.
===> Writing test_cowboy/src/test_cowboy_app.erl
===> Writing test_cowboy/src/test_cowboy_sup.erl
===> Writing test_cowboy/src/test_cowboy.app.src
===> Writing test_cowboy/rebar.config
===> Writing test_cowboy/.gitignore
===> Writing test_cowboy/LICENSE
===> Writing test_cowboy/README.md
```   

非常顺畅的执行成功了。  

### 2.参照文章改造文件  

### 3.把rebar3和rebar3.cmd文件放置到test_cowboy目录中，编译工程：    

``` erlang
C:\Users\danz\erl\1\test_cowboy>rebar3 compile
Hi,I am .erlang file.
===> Fetching rebar3_run ({git,"git://github.com/tsloughter/rebar3_run.git",
                               {branch,"master"}})
===> Compiling rebar3_run
===> Verifying dependencies...
===> Fetching cowboy ({git,"git://github.com/extend/cowboy.git",{tag,"1.0.0"}})
===> Fetching cowlib ({git,"git://github.com/extend/cowlib.git","1.0.0"})
===> WARNING: It is recommended to use {branch, Name}, {tag, Tag} or {ref, Ref}, otherwise updating the dep may not work as expected.
===> Fetching ranch ({git,"git://github.com/extend/ranch.git","1.0.0"})
===> WARNING: It is recommended to use {branch, Name}, {tag, Tag} or {ref, Ref}, otherwise updating the dep may not work as expected.
===> Compiling cowlib
===> Compiling ranch
===> Compiling cowboy
===> Compiling test_cowboy
src/test_cowboy_1.erl:10: Warning: variable 'Param1' is unused
src/test_cowboy_1.erl:11: Warning: variable 'Param2' is unused
```   

### 4.启动应用：  

``` erlang
C:\Users\danz\erl\1\test_cowboy>rebar3 shell
Hi,I am .erlang file.
===> Verifying dependencies...
===> Compiling test_cowboy
===> The rebar3 shell is a development tool; to deploy applications in production, consider using releases (http://www.rebar3.org/docs/releases)
Eshell V7.1  (abort with ^G)
1> ===> Booted ranch
1> ===> Booted cowlib
1> ===> Booted cowboy
1>	===> Booted test_cowboy
```   

### 5.
浏览器访问：http://localhost:8003/test_cowboy_1  
得到结果：Hello Erlang!  

### 6.测试工程文件  

测试工程下载：[下载(test_cowboy.rar)](/download/test_cowboy.rar)  