---
date: 2020-01-27 19:16
title: Python 기초 3 - 조건문과 반복문
category: Python
tags: python
---

# 조건문(Condition)

- 특정 조건에서만 실행시키고자 할 때 사용
- 조건 : Boolean으로 표현 (예외 있음)

## if 문

### if, elif, else

```python
if 조건:
  실행문
elif 조건:
  실행문
else:
  실행문
```

- 조건문 : if, elif, else 코드 마지막에 `:`(콜론, Colon)
  1. 기본적으로 boolean 사용
  2. 정수, 실수, 문자열 리스트 등 기본 타입도 조건에 사용 가능  
     - true : 값이 들어있는 값
     - false : 각 타입의 기본값 &rarr; eg. None, 0, 0.0, ''(빈 문자열), \[\](빈 리스트), ()(빈 튜플), {}(빈 딕셔너리), set()(빈 집합)  
- 실행문 (Block 또는 Code Block)
  : 들여쓰기(tab 또는 4칸 띄어쓰기)로 설정  
  : 들여쓰기는 항상 동일하게 유지해야 함
  
```python
>>> a = 7
>>> if a > 10:
...     print('a > 10')
... elif a > 5:
...     print('a > 5')
... else:
...     print('a <= 5')
... 
a > 5
```

### AND, OR, NOT
- 논리식 사용 가능
- 우선 순위 : NOT > AND > OR

```python
>>> a = 10
>>> b = 9
>>> c = 11

>>> if a == 10 and b != 9:
...     print('this is true')
this is true

>>> if a == 10 or b != ) and c == 7:
...     print('this is true')
this is true

>>> if (a == 10 or b != 9) and c == 7:
...     print('this is true')
# 결과가 false이므로 print 결과 없음
```

### 중첩 조건문(Nested conidition)
- 조건문의 중첩이 가능하며 들여쓰기로 depth(깊이) 설정
- 무제한 사용 가능

# 반복문(Loop)
- 반복적인 작업을 수행
- while문, for문 등

## while 문

```python
while 조건:
  실행문
```

### 기본 구조
- 조건을 만족하는 동안 반복 작업 수행
- while 뒤의 조건이 true인 경우, while 코드 블록을 반복 수행
- 반복을 중단시킬 설정 필수 &rarr; 없으면 무한루프에 빠짐

```python
>>> a = [1, 3, 6, 8, 33, 46]
>>> i = 0
>>> while i < len(a):
...     print(a[i])
...     i += 1
... 
1
3
6
8
33
46
```

### break
- 반복을 중단시킬 때 조건문과 함께 사용
- 웹 크롤링과 같이 데이터의 사이즈를 모르는 경우 용이

```python
>>> a = [1, 3, 6, 8, 33, 46]
>>> i = 0

>>> while i < len(a):
...     if a[i] > 20:
...         print(a[i])
...     i += 1
... 
33
46

>>> while i < len(a):
...     if a[i] > 20:
...         break
...     print(a[i])
...     i += 1
... 
1
3
6
8

>>> while true:
...     data = crowl()
...     if data == None:
...         break
...     print(data)
... 
```

### continue
- while문을 중단시키는 것이 아니라 while의 조건 지점으로 이동시키는 기능
- 특정한 조건에는 코드를 실행시키지 않고 건너뛰기 기능

```python
>>> a = 7
>>> while a > 0:
...     a -= 1
...     if a == 5:
...         continue
...     print(a)
... 
6
4
3
2
1
0
```

## for 문
- 리스트, 문자열, 튜플 등 컬렉션 타입의 순회 가능한 객체를 순회하면서 값을 처리할 때 사용
- 모든 아이템이 순회되면 for 블록 종료

### 문자열 순회

```python
>>> a = 'Hello World'
>>> for char in a:
...     print (a)
H
e
l
i
o

W
o
r
l
d
```

### 리스트 순회

```python
>>> a = [1, 2, 4, 3, 5]
>>> for i in a:
...     print (i, i * 2)
1 2
2 4
4 8
3 6
5 10
```

### dict 순회
- dictionary의 경우 기본적으로 순회 하게 되면 key값을 참조
- keys()함수를 이용하여 key 값만 순회 가능
- values()함수를 이용하여 value 값만 순회 가능
- items()함수를 이용하여 tuple형태로 key, value 순회 가능

```python
>>> a = {'korea':'seoul', 'japan':'tokyo', 'china':'beijing'}
>>> for key in a:
...     print(key, a[key])
korea seoul
japan tokyo
china beijing

>>> for value in a.values():
...     print(value)
seoul
tokyo
beijing

>>> print(list(a.items()))
[('korea', 'seoul'), ('japan', 'tokyo'), ('china', 'beijing')]

>>> for key, value in a.items():
...     print(key, value)
korea seoul
japan tokyo
china beijing
```

### index 사용 (enumerate)
- enumerate(객체) 함수 사용
```python
>>> a = [1, 2, 4, 3, 5]
>>> for idx, val in enumerate(a):
...     print (idx, val)
0 1
1 2
2 4
3 3
4 5
```

### break
- for문 실행을 중단 시킬 때 사용

### continue
- 해당 아이템을 건너뛰게 할 때 사용

### loop 중첩
- 반복문의 경우에도 중첩하여 사용 가능  
- 무제한 사용 가능

eg. 구구단 출력
```python
>>> a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> for i in a:
...     if i < 2:
...         continue
...     for j in a:
...         print(i, 'x', j, '=', i * j)
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
  ...
9 x 7 = 63
9 x 8 = 72
9 x 9 = 81
```