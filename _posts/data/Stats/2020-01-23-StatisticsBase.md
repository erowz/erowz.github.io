---
date: 2020-01-23 18:06:00 -0400
title: 통계학 - 통계학 개념 정리
category: Stats
tags: [bigdata, statistics, stats, 통계학, 기술통계, 추리통계]
description: 제대로 시작하는 기초 통계학 강의 노트
# mode: immersive
# header:
#   theme: dark
# article_header:
#   type: overlay
#   theme: dark
#   background_color: '#203028'
#   background_image:
#     gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
#     src: /assets/images/stats/base/cover.jpg
---
{% assign path = page.imgpath | append: page.id %}

# 통계학(Statistics)의 정의

- 수량적인 비교로 많은 사실을 관찰하고 처리하는 방법을 연구하는 학문
- 어떤 사건이나 현상을 효율적인 자료를 얻어 수치화하여 합리적인 해석을 하는 것

## 기술통계(Descriptive Statistics)
- 수집한 데이터를 요약 및 묘사해서 설명하는 통계 기법
- 기술통계 기법을 통해 수집한 데이터를 시각화해서 분석

1. 집중화 경향(Central tendency) : 평균(mean), 중앙값(median), 최빈값(mode)
2. 분산도(Variation) : 표준편차(standared deviation), 사분위(quartile)
   - 데이터가 어떻게 분포되어 있는 지를 설명 : 넓게 퍼질 수록 좋지 않은 상황이라고 판단

eg. 국민 소득 수준
- 1인당 평균 소득 2만 달러 : 대표값 \> 대표값이 높다고 무조건 좋은 상황이라고 판단 할 게 아니라 분산도 확인해야 한다
- 소득에 대한 편차도 높다면 \> 소득 분포가 넓게 퍼져있다 \>\> 소득의 분배가 잘 이루어지지 않고 있는 상황이다

## 추리통계(Inferential Statistics)
   - 수집한 데이터를 바탕으로 추론 예측하는 통계 기법
   - 제한된 데이터(표본)로 추론을 진행하므로 100% 맞는 것은 아님

eg. 선거 당선 예측
- 설문조사를 통해 데이터를 수집해서 그 결과로 모집단의 결과를 에측하는 것
- 결과의 정확도를 높이기 위해서는 빅데이터가 점점 더 중요해진다

![통계분류]({{path}}/img01.png){:width='560px'}  
*출처 : https://slidesplayer.org/slide/11152136/*

# 통계의 목적
- **의사결정** : 많은 정보 중 하나를 선택하기 위한 기준 제시
- **불확실성의 해소** : 더 많은 정보를 분석해서 더 나은 선택을 하기 위한 것
- **요약** : 데이터를 요약해서 의미 있는 정보로 가공
- **연관성 파악** : 요약된 정보 간의 연관성 파악해서 실제 결정에 사용
- **예측** : 정보의 패턴을 찾아내 다양한 방법을 통해 미래를 예측

# 통계분석의 과정

```mermaid
graph LR;
    A[수집]
    B[정제]
    C[추정]
    D[검정]
    A-->B;
    B-->C;
    C-->D;
```

> **REF**  
> [제대로 시작하는 기초 통계학 | 노경섭 지음](https://www.youtube.com/playlist?list=PLsri7w6p16vs-rMb1uXHfh3FiCk2WjEUG){:target='_blank'}  
> [기술통계와 추리통계란 무엇인가 | 필로홍의 데이터노트](https://drhongdatanote.tistory.com/25){:target='_blank'}