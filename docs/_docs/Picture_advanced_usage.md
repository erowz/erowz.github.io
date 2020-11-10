---
#layout: article
title: 文章中插入图片的高级用法
date: 2020-07-27
permalink: /docs/Picture_advanced_usage
key: docs-Picture-advanced-usage
---  
上一种插入图片的方式比较简单粗暴，直接占满了整个屏幕，可我们有时图片太小，或想要在图片旁边一侧打字，或为图片加上特效该如何实现呢?下面以一张小鱼的图片作为示例。  
这是小鱼的网络地址：[http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg)  
最简单粗暴的效果是这样的：  
![img](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg) 
  

##　图片的高级用法
  
| 样式名称 |
| ---- |
| **方形图片** |
| **阴影图片** |
| **圆角图片** |
| **圆形图片** |
  
### 方形图片

```markdown
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.border}
**这是右侧显示的文字**
```
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.border}
**这是右侧显示的文字**
    
### 阴影图片
```markdown
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.shadow}
```
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.shadow}
  
### 圆角图片
```markdown
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.rounded}
```
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.rounded}  
  
### 圆形图片
```markdown
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.circle}
```
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.circle}

## 混合用法

### 方形+圆角
```markdown
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.border.rounded}
```
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.border.rounded}
  
### 圆形+阴影  
```markdown
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.circle.shadow}
```
![Image](http://pic.yupoo.com/erowz/19de4592/f9ace13f.jpg){:.circle.shadow}
  