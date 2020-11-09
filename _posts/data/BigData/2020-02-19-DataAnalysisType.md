---
date: 2020-02-19 08:35:00 +09:00
title: 빅데이터 - 데이터 분석 유형
category: BigData
tags: [bigdata, dataanalyst]
---
{% assign path = page.imgpath | append: page.id %}

- page : {{page.id}}

# 1. Descriptive analisys
> 기술적 데이터 분석
{:.comment}  

- 주어진 데이터를 요약/집계해서 결과를 도출
- 과거의 데이터를 단순 계산/집계해서 얻은 사실이므로 분석 결과를 따로 해석하지 않는다
- 이달의 매출액, 평균 세션 타임, 설문조사의 남녀비율 등
- 시각화 : 그래프(Pie chart, Box plot, Bar plot), 요약 형식의 테이블

# 2. Exploratory analysis(EDA)
> 탐색적 데이터 분석
{:.comment}  
  
> **REF** [EDA(Exploratory Data Analysis) 탐색적 데이터 분석](https://eda-ai-lab.tistory.com/13){:target='_blank'}

- 데이터를 분석하기 전에 그래프나 통계적인 방법으로 자료를 직관적으로 바라보는 과정
- 주요 목표 : 여러 변수 간 트렌드나 패턴, 관계를 찾는 것
- 그래프를 통한 사실 확인이 주된 작업 : 주로 Plot 
- 데이터 분석 초기에 가설 수립을 위해 주로 사용
  1. 분석의 목적
     - 분석의 목적이 가설 수립인지, 특정 변수들 간의 관계 파악인지, 트렌드 파악인지를 명확히 염두에 두고 분석을 진행한다
  2. Reproduciblity
     - 데이터가 많을 경우 여러 개의 plot을 그리다보면, 흥미로운 plot을 다시 그리게 될 때가 있다. 해당 plot을 다시 그릴 수 있기 위해서는 해당 조건을 기억해두어야 한다
- 시각화 : Scatter plot, Bobble chart 시계열 차트 등

# 3. Inferential analysis
- 표본 - 모집단 간의 관계 파악을 위한 분석
- 표본에서 얻은 결과가 모집단에도 적용 가능하지를 판단
- eg. 95%의 확률로 모집단의 평균 점수는 80~90점 사이라고 할 수 있다와 같은 결론 도출

# 4. Predictive analysis
- 머신 러닝(Machine learning), 의사결정나무(Decision Tree) 등 다양한 통계적 기법을 사용하여 미래 혹은 발생하지 않은 어떤 사건에 대한 예측을 하는 것
- cf. Prescriptive analysis : 철저하게 수학 예측 모델을 기반으로 어떤 의사 결정을 내려야할 지 처방하는 것이 주요 목적

# 5. Causal analysis
- 독립 변수와 종속 변수 간의 인과관계가 있는지 여부를 확인하기 위한 분석
- 실험을 통해 수집된 데이터를 대상으로 한다
  - 선형Regression이 가장 많이 사용되는 분석 방법
  - 변수가 여러개일 경우 Multi variable regression
  - 변수가 범주형일 경우 Logistics regression을 사용

# 6. Mechanistic analysis
- 독립 변수가 어떤 매커니즘으로 종속 변수에 영향을 미치는 지를 분석하는 것
- 어떠한 독립 변수가 어떠한 작용을 통해 독립 변수에 그러한 영향을 미치는 지를 이해하는 것
- 실험을 통해 수집된 데이터를 대상으로 한다

> **REF**  
> [데이터 분석의 유형 6가지 – 목적에 따라 달라지는 분석 방법
](http://www.dodomira.com/2016/01/12/%eb%8d%b0%ec%9d%b4%ed%84%b0-%eb%b6%84%ec%84%9d%ec%9d%98-%ec%9c%a0%ed%98%95/){:target='_blank'}
> [10 Different Kinds of Graphs for Your Data](https://blog.udemy.com/different-kinds-of-graphs/){:target='_blank'}