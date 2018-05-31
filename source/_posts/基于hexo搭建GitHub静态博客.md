---
title: 基于hexo搭建GitHub静态博客
date: 2018-03-26 19:53:58
tags: [dvlp123456,2018,hexo,GitHub,技术]
categories: 技术
description: 基于hexo搭建GitHub静态博客
---

## 0.使用github pages服务搭建博客的好处
&ensp;&ensp;a:全是静态文件，访问速度快；<br/>
&ensp;&ensp;b:免费方便，不用花一分钱就可以搭建一个自由的个人博客，不需要服务器不需要后台；<br/>
&ensp;&ensp;c:可以随意绑定自己的域名，不仔细看的话根本看不出来你的网站是基于github的；<br/>
&ensp;&ensp;d:数据绝对安全，基于github的版本管理，想恢复到哪个历史版本都行；<br/>
&ensp;&ensp;e:博客内容可以轻松打包、转移、发布到其它平台；<br/>
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;备注：以上内容为网上摘抄的

<!--more-->

##  1.准备
- nodejs
- hexo
- git
- github
- markdown，markdownpad

&ensp;&ensp;概括说明：hexo是在nodejs基础上的一个应用，可以生成网站的代码，所以建议对nodejs有所了解；git用于提交文件到github上，github提供一个仓库，存放文件，供他人查看，相当于一个服务器；我们使用markdownpad编辑器编写markdown语言的博客。<br/>
&ensp;&ensp;对于以上提到的内容，建议有基础的了解。

##  2.环境&版本等

| 软件 | 版本 | 
|:----------------------:|:----------------------:|
|nodejs                 |v8.9.3|
|hexo                   |hexo-cli: 1.1.0 os: Windows_NT 10.0.10586 win32 x64 http_parser: 2.7.0 node: 8.9.3 v8: 6.1.534.48 uv: 1.15.0 zlib: 1.2.11 ares: 1.10.1-DEV modules: 57 nghttp2: 1.25.0 openssl: 1.0.2n icu: 59.1 unicode: 9.0 cldr: 31.0.1 tz: 2017b|
|git                    |git version 2.15.0.windows.1  |
|markdownpad            |2.5.x.x.x|
&ensp;&ensp;说明：github和markdown不是安装在本地的。本人是在windows系统下操作的。

##  3.步骤

###  （1）安装nodejs

&ensp;&ensp;到[官网](http://www.nodejs.org/)下载对应版本下载即可。<br/>
&ensp;&ensp;验证是否安装成功，在cmd环境中输入命令：<br/>
&ensp;&ensp;&ensp;&ensp;node -v<br/>
&ensp;&ensp;打印出对应版本信息即为安装成功。

###  （2）安装hexo

&ensp;&ensp;在cmd环境中输入命令：    <br/>
&ensp;&ensp;&ensp;&ensp;npm install -g hexo<br/>
&ensp;&ensp;全局安装hexo。<br/>
&ensp;&ensp;验证是否安装成功，在cmd环境中输入命令：<br/>
&ensp;&ensp;&ensp;&ensp;hexo version<br/>
&ensp;&ensp;打印出对应版本信息即为安装成功。

###  （3）安装git

&ensp;&ensp;具体步骤省略。<br/>
&ensp;&ensp;下载Windows版本的git，安装并测试。检查是否安装成功方法：在任何一个文件夹下右键，看到有Git Bash Here等。

###  （4）申请github账号

&ensp;&ensp;如果没有方便使用的邮箱，可以重新申请一个邮箱，如163的。然后申请github账号，[github官网](https://github.com)。申请github后创建自己的仓库，创建仓库时有一个要求，如图：
![](/img/1.png)
&ensp;&ensp;当然这是把此github账号用于建立静态博客的要求。

###  （5）安装markdownpad

&ensp;&ensp;markdownpad主要用来使用markdown语言（不能说是一门语言，说是一种语法更准确）来编写博客。下载安装后要破解，怎么破解你懂的，在国内破解码到处都是，没有破解的话很多功能不可以使用。另外editplus和sublime text等文本编辑工具都可以编写markdown页面，也可以实时的去浏览效果，markdownpad仅仅是其中一个工具而已。  
&ensp;&ensp;我本机上安装的是markdownpad2 2.5.x.x版本。由于本机是windows 10，此软件的实时效果（即右边的即时浏览功能）无法使用。此时需要本机安装另外一个软件：awesomium_v1.6.6_sdk_win.exe。安装好后重启markdownpad即可。

###  （6）创建hexo和git工作目录

&ensp;&ensp;声明：工作目录可以在本地任何地方。如创建hexo目录E:\XXX\XXX\hexo，XXX表示某一个目录。  
&ensp;&ensp;在cmd环境中进入到目录E:\XXX\XXX\hexo，创建hexo工程，用于存放hexo博客工程，名字：blog（随意起的），命令：  
&ensp;&ensp;&ensp;&ensp;hexo init blog  
&ensp;&ensp;得到以下目录（cmd环境查看）：  

    E:\ ***\***\hexo\blog>ls -l   
    total 177
    -rw-r--r-- 1 danz 197121  1846 Mar 26 10:30 _config.yml    
    drwxr-xr-x 1 danz 197121     0 Mar 26 10:35 node_modules    
    -rw-r--r-- 1 danz 197121 91498 Mar 26 10:35 package-lock.json  
    -rw-r--r-- 1 danz 197121   443 Mar 26 10:35 package.json  
    drwxr-xr-x 1 danz 197121     0 Mar 26 10:30 scaffolds  
    drwxr-xr-x 1 danz 197121     0 Mar 26 10:30 source  
    drwxr-xr-x 1 danz 197121     0 Mar 26 10:30 themes 

&ensp;&ensp;目录说明：  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;themes  --hexo主题存放位置  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;source   --我们编写markdown文件存放位置  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;_config.yml    --hexo全局配置文件  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;node_modules  --依赖文件  
&ensp;&ensp;建立好blog工程后，默认为我们生成一个hello-world实例。此时可在cmd环境中在目录blog下输入：  
&ensp;&ensp;&ensp;&ensp;hexo s 或者  
&ensp;&ensp;&ensp;&ensp;hexo server  
&ensp;&ensp;&ensp;&ensp;在浏览器输入： http://localhost:4000/ ，可以浏览hello文件效果；  
![](/img/2.png)
&ensp;&ensp;创建git工作目录，E:\XXX\XXX\hexo\blog_commit_to_github，用于存放上传博客到github仓库的。

###  （7）把hello实例上传到github，并在浏览器中浏览自己的博客

&ensp;&ensp;a：使用hexo把hello-world.md（E:\ XXX\XXX\hexo\blog\source\_posts）编译为静态网站文件，在cmd环境中进入到目录E:\XXX\XXX\hexo\blog，输入命令：  
&ensp;&ensp;&ensp;&ensp;hexo g 或者  
&ensp;&ensp;&ensp;&ensp;hexo generate  
&ensp;&ensp;得到目录：  

    E:\ XXX\XXX\hexo2\blog>ls -l
    total 209
    -rw-r--r-- 1 danz 197121  1846 Mar 26 10:30 _config.yml
    -rw-r--r-- 1 danz 197121 25047 Mar 26 10:46 db.json
    drwxr-xr-x 1 danz 197121     0 Mar 26 10:35 node_modules
    -rw-r--r-- 1 danz 197121 91498 Mar 26 10:35 package-lock.json
    -rw-r--r-- 1 danz 197121   447 Mar 26 10:39 package.json
    drwxr-xr-x 1 danz 197121     0 Mar 26 10:46 public
    drwxr-xr-x 1 danz 197121     0 Mar 26 10:30 scaffolds
    drwxr-xr-x 1 danz 197121     0 Mar 26 10:30 source
    drwxr-xr-x 1 danz 197121     0 Mar 26 10:30 themes

&ensp;&ensp;目录说明：  
&ensp;&ensp;&ensp;&ensp;此时会生成一个public文件夹，里面就是我们需要上传的文件。

&ensp;&ensp;**如果出现一些莫名其妙的问题，可以先执行hexo clean来清理一下public的内容，然后再来重新生成和发布。**

&ensp;&ensp;**生成文件是依照hello world.md生成的，如果我们自己使用markdownpad编写了`*`.md文件，把对于文件复制到E:\XXX\XXX\hexo\blog\source\_posts目录，然后重新生成文档即可。**

&ensp;&ensp;b:在cmd环境中进入到目录E:\XXX\XXX\hexo\ blog_commit_to_github，输入命令：  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;git clone https://github.com/XXX/XXX.github.io.git  
&ensp;&ensp;XXX是我们申请github账号的名字，步骤（4）中隐藏的部分，如git clone https://github.com/dvlplife/dvlplife.github.io.git。把github仓库同步到本地。  

    E:\ ***\***\hexo\blog_commit_to_github>ls -l
    total 0
    drwxr-xr-x 1 danz 197121 0 Mar 26 10:54 XXX.github.io

&ensp;&ensp;会生成一个XXX.github.io文件夹。  
&ensp;&ensp;把public目录下所有文件，复制到XXX.github.io文件夹下。  
&ensp;&ensp;去到XXX.github.io文件夹下，鼠标右击选择Git Bash Here，输入命令：  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;git add . // 添加修改  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;git commit -m "备注" // 提交  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;git push origin master // 上传到GitHub代码库  
&ensp;&ensp;执行这些步骤的时候不要错误，有错误的话，可以查看是什么错误，然后按照错误提示去修正即可。

&ensp;&ensp;c:上传成功后，此时可以到github的主页看是否有已经上传的文件：  
![](/img/3.png)

&ensp;&ensp;去浏览器输入：https:// /XXX/XXX.github.io，即可访问到我们存放在github的博客了：
![](/img/4.png)
&ensp;&ensp;**路径：https:// /XXX/XXX.github.io即是我们私人博客地址了。**

&ensp;&ensp;d:下图是提交第二个文件到github的截图，可以看到，没有改动的文件是不会再次提交的：    

![](/img/5.png)

&ensp;&ensp;提交一个测试文档到github中  --第二次提交的文件  
&ensp;&ensp;上传hexo hello world文件到github中  --第一次提交的文件  

###  （附录）命令快速浏览

&ensp;&ensp;node –v  
&ensp;&ensp;npm install -g hexo  
&ensp;&ensp;hexo version  
&ensp;&ensp;hexo init blog  
&ensp;&ensp;hexo new "postName"  //新建文章  
&ensp;&ensp;hexo new page "pageName"  //新建页面  
&ensp;&ensp;hexo clean  
&ensp;&ensp;hexo s 或者  
&ensp;&ensp;hexo server  
&ensp;&ensp;hexo g 或者  
&ensp;&ensp;hexo generate  
&ensp;&ensp;git add . // 添加修改  
&ensp;&ensp;git commit -m "备注" // 提交  
&ensp;&ensp;git push origin master // 上传到GitHub代码库  

###  （附录）hexo主题的更换等

&ensp;&ensp;默认主题很丑，我们可以挑选喜欢的主题，官网：https://hexo.io/themes/，如主题：hexo-theme-jekyll 和 hexo-theme-yilia。  
&ensp;&ensp;下载主题到本地，在cmd环境中去到bog目录中，输入命令：  
&ensp;&ensp;git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia  
&ensp;&ensp;下载成功后在themes文件夹中可以到yilia。  
&ensp;&ensp;修改_config.yml中的theme: landscape改为theme: yilia，然后重新执行hexo g来重新生成。  
&ensp;&ensp;如果出现一些莫名其妙的问题，可以先执行hexo clean来清理一下public的内容，然后再来重新生成和发布。  
&ensp;&ensp;**另外可以定义404网页等，美化完善等工作可以自己摸索。**















