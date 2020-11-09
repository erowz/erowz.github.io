---
date: 2020-02-12 23:30:00 +09:00
title: 빅데이터 - 파이썬을 이용한 빅데이터 분석
category: iPython
tags: [bigdata, python]
---
# 분석 도구

- 프로그래밍 언어 파이썬([Python](https://www.python.org/))
- 파이썬의 데이터 분석 패키지 판다스([Pandas](https://pandas.pydata.org/))
- 파이썬의 머신러닝&인공지능 라이브러리인 싸이킷런([scikit-learn](https://willnfate.tistory.com/scikit-learn.org))

# 데이터 분석 과정

1. 데이터 로딩 : read\_csv
1. 시각화 및 가설 : [seaborn](https://seaborn.pydata.org/index.html), [matplotlib](https://matplotlib.org/)
2. 전처리(Preprocessing) : [DecisionTree](https://ko.wikipedia.org/wiki/%EA%B2%B0%EC%A0%95_%ED%8A%B8%EB%A6%AC_%ED%95%99%EC%8A%B5%EB%B2%95)를 사용하기 위해서 데이터를 숫자로 가공
3. 데이터 준비 : feature와 label을 사용해 X\_train, X\_test, y\_train 데이터 생성
4. 학습(Train) : DecisionTree를 사용해 데이터 학습(fit) 및 예측(predict)
5. 반영(Submission) : 제출용 데이터 호출해서 결과값 저장
6. 출력 : csv 파일로 저장 .to\_csv

> **REF**  
> [Seaborn을 사용한 데이터 분포 시각화](https://datascienceschool.net/view-notebook/4c2d5ff1caab4b21a708cc662137bc65/)

# 분석 알고리즘

> **REF**  
> [대표적인 데이터 분석 테크닉 30가지](http://www.dodomira.com/2016/08/19/frequently_used_analyitic_method/)

# 분석 성능 향상

1. 문제 정의 및 그에 맞는 [DecisionTree](https://ko.wikipedia.org/wiki/%EA%B2%B0%EC%A0%95_%ED%8A%B8%EB%A6%AC_%ED%95%99%EC%8A%B5%EB%B2%95) 선택
2. 알고리즘 정의 - Random Forest
3. 탐험적 데이터 분석 - 시각화 분석, 도메인 지식 기반 분석

## 탐험적 데이터 분석

> **REF**  
> 03-bike-sharing-demand.pdf

1. 알고리즘 업데이트 가능 여부
2. 데이터적으로 가공 가능 여부

### 데이터 분석

- 가설
  - 데이터를 보고 가설 수립
- 검증
  - 엑셀 : pivot table
  - python : decision tree
- 예측
  - 검증을 통해 가설이 맞다면 예측한 뒤 사용

### Model Validation
- 테스트를 하기 전에 검증을 하는 과정

#### Hold-out Validation
- train data를 8:2(fit:predict)로 나누어 분석
- 한번만 나누어 작업하므로 빠르지만 정확도가 떨어질 우려가 있다

#### Cross Validation
- 결과가 좋지 않은 경우 test set을 여러 개 생성해서 분석
- 1/n로 데이터를 나누어 하나씩 validation하여 n번 looping해서 정확도를 높여준다
- 실행 속도가 느리지만 정확도를 높힐 수 있다
- 각각의 데이터 결과를 모두 비교/분석하여 결과 도출

### Evaludation Metric for regression
- regression : 정답에 최대한 가깝게 예측하는 게 좋다
- 정확도를 측정하는 방법
- 정답(actural, a)과 예측값(predict, p)의 차이를 비교해서 이 수치가 0에 가까울 수록 좋은 결과
- 그외 : precesion, recall

1. Mean Absolute Error(MAE)
   - 절대값으로 계산
   - 에측값과 실제값의 평균적인 차이
   - \|$p-a$\|
2. Mean Squared Error(MSE)
  - 제곱을 하여 계산
  - 오차를 제곱하면 그 값이 차이가 커지므로 더 많이 틀릴 수록 패널티를 적용하는 개념이 됨
  - $(p-a)^2$
3. Root Mean Squared Error(RMSE)
   - 루트를 씌워서 현실값과 유사하게 계산
   - 현실값과 유사하게 맞춰 직관적으로 판단하기 용이
   - $\sqrt{({p - a})^2}$

### Online Evaluation
- 회사(또는 부서, 서비스)에서 일반적으로 사용하는 온라인 지표(online metric)과 가장 일치하는 오프라인 지표를 사용

### Root Mean Squared Logarithmic Error? (RMSLE)
- RMSE와 유사하게 계산을 하지만 사전에 log를 씌워서 계산
- 값이 커지는 부분을 완화시켜주기 위한 처리 : 값이 튀는 데이터가 많은 경우 사용

# 정확도 높이기

## 1. count 값 outlier
- distplot으로 `train['count']`를 보니 왼쪽으로 치우쳐진 꼬리가 긴 형태
```python
sns.displot(data=train['count'], hist=False)
```
- count 값에 log 적용
```python
y_train = np.log(train[label]+1)
...
prediction = np.exp(prediction)-1
```
- 결과값이 확연히 좋아짐

## 2. registerd / casual
- hour로 시각화해보면 둘의 양상이 다르다
- 각각 중요한 변수가 다를 것이다
- 둘을 각각 모델링해서 둘의 결과를 산출해서 더해서 count를 구해보자

1. y_train 분리
```python
y_train_reg = train['registered']
y_train_cas = train['casual']
```
1. model, fit(), predict()를 각각 따로 처리
2. 결과 합산
```python
predict = predict_reg + predict_cas
```

- count log 결과보다는 정확도가 떨어지지만 둘을 함께 적용하면 더 좋아질 거라 예상해봄

## 3. Hyper-parameter Tuning
- model의 다양한 파라미터 값을 설정해서 튜닝
- hyper-parameter : 사람이 직접 조정하는 파라미터
```python
RandomForestRegressor(bootstrap=True, criterion='mse', max_depth=None,
                      max_features='auto', max_leaf_nodes=None,
                      min_impurity_decrease=0.0, min_impurity_split=None,
                      min_samples_leaf=1, min_samples_split=2,
                      min_weight_fraction_leaf=0.0, n_estimators='warn',
                      n_jobs=-1, oob_score=False, random_state=37, verbose=0,
                      warm_start=False)
```

### RandomForestRegressor parameter

- n_estimators
  - decisionTree를 몇 개 쌓을 것인지 지정
  - 클 수록 좋지만 무작정 높인다고 결과가 좋아지는 것이 아님 (로그 그래프 형태로 성능 향상)
  - 10 또는 100(최신 버전)
- max_features
  - bagging(데이터셋을 여러개 구성하고 여러 개의 모델 사용)에서 각 트리 하나당 몇 개의 변수를 선택할 지 지정
  - eg. 30 (각 트리당 30개의 변수 지정), 0.1(비율로 지정)
  - 0.1 간격으로 0~1 사이의 값을 테스트해보자
- max_depth
  - 몇 번의 질문을 할 것인지 설정
  - 기본 설정으로 모델이 몇 개의 트리를 설정했는지 확인해서 그 값으로부터 시작해서 설정 조절
- min_samples_leaf
  - Decision Tree의 노드에서 더 질문을 할지 말지 여부를 결정
  - 질문을 진해할 최소 데이터 개수 지정. eg. 10으로 지정 시 10개의 데이터가 쌓이면 질문 중단

### 파라미터 설정 방법

#### 1) Grid Search
- [scikit-learn GridSearchCV](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html)
- 가장 좋은 설정값을 찾는 과정
- 테스트가 많아질 수록 시간이 많이 걸리는 단점

1. max_features와 max_depth의 적정값을 찾아서 설정
  - for문 돌려서 다양한 값 적용해서 cross_val_predict로 score 게산해서 확인
2. n_estimators 설정

#### 2) Random Search
- 넣어주는 파라미터를 랜덤하게 설정오는 방법

```python
max_depth = np.random.randint(50)

for .. :
  # 모델 생성
  # 점수 산출
```

#### 3) Coerse & Fine Search
- 랜덤 서치 2번 실행
  1. 대략의 범위로 1차 랜덤 서치 실행
  2. 1차 서치에서 산출한 값으로 범위를 좁혀서 2차 실행

# 빅데이터 분석 주요사항

1. 문제 분석 : 무엇을 맞추고 싶은 지 값을 먼저 결정
2. 알고리즘 선택
3. 데이터 준비 : 일반 데이터의 경우 8:2로 train/test 데이터 구성
4. 데이터 시각화 : 데이터 분포 파악
5. 데이터 전처리 : 빈값 채우기, 숫자로 변경
6. 성능 향상
7. 튜닝
8. 검증
9. 배포

모델 선택
- 기본부터 시작 : Decision Tree
- svm 알고리즘 : 분류에 좋대
