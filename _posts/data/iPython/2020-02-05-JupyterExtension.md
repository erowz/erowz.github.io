---
date: 2020-02-05 19:12 +09:00
title: Jupyter Notebook Extensions
category: iPython
key: JupyterExtension
tags: [python, jupyternotebook, extensions]
---
{% assign path = page.imgpath | append: page.id %}

# 쥬피터 노트북 확장 프로그램 설치

### 설치

```
$pip install jupyter_contrib_nbextensions      # 라이브러리 설치
$jupyter contrib nbextension install --user    # 쥬피터노트북에 등록
```

### 설정

1.  extension 설정 접속  
    [http://localhost:8888/nbextensions](http://localhost:8888/nbextensions){:target="_blank"}
    
2.  기능 추가
    -   체크 박스 해제 : disable configuration for nbextensions without explicit compatibility
    -   원하는 기능 체크 박스 설정해서 추가  
        ![extensions]({{path}}/img01.png)

# 확장 프로그램 추가 및 사용

### Table of Contents
: 쥬피터 노트북 목차 생성  
![extensions]({{path}}/img02.png){:style='width:600px'}
![extensions]({{path}}/img03.png){:style='width:600px'}

### Collapsible Headings
: 구간 폴딩  
![extensions]({{path}}/img04.png){:style='width:600px'}
![extensions]({{path}}/img05.png){:style='width:600px'}

> **REF**  
> [쥬피터노트북 확장 프로그램 설치하기(nbextension)\|작성자 데이터공방](http://blog.naver.com/PostView.nhn?blogId=kiddwannabe&logNo=221583729175){:target="_blank"}  
> [Jupyter notebook에 nbextension 설치/사용 방법](https://skysign.tistory.com/33){:target="_blank"}