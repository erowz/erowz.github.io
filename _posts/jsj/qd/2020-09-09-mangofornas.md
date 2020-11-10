---
date: 2020-09-09 18:23:00
title: 如何在NAS中部署漫画管理仓库mango
category: 博客-Nas
tags: [漫画,NAS,备忘]
---
# 前言
该版本的`mango`来自于这个[B站UP主](https://www.bilibili.com/video/BV1zQ4y1P7dn)的打包修改版。

本文只是docker-mango部署记录，备忘。

201110/更新  
经过一段时间的测试和使用后发现，这个版本的mango还存在着许多问题  
例如`回到之前阅读位置`功能的错乱，批量识别的不方便等（只能识别单个文件夹内的zip文件）  
建议还是前往github mango下载最新版
{:.error}

<!--more-->

# docker-tar包的下载地址
> 安装包需要部署到docker上，且是二次修改版本。所以要在**`映像/新增/从文件添加`**中自行安装。下面是tar 的下载地址。
{:.comment} 

链接:[https://pan.baidu.com/s/1V8Ds8anL9gWO_e9xIB6q7A]( https://pan.baidu.com/s/1V8Ds8anL9gWO_e9xIB6q7A)  提取码: qb5q

下载完成后，把tar包拖进NAS的任意一个文件夹里，只要你找得到就好。

然后手动安装。

加载完后双击新出现的映像，接下来进行**容器的配置**。
# 容器的配置
> 双击后点击**`高级配置`**
{:.comment} 

 - 在高级配置中点击**卷**，再点击**添加文件夹**，选择`data/mango/storage`的路径。
 
> 如果没有此文件夹，可以在`控制面板/共享文件夹/新增`里自行创建。

 - 在**装载路径**中粘贴`/root/mango`。
 
 以上是漫画的存放地址
 {:.info}

 - 再次点击**添加文件夹**，然后选择`data/mango/config`路径，如果没有可以自己创建。
 - 在**装载路径**中粘贴`/root/.config/mango`。
 
以上是漫画管理仓库的配置地址
 {:.info}

![img](http://pic.yupoo.com/erowz/23f5973a/fa5dd4e0.jpg){:.border width='650px'}{:.rounded.shadow}

----

完成卷的设置后，再点击高级设置里的**端口**

 - 添加新端口，本地端口`9001`，容器端口`9000`，切勿与其他端口冲突。
![img](http://pic.yupoo.com/erowz/15fc1eea/bb1f87e8.jpg){:.border width='650px'}{:.rounded.shadow}

----

在高级设置中勾选**创建桌面快捷方式**、点击子选项里的**网页**，输入`NAS ip+本地端口`。

如`http://192.168.1.111:9001`。

![img](http://pic.yupoo.com/erowz/5aed1048/a2827b16.jpg){:.border width='650px'}{:.rounded.shadow}

**点击 应用/下一步/应用 即配置完成**

# 登陆mango
应用后容器已经开始自动运行了~

我们可以在网页中输入`NAS ip+本地端口`进行登录。

但很有可能刷新不出来，这是因为我们还要做一件事。

选定容器后点击`详情`,再点击`终端机`，在终端机里`回车`，则会跳出管理库的admin账户密码。

![img](http://pic.yupoo.com/erowz/705cc1ac/dbef80b7.jpg){:.border width='650px'}{:.rounded.shadow}

复制它们，登陆`NAS ip+本地端口`，然后粘贴。

![img](http://pic.yupoo.com/erowz/3bd0c9eb/c8307dfa.jpg){:.border width='650px'}{:.rounded.shadow}

点击连接，可以进去漫画库啦，看图！

![img](http://pic.yupoo.com/erowz/fcaed1c2/e3a782dd.jpg){:.border width='650px'}{:.rounded.shadow}

# 修改mango用户密码
刚刚在终端分配的初始密码太难记

我们可以在mango里点击`管理/用户管理`进行修改

![img](http://pic.yupoo.com/erowz/2a493083/a3bbb1de.jpg){:.border width='650px'}{:.rounded.shadow}

# 添加漫画
漫画添加的路径，在容器配置时就已经设定好了

我的路径在`/data/mango/storage/library`下

只要将漫画的.zip文件拖入进去，就好了

在管理中选择`管理/扫描媒体库`即可对新添加的漫画进行匹配

下面是最终效果

![img](http://pic.yupoo.com/erowz/cd4e4c5d/04211f9d.jpg){:.border width='650px'}{:.rounded.shadow}

![img](http://pic.yupoo.com/erowz/2aa7e4eb/ee1ad9f3.jpg){:.border width='650px'}{:.rounded.shadow}

![img](http://pic.yupoo.com/erowz/668b695d/0c4f3ddb.jpg){:.border width='650px'}{:.rounded.shadow}

# 一些问题！
mango 的显示逻辑，是由一个个子集文件夹形成的

而单独丢进去一个[zip]压缩包

它！是！不！会！显！示！的！

```
----文件夹  
---------漫画.zip  
---------漫画.zip  
----文件夹  
---------漫画.zip  
---------漫画.zip  
```

必须如上

所以..

（强迫症福音 ×

强迫症+懒癌的噩梦 √
