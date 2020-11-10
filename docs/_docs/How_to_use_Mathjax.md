---
#layout: article
title: 如何在文章中使用数学公式？
date: 2020-07-06
permalink: /docs/How_to_use_Mathjax
key: docs-How-to-use-Mathjax
mathjax: true
mathjax_autoNumber: true
---  

## 使用前提  
  

要想使用数学公式系统，必须要在文章的头部内添加开启的声明
{:.warning}

**如下示例：**
```markdown
...
mathjax: true
mathjax_autoNumber: true
---
```
  
## 使用教程  
  
markdown的数学公式教程，已有前人作了较完善的使用手册，请移至[此处](https://blog.csdn.net/dabokele/article/details/79577072)查看
{:.info}
下面只是示例与展示。  
  
## 示例与展示  
```markdown
$$\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.$$
```
  
$$\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.$$  
  
---  
```markdown
当 $$a \ne 0$$, 有两种解 $$ax^2 + bx + c = 0$$ 它们是
$$x_1 = {-b + \sqrt{b^2-4ac} \over 2a}$$
$$x_2 = {-b - \sqrt{b^2-4ac} \over 2a} \notag$$
```
  
当 $$a \ne 0$$, 有两种解 $$ax^2 + bx + c = 0$$ 它们是
$$x_1 = {-b + \sqrt{b^2-4ac} \over 2a}$$
$$x_2 = {-b - \sqrt{b^2-4ac} \over 2a} \notag$$