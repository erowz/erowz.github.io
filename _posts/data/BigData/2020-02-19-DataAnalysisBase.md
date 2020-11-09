---
date: 2020-02-19 05:54:00 +09:00
title: 빅데이터 - 데이터 분석
category: BigData
tags: [bigdata, dataanalyst]
---
{% assign path = page.imgpath | append: page.id %}

# 데이터 분석가
> **REF** [데이터 분석가(Data scientist)에게 꼭 필요한 4가지 역량](http://www.dodomira.com/2016/02/26/%eb%8d%b0%ec%9d%b4%ed%84%b0-%eb%b6%84%ec%84%9d%ea%b0%80%ec%97%90%ea%b2%8c-%ed%95%84%ec%9a%94%ed%95%9c-4%ea%b0%80%ec%a7%80/){:target='_blank'} (2016.02.26)

- 데이터 싸이언티스트, 데이터 애널리스트, 데이터 엔지니어, 비즈니스 애널리스트 등 다양한 직군 &rarr; 여기에서는 데이터 분석하는 사람을 '데이터 분석가'로 통칭

## 필요한 역량

### 데이터에 대한 이해
- 데이터베이스에서 데이터 추출 능력 : RDBMS(SQL), MongoDB(JSON) 등

### 통계 및 분석 방법에 대한 이해
- 데이터 분석을 하기 위해서는 통계적 지식이 필수
- 다양한 분석 기법 습득 : [온라인 강의 참고](https://www.analyticsvidhya.com/blog/2015/08/data-science-bootcamps-machine-learning-certifications/){:target='_blank'}
- 지도학습, 비지도학습 영역 별로 사실 자주 사용되는 기본 분석 방법론
- 최신 분석 방법 습득 : Kaggle 또는 유명 데이터 분석가 블로그 팔로잉 등 다양한 방법으로 시도할 것

### 분석 Tool에 대한 이해
- 분석 툴 종류
  - 오픈소스 : R, Python [R vs Python 참고](https://medium.com/@InDataLabs/r-vs-python-729ceaa15620#.r2lkjj362){:target='_blank'}
  - 유료 : SAS, SPSS

### 비즈니스 커뮤니케이션
- 문제 정의 능력
  - 데이터 분석 전 달성 목적 및 비즈니스 임팩트 사전 정의가 중요
  - 기본적인 [Problem Solving](https://en.wikipedia.org/wiki/Problem_solving){:target='_blank'} 방법론과 데이터 분석의 기본인 [문제 유형](http://www.dodomira.com/2016/01/12/%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B6%84%EC%84%9D%EC%9D%98-%EC%9C%A0%ED%98%95/){:target='_blank'}을 습득하고 있어야 무엇을 해결해야하는 지에 대한 협의가 가능
- 결과 전달 능력 (STORYTELLING AND VISUALIZATION)
  - 데이터 분석의 결과를 필요한 사람/부서에서 잘 이해할 수 있도록 전달하는 것 또한 필수적인 스킬 중 하나

# 데이터 분석 단계
> **REF** [빅데이터 분석의 세 단계](https://post.naver.com/viewer/postView.nhn?volumeNo=16213726&memberNo=2367855){:target='_blank'}  

## 1. 빅데이터 사전 처리 및 특징변수 식별

1. 분석 목적에 맞는 가설 수립 및 데이터 확보
2. 기초적인 데이터베이스 클렌징 및 분석에 필요한 크기의 데이터 수집
3. 데이터 시각화 기법으로 분석하고 새로운 특징변수를 추출한 후 학습을 위한 충분한 케이스 데이터 수집

## 2. 알고리즘 선정 및 학습

1. 특징변수를 최종 확정하고 분석 목적에 맞는 머신러닝 알고리즘을 선정
2. 알고리즘의 매개변수를 조정하거나 보완
3. 빅데이터 분석 데이터 세트를 활용하여 알고리즘 학습
4. 향후 추가 데이터의 오류 발생 최소화를 위해 학습된 알고리즘의 노이즈 등에 대한 민감도 테스트

## 3. 학습된 알고리즘에서 업무 규칙 추출

- 분석 담당자나 업무 담당자가 이해할 수 있도록 전문가 시스템에서 주로 많이 사용하는 IF-THEN 형태로 알고리즘의 학습 결과를 변환시켜주는 단계
- 머신러닝 알고리즘으로부터 업무 규칙을 추출하는 것이 주된 목적

[^1]: [데이터 분석가(Data scientist)에게 꼭 필요한 4가지 역량](http://www.dodomira.com/2016/02/26/)