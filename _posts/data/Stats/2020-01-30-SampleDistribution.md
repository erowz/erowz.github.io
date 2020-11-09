---
date: 2020-01-30 04:36:00 +09:00
title: 통계학 - 표본의 분포
category: Stats
tags: [bigdata, statistics, stats, 통계학, 표준화, 표본평균, 표본분산, 표본비율]
description: 제대로 시작하는 기초 통계학 강의 노트
---
{% assign path = page.imgpath | append: page.id %}

표본을 분석하기 위해서 가장 쉽게 파악할 수 있는 표본평균, 표본분산, 표본비율을 알아야 한다.

#### [eg](#){:.button.button--outline-success.button--pill.button--sm} 성적 비교
- A - 영어 : 80점 / 평균 90점
- B - 수학 : 60점 / 평균 50점

-> 실제 점수가 낮더라도 **평균보다 높은 점수를 받은 B가 공부를 더 잘했다**고 할 수 있다

#### [eg](#){:.button.button--outline-success.button--pill.button--sm} 점수가 60점 미만이면 과락으로 진급 누락일 때

|구분|A반|B반|
|:---:|:---:|:---:|
|반 평균|70|70|
|점수 분포|65~75|0~100|

-> 진급 기준으로 보면 **과락 없이 모두 통과한 A반이 더 잘했다**고 볼 수 있다

# 표준화

## 정규분포(Normal distribution)
- 표본분포 중 가장 단순하고 많이 나타나는 형태
- 어떤 사건이 일어난 빈도(frequency)를 계산해서 그래프로 봤을 때 중심(평균, $\mu$)을 기준으로 좌우 대칭되는 분포 형태
- 1,2회 정도의 빈도가 낮은 사건을 횟수($n$)를 반복해서 $n \rightarrow \infty$하면 정규분포 그래프의 사건이 발생

![정규분포]({{path}}/img01.jpeg){:width='400px'}   
*정규분포 그래프 | 출처 : https://images.app.goo.gl/PRp4MYsRNZQ62Ebp6*

## 표준화(Standardization)
> **REF** [정규분포 표준화 하는 법](https://math100.tistory.com/38){:target='_blank'}

- 단순한 현상은 정규분포만으로 충분하지만 실제 연구에서는 복잡한 관계에 대한 분석 결과가 필요
- 여러 특성에 대한 분석 결과를 기준점을 동일하게 맞춰 서로 비교하기 쉽게 만드는 과정

![표준화]({{path}}/img02.jpeg){:width='600px'}   
*출처 : https://brainstudy.tistory.com/4*

# 표본의 분포

<table class='mk-table'>
    <tr><th>구분</th><th>특징</th><th>이름</th><th>설명</th></tr>
    <tr><td rowspan='2'>표본평균의 확률분포</td><td rowspan='2'>평균과 관련된 분포</td><td>$z$분포</td><td class='text--left'>표본 개수가 충분한 경우 사용</td></tr>
    <tr><td>$t$분포</td><td class='text--left'>표본 개수가 충분하지 못한 경우 사용</td></tr>
    <tr><td rowspan='2'>표본분산의 확률분포</td><td rowspan='2'>분산의 추론과 관련된 분포</td><td>$x^2$분포</td><td class='text--left'>한 개의 분산(표본)을 추론한 분포<br/>직접적으로 조사 대상 설명 가능</td></tr>
    <tr><td>$F$분포</td><td class='text--left'>두 개의 분산(표본)을 추론하는 분포<br/>직접 이용하기보다는 추론된 분산을 이용</td></tr>
    <tr><td>표본비율의 확률분포</td><td>비율과 관련된 분포</td><td>$\hat{p}$분포</td><td class='text--left'>모비율을 추정하기 위해 사용</td></tr>
</table>*표본 확률분포의 종류*

## 표본평균의 확률분포

### $z$분포
> 표준정규분포, Standard normal dsitribution
{:.comment}  

- 표본의 개수가 충분(30개 이상)할 때 표준화 과정을 거친 정규분포
- 평균 = 0, 분산 = 1

$$
z=\frac{X-\mu}{\sigma / \sqrt{n}}
$$

($X$: 측정치, $\mu$: 평균, $\sigma / \sqrt{n}$: 표준오차)

### $t$분포
> 스튜던트 $t$분포, Student’s t-distribution
{:.comment}  

- 모집단이 정규분포이고, 표본이 충분치 않은 경우 표본이 충분치 않아 정규분포를 이루지 못할 가능성이 크기 때문에 정규분포 대신 사용
- 평균 = 1, 분산 > 1

$$
t_{n-1}=\frac{X-\mu}{s/ \sqrt{n}}
$$

($X$: 측정치, $\mu$: 평균, $s/ \sqrt{n}$: 표준오차, $n-1$: 자유도)

### $z$분포와 $t$분포의 관계

$z=\frac{X-\mu}{\sigma / \sqrt{n}} \quad$ vs $\quad t_{n-1}=\frac{X-\mu}{s/ \sqrt{n}}$  
- 두 식을 비교해보면 $n$과 $n-1$을 제외하고 동일한 식
- $n \rightarrow \infty$면 $t$분포가 $z$분포로 수렴해 결국 동일한 분포가 된다

![]({{path}}/img03.png){:width='400px'}   
*$z$분포와 $t$분포의 비교 | 출처 : 제대로 시작하는 기초 통계학(p.42)*

## 표본분산과 확률분포

### $x^2$분포
> 카이제곱분포, chi-squared distribution
{:.comment}  

- 신뢰구간이나 가설검정 등의 모델에서 자주 등장
- 모분산의 추정이나 계수 값을 해석하는데 사용
- 정규분포로부터 도출 -> $z$분포(표준정규분포)의 제곱에 대한 분포 --> 항상 양수
- 확률변수 $x_1, x_2, x_3, \cdots, x_n$ : 표준정규분포이면서 독립이라면
  - $x_1^2, x_2^2, x_3^2, \cdots, x_n^2$ : 새로운 확률변수를 구성 -> 자유도가 $n$인 $x^2$분포
  - $x^2$분포 = 확률변수 $\sum_{i=1}^{n}x_i^2$의 분포  

![]({{path}}/img04.png){:width='400px'}   
*$x^2$분포의 특성 | 출처 : 제대로 시작하는 기초 통계학(p.43)*

### $F$분포
> F-distribution 또는 Snedecor's F distribution 또는 Fisher–Snedecor distribution
{:.comment}  

- 두 카이제곱분포를 각각의 자유도로 나눈 후 다시 서로 나눈 값
- 분산의 동일성 여부를 판단하는 수단으로 사용
- 두 개의 분산에 관한 추론 : $F_{(v_1, v_2)}$ ($v_1, v_2$ : $X^2$에 대한 분산)*
  - $x_1, x_2, x_3, \cdots, x_n$과 $y_1, y_2, y_3, \cdots, y_n$이 서로 독립
  - 각각 n, m의 자유도를 가지는 $X^2$분포
  - -> $\frac{v_x}{v_y}$ : $F$분포를 따르게 됨
- 분산이 같은 모집단에서 $x_n, y_n$만큼 표본 추출
  - 각각의 분산  

    $$
    v_1 = \frac{s_1}{(n-1)}, v_2 = \frac{s_2}{(m-1)}
    $$

  - 각 비율  
  
    $$
    F = \frac{v_1}{v_2}
    $$

    : 자유도 $(n-1), (m-1)$인 $F$분포

![]({{path}}/img05.png){:width='400px'}   
*$F$분포의 특성 | 출처 : 제대로 시작하는 기초 통계학(p.44)*

- $F$분포의 특성
  - $v_1 = v_2$(등분산) -> 1을 기준으로 값이 결정 ($F_{(50,50)}$ 그래프 참고)
  - $v_1 \neq v_2$ -> 1에서 멀어짐
  - 표본의 개수가 많을수록 1과 가까운 분포

## 표본비율의 확률분포
- 경우에 따라 비율이 평균보다 많이 사용
- eg. 점수가 700점 이상일 확률, 시험 1회 응시의 합격률 등과 같이 표본비율이 사용됨

### $\hat{p}$분포

- 모비율 추정을 위해 사용
- Yes/No 형태의 어느 한 사건이 발생하는 베르누이 시행의 이항분포를 활용하여 표본비율의 분포를 구할 수 있다

> **REF**  
> [제대로 시작하는 기초 통계학 | 노경섭 지음](https://www.youtube.com/playlist?list=PLsri7w6p16vs-rMb1uXHfh3FiCk2WjEUG){:target='_blank'}  
> [통계시각화 matplotlib](https://cometouniverse.tistory.com/69){:target='_blank'} : Python으로 시각화를 해보자!