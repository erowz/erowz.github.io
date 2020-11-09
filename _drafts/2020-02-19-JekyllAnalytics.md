---
date: 2020-02-19 06:30:00 +0900
title: Jekyll - Google Analytics 설정
category: Blog
tags: [blog, jekyll, Analytics]
# published: false
---
> MEMO  
> 나는 [Jekyll-TeXt-Theme](https://tianqi.name/jekyll-TeXt-theme/)을 사용하고 있어서 해당 프로젝트를 바탕으로 작성함

# Google Analitics 등록

- 추적 ID : UA-158719188-1

- 범용 사이트 태그(gtag.js)
이 속성의 범용 사이트 태그(gtag.js) 추적 코드입니다. 이 코드를 복사하여 추적할 모든 웹페이지의 <HEAD>에 첫 번째 항목으로 붙여넣으세요. 이미 페이지에 범용 사이트 태그가 있다면 아래 스니펫의 config 행을 기존 범용 사이트 태그에 추가하기만 하면 됩니다.

```html
<!-- Global site tag (gtag.js) - Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=UA-158719188-1"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'UA-158719188-1');
</script>
```

# 블로그 설정 추가

- Google Analytics
In order to use Google Analytics, set `tracking_id` to your Google Analytics tracking code. You can also set `anonymize_ip` to `true` to anonymize IP tracking for analytic.

_config.yml
```yml
analytics:
  provider: google
  google:
    tracking_id: "your-google-analytics-tracking-code"
    anonymize_ip: true
```