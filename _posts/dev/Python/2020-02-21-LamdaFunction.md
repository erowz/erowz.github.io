---
date: 2020-02-20 21:00 +09:00
title: Python 기초 5 - Lambda 함수
category: Python
tags: [python, function, lambda]
---
# Lambda 함수
- 단일문으로 표현되는 익명함수 : 이름이 없는 구현체만 존재하는 간단한 함수를 의미
- 코드 상에서 한번만 사용되는 기능이 있을 때 굳이 함수로 만들지 않고 1회성으로 만들어서 쓸 때 사용
- 형식 : `lambda 입력값:출력값`

### 기본 구조

```python
# lambda 함수
square = lambda x:x**2

print(type(square))
print(square(5))
>> <class 'function'>
>> 25
```
  
### 기본 함수와 비교

```python
# 기본 함수
def square(x):
    return x**2

print(type(square))
print(square(5))
>> <class 'function'>
>> 25
```
  
```python
def add(x, y):
    return x + y

add2 = lambda x,y:x+y
print(add2(20, 30))
>> 50
```

### sort() 예제

```python
strs = ['bob', 'ashley', 'charles', 'alexander']

# 기본 알파벳 순서 정렬
strs.sort()
print(strs)
>> ['alexander', 'ashley', 'bob', 'charles']

# 글자수 순서 정렬
strs.sort(key=order_len)
print(strs)
>> ['bob', 'ashley', 'charles', 'alexander']

# lambda 함수 사용 글자수 정렬
strs.sort(key=lambda s:len(s))
print(strs)
>> ['bob', 'ashley', 'charles', 'alexander']
```

# lambda 사용 대표 함수  
: filter, map, reduce  
- lambda가 유용하게 쓰이는 3가지 대표 함수
- 함수형 프로그래밍의 기본 요소

### filter
```
filter(함수, 리스트)
```
- 리스트 필터링 함수
- 특정 조건을 만족하는 요소만 남기고 필터링
- 리스트의 각 원소에 함수를 적용해서 결과값이 True면 남기고, False면 제거

```python
# 짝수만 남기는 필터링
nums = list(range(1, 21))
list(filter(lambda n:n%2==0, nums))
>> [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

### map
```
filter(함수, 리스트)
```
- mapping 시켜서 다른 리스트를 생성
- 각 원소를 주어진 수식에 따라 변형하여 새로운 리스트를 반환
- 리스트의 개수는 변하지 않음

```python
# 기존 리스트 값의 제곱값으로 이루어진 새로운 리스트 생성
nums = list(range(1, 10))
list(map(lambda n:n**2, nums))
```

### reduce
```python
import functools
functools.reduce(함수, 리스트)
```
- python v3부터 기본 함수에서 제외됨 &rarr: import 필수
- 차례대로 앞 2개의 원소를 가지고 연산. 연산의 결과가 또 다음 연산의 입력으로 진행됨. 따라서 마지막까지 진행되면 최종 출력은 한개의 값만 남게 됨

<table>
<tr><td>1</td><td>2</td><td>3</td><td>4</td></tr>
<tr><td colspan='2'>3</td><td>3</td><td>4</td></tr>
<tr><td colspan='3'>6</td><td>4</td></tr>
<tr><td colspan='4'>10</td></tr>
</table>*앞 두개씩 더하는 로직의 경우*

```python
# 리스트 내의 숫자의 합
nums =[1, 2, 3, 4]
functools.reduce(lambda a,b:a+b, nums)
>> 10
```