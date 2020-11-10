---
title: 如何添加音乐、视频、PPT？
permalink: /docs/Advanced_extended_usage
key: docs-Advanced-extended-usage
---
  
## 音频
可以添加**声云**和**网易云音乐**的音乐此处只以网易云音乐作示范。

### 网易云音乐

**获取id如图:**

![extensions-soundcloud](http://pic.yupoo.com/erowz/9b7c31fa/d0785e6b.jpg){:style="max-height:320px"}{:.border}
  
**markdown语法:**
  
```markdown
<div>{%- include extensions/netease-cloud-music.html id='28638802' -%}</div>
```

修改【id='xxxx'】中的数字即可，ID的获取方式如上图
{:.info} 

**效果展示：**  

<div>{%- include extensions/netease-cloud-music.html id='19027624' -%}</div>


## 视频

视频可以插入“YouTube”、“TED”、“哔哩哔哩”的视频，由于某些原因，此处只以哔哩哔哩的视频作示范。
  
### 哔哩哔哩

**获取id如图:**

![extensions-bilibili](http://pic.yupoo.com/erowz/98c6a6f6/da97a594.jpg){:style="max-height:190px"}{:.border}

**markdown语法:**

```
<div>{%- include extensions/bilibili.html id='73467462' -%}</div>
```
  
修改【id='xxxx'】中的数字即可，ID的获取方式如上图
{:.info}
  
**效果展示：**  
  
<div>{%- include extensions/bilibili.html id='73467462' -%}</div>
  
## 幻灯片
  
幻灯片是是引用的**SlideShare**的ppt，如果你想在文章里添加ppt，必须上传到**SlideShare**，这里不作示范。
  
### SlideShare

**id获取:**

![extensions-slideshare](https://raw.githubusercontent.com/kitian616/jekyll-TeXt-theme/master/docs/assets/images/extensions-slideshare.jpg){:style="max-height:480px"}{:.border}

**markdown语法:**

```
<div>{%- include extensions/slideshare.html id='u9L9zDsqEWNKE1' -%}</div>
```
  