---
date: 2020-02-13 19:48 +09:00
title: Jekyll - Category 설정
category: Blog
# permalink: /blog/jekyll-category
tags: [jekyll, categroy]
# published: false
---
{% assign path = page.imgpath | append: page.id %}

> MEMO  
> 나는 [Jekyll-TeXt-Theme](https://tianqi.name/jekyll-TeXt-theme/)을 사용하고 있어서 해당 프로젝트를 바탕으로 작성함

Navigation Bar에 카테고리를 설정하고 싶어서 방법을 찾아보았다.

# 설정하는 법

## catetory list

1. /category 폴더 생성 
2. 파일명 \[category name\].md 형식으로 각 카테고리별 파일 생성  
  ![categories]({{path}}/img01.png){:width='140px'}

- recently  
  ```markdown
  ---
  title: Algorithm
  permalink: /algorithm
  ---
  ```
- Before  
  ```markdown
  ---
  layout: category
  title: Algorithm
  permalink: /algorithm
  sidebar:
      nav: nav-kr
  ---
  ```
   - title : 카테고리 이름
   - permalink : 링크 관리 
   - ~~sidebar : 카테고리별 포스트 목록 페이지에 sidebar를 포함시키기 위해 설정~~ &rArr; _config.yml에 기본 설정으로 대체

## _config.yml
- 공통 속성 설정하기 : layout, sidebar

```yml
defaults:
  ...
  - scope:
      path: "category"
    values:
      layout: category
      sidebar:
        nav: nav-kr
```

## navigation list

- /_data/navigation.yml 에 nav list 추가 

  ```yaml
  nav-kr:
  - title: Data Science
    children:
      - title:  Big Data
        url:    /bigdata
      - title:  Stats
        url:    /stats
  - title: Python
    children:
      - title:  Python
        url:    /python
  - title: ETC
    children:
      - title:  Blog
        url:    /blog
  ```

## category page

1. _layouts/category.html

  ```html
  ---
  layout: articles
  show_title: true
  articles:
    data_source: site.category
    article_type: BlogPosting
    show_cover: false
    show_excerpt: true
    show_info: true
    type: item
  ---
  {% raw %}
    <div class="layout--home">
      {%- include paginator.html -%}
    </div>
    <script>
      {%- include scripts/home.js -%}
    </script>

    {{ content }}
  {% endraw %}
  ```

2. articles.html 수정

```html
{%- raw -%}
{%- for _key in _keys -%}
  {%- if forloop.first -%}
    {%- case _key -%}
      {%- when 'site' -%}
        {%- assign _articles = site -%}
      {%- when 'page' -%}
        {%- assign _articles = page -%}
      {%- when 'layout' -%}
        {%- assign _articles = layout -%}
      {%- when 'paginator' -%}
        {%- assign _articles = paginator -%}
      {%- else -%}
        {%- assign _articles = site[_key] -%}
      {%- else -%}
    {%- endcase -%}
  {%- else -%}
    <!-- # 카테고리용 포스트 지정 -->
    {%- if _key == 'category' -%}
      {%- assign _articles = site.categories[page.title]-%}
    {%- else -%}
      {%- assign _articles = _articles[_key] -%}
    {%- endif -%}
  {%- endif -%}
{%- endfor -%}

{% endraw %}
```

# Output

Navigation Bar를 포함한 기타 등등의 자잘한 CSS까지 정리된 현재의 결과물이다.

![Navi Bar]({{path}}/img02.png){:.border width='600px'}

> **REF**  
> [DevYurim](https://devyurim.github.io/DE/Github%20Blog){:target="_blank"}
