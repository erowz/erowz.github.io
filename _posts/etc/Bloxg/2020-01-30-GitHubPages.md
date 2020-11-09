---
date: 2020-01-30 19:28
title: GirHub Blog - GitHub Pages
category: Blog
# permalink: /blog/github-pages
tags: [github, pages, blog, jekyll]
# published: false
---
{% assign path = page.imgpath | append: page.id %}

# GitHub Pages 생성하기

> **REF**  
> [GitHub Help - Page](https://help.github.com/en/github/working-with-github-pages)  
> [TeXt Theme Help](https://tianqi.name/jekyll-TeXt-theme/docs/en/quick-start)

![GitHub Pages]({{path}}/img01.png){:width='400px'}  
*출처 : [https://youtu.be/2MsN8gpT6jY](https://youtu.be/2MsN8gpT6jY){:target='_blank'}*

# GitHub Pages 생성

**\* 주의**

- GitHub Pages  
    : 저장소가 비공개여도 페이지는 공개 상태이므로 비공개 데이터가 있는 경우 지우고 배포해라.  
    : GitHub Pages sites are publicly available on the internet, even if their repositories are private. If you have sensitive data in your site's repository, you may want to remove it before publishing.

### Git Repository 생성

1. 새 repository 생성  
    ![GitHub Pages]({{path}}/img02.png){:width='160px'}
2. name 입력 후 생성  
    ![GitHub Pages]({{path}}/img03.png){:.border width='600px'}
3. 생성 확인  
    : 생성 시 입력한 이름으로 접속해보면 페이지 확인 가능  
    ![GitHub Pages]({{path}}/img04.png){:.border width='400px'}

### 기본 Theme 지정하기

- Setting Tab > GitHub Pages  
    : 기본 테마 중 선택해서 적용 가능
    ![GitHub Pages]({{path}}/img05.png){:.border width='600px'}
- 커스텀 테마 적용하기  
    : 기본 테마가 마음에 들지 않을 경우 커스텀 제작된 테마 적용 가능 (다른 포스트에 정리)