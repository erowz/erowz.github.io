---
#layout: article
title: 如何在文章中插入图片
date: 2020-07-27
permalink: /docs/How_to_insert_pictures
key: docs-How-to-insert-pictures
---  
文章中插入图片的方式很简单，但是你首先得知道一件事情，你所插入的图片地址是什么？  
图片地址，一般来说，就是它存于某服务器的路径  
类似于：http://www.xxxx.com/xxx/xxxxx/xxx/xxx.jpg  
一旦得知了这个地址，我们就可以把这个图片贴到文章内了。  
  
我们可以把它上传到github的网站文件内，这样只要我们的网站文件存在，我们的图片地址就不会丢失。  
但这样也会导致一个新问题————那就是，访问图片会很慢，甚至会打不开，因为github的服务器地址在美国。
为了解决这个问题，我强烈建议把网站内的所有图片都上传至国内的图床，这样就可以很完美的解决图片加载过慢的问题。  
我常用的图床是[yupoo](yupoo.com)，它是免费的，只要注册就可以使用。  
往网站中上传图片即可获得该图片的网络地址。  
下面是一些实操。  
#### 上传图片至yupoo  
我截了一张Bing的封面图，然后想发布在文章内。  
于是我就可以先在yupoo上传，如图：  
![img](http://pic.yupoo.com/erowz/76253710/c8e3704e.jpg)  
再点击上传后的链接图标，我便得到了该图片的网络地址  
![img](http://pic.yupoo.com/erowz/016f1ae2/7dde3b03.jpg)  
#### 在文章中添加
它的网络地址是“http://pic.yupoo.com/erowz/e5a9dc5d/991ac2f6.jpg ”  
于是我们就可以将它添入至文章内  
下面是添加的语法示范和展示：
```markdown
![img](http://pic.yupoo.com/erowz/e5a9dc5d/991ac2f6.jpg)
```
于是就会得到图片:  
![img](http://pic.yupoo.com/erowz/e5a9dc5d/991ac2f6.jpg)  

注意一定要使用英文输入法，开头一定要有英文的叹号!,"[]"内是该图片的名字，可以偷懒简写为img。括号内是该图的网络地址。
{:.error}