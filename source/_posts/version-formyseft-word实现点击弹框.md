---
title: word实现点击弹框功能
date: 2018-05-28 22:51:23
tags: [dvlp123456,2018,word,技术]
categories: 技术
description: word实现点击弹框功能
---

## 来龙去脉介绍-ysz2  

受朋友之托，想要在word里面实现插入一张某个省份的地图，如，湖南省的，然后点击地图中的某个市，实现弹窗功能。   
基于以上需求分析：需要在图片上加上点击事件。  
<!--more-->

## 开始尝试  

平常使用word都不需要点击事件的，经过网上搜索得知**word一般用于文字的处理**，其它花哨（相对来说）功能较少，搜索得到两个比较有用的信息：  
> 1、新建一word文档。  
> 2、在[控件工具箱]中双击[图像]控件，图像框添加到word文档中。  
> 3、在word文档中的图像框上右单击鼠标，选择[属性]，弹出[属性]对话框，在AutoSize属性选择true，在Picture属性选择你想要的图片，然后关闭属性对话框。  
> 4、在word文档中，双击[图像框]控件，它打开Microsoft Visual Basic编辑器，并呈现以下代码：  
> Private Sub Image2_Click()
> 
> End Sub  
> 5、在子程序中输入msgbox "单击了图片",象以下这样：  
> Private Sub Image2_Click()  
>    msgbox "单击了图片"  
> End Sub    
> 6、关闭Microsoft Visual Basic编辑器。  
> 7、保存word文档，然后关闭word文档。  
> 8、打开刚编辑好的word文档，单击一下[图像框]试试  
> 9、如果想在单击[图像框]后完成其它任务，添加修改子程序中的语句即可。    
> Private Sub Image2_Click()  
>    '你的语句在这里  
>    '你的语句在这里  
>    '  
>    '  
> End Sub    

资料一摘自：https://bbs.csdn.net/topics/320012224  
另外一份资料是word对VBA基础教学，题目是：WORD-VBA编程-从零开始学VBA，地址：https://wenku.baidu.com/view/7928f6e16e1aff00bed5b9f3f90f76c661374c25.html  
经过以上两个资料的学习以及入门操作对offic的word中的vba有了一定了认识。要完成我们的目标，应该是使用vba和word开发工具菜单里面的一些控件。

## 第二次尝试  

在以上的尝试后，现尝试其中一条可能性。具体做法如下： 
 
### 步骤：  

网上下载合适的一张湖南地图，如下：  

![](/img/word-map-hunan1.jpg)   

使用picpick工具对原图进行挖字和画色回去得到下图：  

![](/img/word-map-hunan2.jpg)    

继续使用picpick工具制作对应颜色的市名称，得到：  

![](/img/word-map-hunan3.gif)  
![](/img/word-map-hunan4.gif)   
![](/img/word-map-hunan5.gif)    
![](/img/word-map-hunan6.gif)    
![](/img/word-map-hunan7.gif)    

打开word，新建，插入处理后的湖南地图，word添加开发工具菜单，步骤如下：  

![](/img/word-map-hunan8.png)  

选中设计模式，即打开word的设计模式。  
在word空白处添加开发工具里面的图像（activeX控件），右击图像控件--属性，属性对话框里面的Picture选中对应名字的图片，如长沙市，去掉控件的border属性，步骤如图：  

![](/img/word-map-hunan9.png)  

右击图像控件，进行位置属性设置，设置后可以把此控件放置到对应图片的位置，如果图长沙市的位置：  

![](/img/word-map-hunan10.png)  

对控件进行事件设置，双击控件，进入vbe环境，写上控件处理内容，如弹窗，保存，关闭设计模式，此时去点击控件，会弹出对应文字，如图：  

![](/img/word-map-hunan11.png)  
![](/img/word-map-hunan12.png)  

其它市也是同样的步骤。  
至此图片上面有了点击事件。  

## 总结  

1.只能在文字上点击，其实是点击了控件，才会有事件响应；  
2.目前是弹窗显示一点内容，或者是简单的交互，实现在截图（点击事件处理方法：弹窗显示）的下面；  
3.能不能输入内容后填入word的表格里面？；
4.能不能弹一个表格出来展示，如应用场景：点击某一地区展示此地区的人员信息，或者地区的介绍？  

## 所有资源  

[所有资源下载](/download/word_excel.rar)  