---
date: 2020-01-31 00:16
title: GirHub Blog - Jekyll Theme
category: Blog
# permalink: /blog/jekyll-themes
tags: [github, pages, blog, jekyll]
# published: false
---
{% assign path = page.imgpath | append: page.id %}

# Jekyll Theme 사용해보기

> **REF**  
> [GitHub Desktop](https://desktop.github.com/){:target='_blank'}  
> [Jekyll Theme 공식 사이트](https://jekyllthemes.io/){:target='_blank'}  
> [Jekyll theme을 사용하여 블로그 생성하기](https://devinlife.com/howto%20github%20pages/new-blog-from-template/){:target='_blank'}  

### 블로그 설정 과정

1. 로컬에 테마 설치
2. 테마 수정
3. GitHub에 배포
   - GitHub Pages 생성
   - Git Push

# Jekyll Theme 선택

### Theme

- [jekyll-TeXt-theme](https://tianqi.name/jekyll-TeXt-theme/){:target='_blank'}
- [Doc](https://tianqi.name/jekyll-TeXt-theme/docs/en/update-from-1-to-2)  
    ![Image]({{path}}/img01.png){:width='300px'} 

### Theme List

|[**Documentation Jekyll theme**](https://jekyllthemes.io/theme/documentation){:target='_blank'} |[**Just The Docs Jekyll theme**](https://jekyllthemes.io/theme/just-the-docs){:target='_blank'} |[**Docs Jekyll theme**](https://jekyllthemes.io/theme/docs-responsive-documentation-or-manual-jekyll-theme){:target='_blank'}
|:-:|:-:|:-:
|![Image]({{path}}/img02.jpeg){:width='300px'} |![Image]({{path}}/img03.jpeg){:width='300px'} |![Image]({{path}}/img04.jpeg){:width='300px'}
|[**Leonids Jekyll theme**](https://jekyllthemes.io/theme/leonids){:target='_blank'} |[**Minimal Mistakes Jekyll theme**](https://jekyllthemes.io/theme/minimal-mistakes){:target='_blank'} |[**Online CV**](https://jekyllthemes.io/theme/online-cv){:target='_blank'} |
|_이력서, 카테고리 보유_ |  |_온라인 이력서 작성 시 좋을 듯_ |
|![Image]({{path}}/img05.jpeg){:width='300px'} |![Image]({{path}}/img06.jpeg){:width='300px'} |![Image]({{path}}/img07.jpeg){:width='300px'}
|[**Meuse Jekyll theme**](https://jekyllthemes.io/theme/meuse-multi-purpose-theme-powered-by-jekyll){:target='_blank'} |  |  |
|_$24_ |  |  
|![Image]({{path}}/img08.jpeg){:width='300px'} |  |  |

# jekyll-TeXt-theme

- 참고 : [TeXt Theme](https://github.com/kitian616/jekyll-TeXt-theme){:target='_blank'}  
    ![Image]({{path}}/img09.png){:width='600px'}  
    *출처 : jekyll_TeXt-theme*

1. install the theme
    1. common method
    2. ruby gem method : setup your site 필요
2. setup your site
3. local preview for development, build and publish.

### Install Theme

1. fork theme git  
    : git clone을 통해서도 가능  
    : github pages 사용 시 fork로 간단하게 적용 가능하므로 편한 방법을 선택할 것
    
    - [jekyll-Text-theme](https://github.com/kitian616/jekyll-TeXt-theme){:target='_blank'} github 방문
    - fork git  
        ![Image]({{path}}/img10.png){:width='600px'}
2. 내 github 설정
    
    - repository rename  
        ![Image]({{path}}/img11.png){:width='600px'}
    - page 접속 확인  
        ![Image]({{path}}/img12.png){:width='600px'}

### Local Preview

- git clone  
    ![Image]({{path}}/img13.png){:width='300px'}

```
$git clone https://github.com/willnfate/willnfate.github.io.git
$cd willnfate.github.io.git

# 설치
$bundle
Using jekyll-text-theme 2.2.6 from source at `.`
Bundle complete! 3 Gemfile dependencies, 42 gems now installed.
Use `bundle info [gemname]` to see where a bundled gem is installed.
Post-install message from html-pipeline:
-------------------------------------------------
Thank you for installing html-pipeline!
You must bundle Filter gem dependencies.
See html-pipeline README.md for more details.
https://github.com/jch/html-pipeline#dependencies
-------------------------------------------------

# 서버 실행 // $jekyll serve 
$ bundle exec jekyll serve
Configuration file: /Users/minky/work/willnfate.github.io/_config.yml
            Source: /Users/minky/work/willnfate.github.io
       Destination: /Users/minky/work/willnfate.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 1.162 seconds.
 Auto-regeneration: enabled for '/Users/minky/work/willnfate.github.io'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```

![Image]({{path}}/img14.png){:width='600px'}

### Build and Publish

If you host your site on GitHub Pages, just push the source to the master branch of your USERNAME.github.io repository, GitHub would build automatically. You can visit your site on [https://USERNAME.github.io](https://USERNAME.github.io){:target='_blank'} several minutes later.

If you host your site on your server, you need first run JEKYLL\_ENV=production bundle exec jekyll build to generated your site, then update the files in \_site folder to your server.

이제 기본 설치가 완료되었다!!

# Skin Customizing

> **REF** [Configuration](https://tianqi.name/jekyll-TeXt-theme/docs/en/configuration){:target='_blank'}

### 스킨 설정

```
text_skin: default # "default" (default), "dark", "forest", "ocean", "chocolate", "orange"
```

### MathJax 설정

### \_config.yml

```
## Mathjax
mathjax: true # false (default), true
mathjax_autoNumber: false # false (default), true << 자동 수식 번호매기기 해제
```

#### text align

mathjax.html > \_config에 displayAlign과 displayIndent 추가

- 추가 코드

```html
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  displayAlign: "left",
  displayIndent: "2em"
});
</script>
```
   
- 적용 예

```html
{%- raw -%}
{%- include snippets/get-sources.html -%}
{%- assign _sources = __return -%}

{%- include snippets/assign.html target=site.data.variables.default.mathjax_autoNumber
  source0=site.mathjax_autoNumber source1=page.mathjax_autoNumber -%}
{%- assign _mathjax_autoNumber = __return -%}

<script type="text/x-mathjax-config">
    var _config = { 
        tex2jax: {
            inlineMath: [['$','$'], ['\\(','\\)']]
        },
        displayAlign: "left",
        displayIndent: ".5em"
    };
    {%- if _mathjax_autoNumber == true -%}
        _config.TeX = { equationNumbers: { autoNumber: "all" } };
    {%- endif -%}
    MathJax.Hub.Config(_config);
</script>
<script type="text/javascript" src="{{ _sources.mathjax }}" async></script>
{% endraw %}
```