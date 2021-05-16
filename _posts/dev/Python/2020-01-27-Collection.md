---
date: 2020-01-27 18:38
title: Python 기초 2 - Collection
category: Python
# permalink: /python/collection
subject: python
tags: python collection list tuple dictionary set
---

# Collection
\- 복수 개의 값을 담을 수 있는 데이터 구조

- list : mutable (생성 후 변경 가능)
- tuple : immutable (생성 후 변경 불가능)

## 컬렉션 내장 함수
 - abs, len, type, range 등

### len()
- 리스트의 길이 반환

### range()
- 리스트나 튜플을 쉽게 만들 수 있게 해주는 내장함수
- 파라미터에 따라 다양한 결과 반환
  - range(a) : 0부터 a-1 사이의 숫자 반환
  - range(a, b) : a부터 b-1 사이의 숫자 반환
  - range(a, b, c) : a부터 b-1 사이의 숫자를 c씩 건너뛰며 반환

```python
>>> print(range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

>>> print(range(2, 10))
[2, 3, 4, 5, 6, 7, 8, 9]

>>> print(range(2, 10, 3))
[2, 5, 8]
```

# 리스트(List)

## 리스트 초기화
- \[\] 안에 값을 담아서 생성
- list() 함수로 생성
- string.split() 함수로 생성

### list()
- 다른 데이터 타입을 리스트로 변환할 때도 사용
- string > list, tuple > list
- list(value) 형식으로 사용

```python
# string to list
>>> a = 'Hello World'
>>> b = list(a)
>>> print(b)
['H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd']

# tuple to list
>>> a = (1, 2, 3)
>>> b = list(a)
>>> print(b)
[1, 2, 3]
```

### split()
- 구분자로 구분한 후 리스트로 반환
- 구분자(delimiter)  
    : optional  
    : 미지정 시 기본값인 빈칸 띄어쓰기 적용

```python
>>> a = 'Hello world, nice to meet you'
>>> print(a.split())
['Hello', 'world,', 'nice', 'to', 'meet', 'you']
>>> print(a.split(','))
['Hello world', ' nice to meet you']
```

## 리스트 인덱스
- 문자열의 인덱싱과 동일하게 동작

### 리스트 인덱싱(list indexing)
- \[\] 연산자를 이용하여 항목 얻어오기
    - \[i\] : i 번째 원소를 반환
    - \[-i\] : 마지막 원소가 -1, 앞으로 갈 때마다 1씩 감소

```python
>>> a = [1, 2, 3, 4, 5]
>>> a[2]
3
>>> a[4]
5
>>> a[-1]
5
```

### 리스트 개별 아이템 변경
- 인덱스로 접근하여 값 업데이트 가능
- string, tuple과 같은 immutable 타입은 적용 불가

```python
>>> a = [1, 2, 3, 4, 5]
>>> a[0] = 100
>>> a[-1] = 90
>>> print(a)
[100, 2, 3, 4, 90]
```

### 리스트 슬라이싱(list slicing)
- 문자열 슬라이싱과 동일하게 동작
- 슬라이싱의 결과 역시 list
- \[start : end : increment\]
    - start : 시작 인덱스
    - end : 끝 인덱스, 해당 인덱스의 원소는 제외
    - increment : 증가 단위. 기본값은 1

```python
>>> a = [1, 2, 3, 4, 5, 6, 7]
>>> a[1:4]
[2, 3, 4]
>>> a[3:]
[4, 5, 6, 7]
>>> a[:6]
[1, 2, 3, 4, 5, 6]
>>> a[1:6:1]
[2, 3, 4, 5, 6]
>>> a[1:6:2]
[2, 4, 6]
```

## 리스트 멤버 함수
- 생성된 리스트 객체에 동작하는 함수

### extend()
- 리스트 연장
- += 으로도 가능

```python
>>> a = [1, 2, 3, 4, 5]
>>> b = [6, 7, 8, 9, 10]
>>> a.extend(b)
>>> print(a)
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

>>> a = [1, 2, 3, 4, 5]
>>> b = [6, 7, 8, 9, 10]
>>> a += b
>>> print(a)
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### append()
- 리스트의 끝에 항목 추가

```python
>>> a = [1, 2, 3, 4, 5]
>>> a.append(10)
>>> print(a)
[1, 2, 3, 4, 5, 10]
```

### insert()
- 리스트의 원하는 위치에 항목 추가
- list.insert(index, object) : 앞에 인덱스, 뒤에 아이템을 명시

```python
>>> a = [1, 2, 3, 4, 5]
>>> a.insert(1, 40)
>>> print(a)
[1, 40, 2, 3, 4, 5]
```

### remove()
- 지정한 값의 첫 번째 항목 삭제
- 리스트에 해당 값이 없을 경우 오류 발생

```python
>>> a = [1, 2, 3, 4, 5, 3]
>>> a.remove(3)
>>> print(a)
[1, 2, 4, 5, 3]
```

### pop()
- 인덱스로 삭제. 인덱스 미지정 시 마지막 항목 삭제
- 삭제하는 값을 반환 후 삭제 처리

```python
>>> a = [1, 2, 3, 4, 5]
>>> a.pop()
5
>>> print(a)
[1, 2, 3, 4]

>>> a = [1, 2, 3, 4, 5]
>>> b = a.pop(2)
>>> print(b, a)
3 [1, 2, 4, 5]
```

### index()
- 찾고자 하는 값의 인덱스 반환
- 찾는 값이 없을 경우 오류 발생

```python
>>> a = [1, 2, 3, 4, 5]
>>> a.index(3)
2
```

### in 키워드
- 리스트 내에 해당 값의 존재 여부 반환(True/False)
- value in \[list\] 형식으로 사용

```python
>>> a = [1, 2, 3, 4, 5]
>>> print(3 in a)
True
>>> print(10 in a)
False
```

## 리스트 정렬

### sort()
- 리스트 자체를 내부적으로 정렬
- parameter
  - reverse : 정렬 순저 지정. 기본값 False
  - key : 별도로 원하는 정렬 방식 지정. Lambda 함수 용이

```python
>>> a = [5, 2, 9, 6, 8, 11, 56]
>>> a.sort()
>>> print(a)
[2, 5, 6, 8, 9, 11, 56]
>>> a.sort(reverse=True)
>>> print(a)
[56, 11, 9, 8, 6, 5, 2]
```

### sorted()
- 리스트의 정렬된 복사본을 반환

```python
>>> a = [5, 2, 9, 6, 8, 11, 56]
>>> b = sorted(a)
>>> print(a)
[5, 2, 9, 6, 8, 11, 56]
>>> print(b)
[2, 5, 6, 8, 9, 11, 56]
```

```python
>>> a = [1, 2, 3, 4]
>>> print(len(a))
4
```

# 튜플(Tuple)
- 리스트처럼 복수 개의 값을 갖는 컬렉션 타입
- 생성된 후 변경 불가능

```python
>>> a = (1, 2, 3)
>>> print(a)
(1, 2, 3)

>>> a = 100, 200
>>> print(a)
(100, 200)
```

### tuple unpacking

- 튜플의 값을 차례대로 변수에 대입 가능 : 다수의 변수를 하나의 라인에 초기화 가능

```python
>>> a, b, c, d = 100, 200, 300, 400
>>> print(a, b, c, d)
100 200 300 400

# a, b의 값 교환
>>> a = 5
>>> b = 4
>>> a, b = b, a  # 튜플 사용으로 값 변환
>>> print(a, b)
4 5
```

# Dictionary

- 키 & 값을 갖는 데이터 구조  
    : { key : value, ...} 구조
- 키 : 내부적으로 hash 값으로 저장 >> 키 중복 불가
- 순서 없음(Unordered) > 인덱스가 없음

```python
>>> a = {'Korea':'Seoul', 'Canada':'Ottawa', 'USA':'Washinton D.C'}
>>> print(type(a))
<class 'dict'>
>>> print(a)
{'Korea': 'Seoul', 'Canada': 'Ottawa', 'USA': 'Washinton D.C'}
>>> print(a['Korea'])
Seoul
>>> b = {0:1, 3:7, 4:10, 8:2}
>>> print(type(b))
<class 'dict'>
>>> print(b)
{0: 1, 3: 7, 4: 10, 8: 2}
>>> print(b[0])
1
>>> print(b[2])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 2
```

## 값 접근 (value access)

- dict\[key\] : key가 없는 경우 오류 발생
- dict.get(key) : key가 없는 경우 None 반환

```python
>>> a = {'a':1, 'b':4, 'c':8}
>>> a['a']
1
>>> a['d']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'd'

>>> print(a.get('d'))
None

>>> if 'd' in a:
...     print(a['d'])

```

## keys, values 접근

- keys() : 키만 반환
- values() : 값만 반환
- items() : 키 & 값 튜플 반환

```python
>>> a = {'a':1, 'b':4, 'c':8}

>>> print(a.keys())
dict_keys(['a', 'b', 'c'])
>>> print(list(a.keys()))
['a', 'b', 'c']

>>> print(a.values())
dict_values([1, 4, 8])
>>> print(list(a.values()))
[1, 4, 8]

>>> print(a.items())
dict_items([('a', 1), ('b', 4), ('c', 8)])
>>> print(list(a.items()))
[('a', 1), ('b', 4), ('c', 8)]
```

## 항목 추가 및 변경

- 기존 키 존재 : 값 업데이트
- 신규 키 : 새로운 키 & 값 생성

```python
>>> a = {'Korea':'Seoul', 'Canada':'Ottawa', 'USA':'Washinton D.C'}
# 신규 생성
>>> a['Japan'] = 'Tokyo'
>>> print(a)
{'Korea': 'Seoul', 'Canada': 'Ottawa', 'USA': 'Washinton D.C', 'Japan': 'Tokyo'}

# 업데이트
>>> a['Japan'] = 'Kyoto'
>>> print(a)
{'Korea': 'Seoul', 'Canada': 'Ottawa', 'USA': 'Washinton D.C', 'Japan': 'Kyoto'}
```

## update()

- 두 딕셔너리를 병합
- dict.update(parameter) 형식으로 사용
- 동일 키가 있을 경우 parameter dict의 값으로 overwrite

```python
>>> a = {'a':1, 'b':4, 'c':8}
>>> b = {'a':10, 'd':2, 'e':9}
>>> a.update(b)
>>> print(a)
{'a': 10, 'b': 4, 'c': 8, 'd': 2, 'e': 9}  ## b dict의 a key의 값으로 overwrite됨
```

## key 삭제

### pop 함수 이용

- pop(키) 형식으로 삭제
- 해당 키의 값 반환 후 삭제

### del 키워드 사용

- del 변수명 : 변수 자체를 삭제
- del 변수명\[키\] : 해당 키 & 값 삭제

```python
>>> a = {'a':1, 'b':4, 'c':8}
>>> print(a)
{'a': 1, 'b': 4, 'c': 8}
>>> a.pop('a')
1
>>> print(a)
{'b': 4, 'c': 8}
>>> del a['b']
>>> print(a)
{'c': 8}
```

### clear()

- 해당 dict를 초기화할 때 사용
- dict.clear() 형식

```python
>>> a = {'a':1, 'b':4, 'c':8}
>>> print(a)
{'a': 1, 'b': 4, 'c': 8}
>>> a.clear()
>>> print(a)
{}
```

## in 키워드

- 딕셔너리 내에 해당 키의 존재여부 확인
- O(1) 연산
    - 딕셔너리의 크기와 무관하게 항상 연산 속도가 일정함을 의미
    - 리스트의 경우 in 키워드 사용 시 리스트의 전체 값을 서칭하므로 사이즈에 따라 연산 속도 좌우됨

```python
>>> a = {'a':1, 'b':4, 'c':8}
>>> 'b' in a
True
>>> 1 in a  # 1 이라는 키가 a에 없으므로 False 반환
False
>>> b = [0, 1, 3, 4, 6, 7, 9]
>>> 2 in b
False
```

# Set (집합 자료형)

- Dictionary에서 key만 활용하는 데이터 개념  
    : {value, ....} 구조
- 수학의 집합과 동일한 개념
    - 중복 불가 > index가 없음
    - 순서 없음(Unordered)

```python
>>> a = {1, 1, 3, 4, 5, 5, 6, 7, 7, 8}
>>> print(type(a))
<class 'set'>
>>> print(a)  # 중복 값이 제거된 set으로 생성됨
{1, 3, 4, 5, 6, 7, 8}
```

## set()

- set 함수 초기화 : {}로 생성 시 Dictionary로 생성됨
- 집합으로 변환 : set(object) 형식으로 변환

```python
# 집합 초기화
>>> a = {}
>>> print(type(a))
<class 'dict'>

>>> a = set()
>>> print(type(a))
<class 'set'>

# 집합으로 변환
>>> a = [1, 1, 3, 4, 5, 5, 6, 7, 7, 8]
>>> b = set(a)
>>> print(a)
[1, 1, 3, 4, 5, 5, 6, 7, 7, 8]
>>> print(b)
{1, 3, 4, 5, 6, 7, 8}
```

$$\bar{x} = \frac{1}{n}\ \times\sum_{i=1}^n x^i \ $$

## set operations

- 수학의 연산과 동일
- 합집합, 교집합, 차집합 등 지원
    - a.union(b) : 합집합
    - a.intersection(b) : 교집합
    - a.difference(b) : 차집합
    - a.issubset(b) : 부분집합 여부

```python
>>> a = {1, 2}
>>> b = {2, 3, 4}
>>> c = {2, 4}
>>> print(a.union(b))  # 합집합
{1, 2, 3, 4}
>>> print(a.intersection(b))  # 교집합
{2}
>>> print(a.difference(b))  # 차집합
{1}

# 부분집합 여부
>>> print(a.issubset(b))
False
>>> print(c.issubset(b))
True
```