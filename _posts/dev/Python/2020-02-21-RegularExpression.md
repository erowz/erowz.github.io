---
date: 2020-02-22 17:34 +09:00
title: Python 기초 8 - 정규 표현식
category: Python
tags: [python, regularExpression]
---

# 정규표현식
> regular expression, re
{:.comment}

- 특정한 패턴과 일치하는 문자열를 '검색', '치환', '제거' 하는 기능을 지원
- 정규표현식의 도움없이 패턴을 찾는 작업(Rule 기반)은 불완전 하거나 작업의 cost가 높음
- crawling에서도 많이 사용
- eg. 이메일 형식 판별, 전화번호 형식 판별, 숫자로만 이루어진 문자열 등

### raw string
- 문자열 앞에 r이 붙으면 해당 문자열이 구성된 그대로 문자열로 변환
- 정규표현식 사용 시 raw string을 이용

```python
print('abcdef\n')  # escape 문자열
print(r'abcdef\n')
>> ----------------
abcdef

abcdef\n
```

## search 함수
`re.search(r'pattern', string, flag[optional])`
- `re` 패키지 임포트해서 `search` 함수 사용
- 첫 번째로 패턴을 찾으면 match 객체를 반환
  - match.start() : 시작 인덱스
  - match.end() : 종료 인덱스
  - match.group() : 그룹 정보
  
```python
m = re.search(r'abc', 'abcdef')

print(m)
print(type(m))
print(m.start())
print(m.end())
print(m.group())
>> ----------------
<re.Match object; span=(0, 3), match='abc'>
<class 're.Match'>
0
3
abc
```

- 패턴을 찾지 못하면 None 반환

```python
m = re.search(r'abc', 'abdef')

print(m)
print(type(m))
>> ----------------
None
<class 'NoneType'>
```

- 검색 예제

```python
# 3자리 숫자 검색
re.search(r'\d\d\d', '123abcd456')
>> <re.Match object; span=(0, 3), match='123'>

# 4자리 숫자 검색
re.search(r'\d\d\d\d', '123abcd456')
>> 

# 3자리 숫자와 다음 1자리 문자 검색
re.search(r'\d\d\d\w', '123abcd456')
>> <re.Match object; span=(0, 4), match='123a'>

# 2자리 모든 패턴과 2자리 문자 검색
re.search(r'..\w\w', '@#$#ABCDabcd')
>> <re.Match object; span=(2, 6), match='$#AB'>
```

## 기본 패턴

> **REF** [re — Regular expression operations](https://docs.python.org/3/library/re.html){:target='_blank'}

- **character**
  - a, X, 9 등등 문자 하나하나의 글자들은 정확히 해당 문자와 일치
  - eg. 패턴 test는 test 문자열과 일치하는 지를 검사
- **대소문자**
  - 기본적으로 대소문자 구별
  - 구별하지 않도록 설정도 가능
- **예외 문자**
  - . ^ $ * + ? { } [ ] ( ) \ \|
  - 몇몇 문자들에 대해서는 예외 존재 &rarr; 특별한 의미로 사용
- **. (마침표)** : 어떤 한개의 character와 일치 (newline(엔터) 제외)
- **\w** : 문자 character(대소문자, 숫자) 1개와 일치 [a-zA-Z0-9_]
- **\d** : 숫자 character 1개와 일치 [0-9]
- **\s** : 공백문자와 일치
- **\t, \n, \r** : tab, newline, return
- **^, $** : 각각 문자열의 시작과 끝
- **\\ (백슬래시)**가 붙으면 스페셜한 의미가 없어짐
  - **\\.** : .자체를 의미 
  - **\\\\** : \를 의미


## 메타 캐릭터 (metacharacters)
- 특별한 의미로 사용되는 예외 문자

### \[ \] (대괄호)
- 문자들의 범위를 나타내기 위해 사용
- [] 내부의 메타 캐릭터는 캐릭터 자체를 의미 &rarr; 예외문자로 처리되지 않음
- pattern
  - [나열] : or
  - [시작-끝] : **-**와 함께 사용되면 해당 문자 사이의 범위에 속하는 문자 중 하나
  - [^패턴] : ^가 맨 앞에 사용 되는 경우 NOT처럼 적용 &rarr; 해당 문자 패턴이 아닌 것과 매칭
- eg.  
  - [abck] : a or b or c or k
  - [abc.^] : a or b or c or . or ^
  - [a-d] : abcd
  - [0-9] : 모든 숫자
  - [a-z] : 모든 소문자
  - [A-Z] : 모든 대문자
  - [a-zA-Z0-9] : 모든 알파벳 대소문자 및 숫자
  - [^0-9] : 숫자가 아닌 것

### \\ (백슬래시)
1. 다른 문자와 함께 사용되어 특수한 의미를 지님
   - \d : 숫자 &rarr; [0-9]와 동일
   - \D : 숫자가 아닌 문자 &rarr; [^0-9]와 동일
   - \s : 공백 문자(띄어쓰기, 탭, 엔터 등)
   - \S : 공백이 아닌 문자
   - \w : 알파벳대소문자 숫자 &rarr; [0-9a-zA-Z]와 동일
   - \W : non alpha-numeric 문자 &rarr; [^0-9a-zA-Z]와 동일
2. 메타 캐릭터가 캐릭터 자체를 표현하도록 할 경우 사용
   - \\. , \\\\

### . (마침표)
- 모든 문자를 의미

```python
re.search(r'p.g', 'pig')
>> <re.Match object; span=(0, 3), match='pig'>
```

### ^(틸드), $(달러)
- ^ : 문자열의 맨 앞부터 일치하는 경우 검색. 해당 문자열로 시작
- $ : 문자열의 맨 뒤부터 일치하는 경우 검색. 해당 문자열로 끝

### 반복패턴
- 패턴 뒤에 위치하는 *, +, ?는 해당 패턴이 반복적으로 존재하는지 검사
  - '+' &rarr; 1번 이상의 패턴이 발생
  - '*' &rarr; 0번 이상의 패턴이 발생 (없는 경우도 포함)
  - '?' &rarr; 0 혹은 1번의 패턴이 발생
- 반복 패턴의 경우 greedy하게 검색 &rArr; 가능한 많은 부분이 매칭되도록 작동함  
    e.g) a[bcd]*b 패턴을 abcbdccb에서 검색하는 경우
    - ab, abcb, abcbdccb 전부 가능 하지만 최대한 많은 부분이 매칭된 abcbdccb가 검색된 패턴

### {} (중괄호)
- *, +, ?을 사용하여 반복적인 패턴을 찾는 것이 가능하나, 반복의 횟수 제한은 불가
- 패턴뒤에 위치하는 중괄호{}에 숫자를 명시하면 해당 숫자 만큼의 반복인 경우에만 매칭
  - {4} - 4번 반복
  - {3,4} - 3 ~ 4번 반복

### 미니멈 매칭(non-greedy way)
- 기본적으로 *, +, ?를 사용하면 greedy(맥시멈 매칭)하게 동작함
- *?, +?을 이용하여 해당 기능을 구현 &rarr; 최소한으로 매칭되는 것을 찾아줌

```python
re.search(r'<.+>', '<html>text</html>')
>> <re.Match object; span=(0, 17), match='<html>text</html>'>

re.search(r'<.+?>', '<html>text</html>')
>> <re.Match object; span=(0, 6), match='<html>'>
```

### {}?
- {m,n} : m번 에서 n번 반복하나 greedy하게 동작
- {m,n}? : non-greedy하게 동작 &rarr; 최소 m번만 매칭하면 만족

```python
re.search(r'a{3,5}', 'aaaaa')
>> <re.Match object; span=(0, 5), match='aaaaa'>

re.search(r'a{3,5}?', 'aaaaa')
>> <re.Match object; span=(0, 3), match='aaa'>
```

## grouping
- ()을 사용하여 그루핑
- 매칭 결과를 각 그룹별로 분리 가능
- 패턴 명시 할 때, 각 그룹을 괄호() 안에 넣어 분리하여 사용

```python
m = re.search(r'(\w+)@(.+)', 'test@gmail.com')

print(m)
print(m.group(0))
print(m.group(1))
print(m.group(2))
>> --------------------
<re.Match object; span=(0, 14), match='test@gmail.com'>
test@gmail.com
test
gmail.com
```

## match 함수
- search와 유사하지만 match는 주어진 문자열의 **시작**부터 비교하여 패턴이 있는지 확인
- `search(r'^')` 사용과 같은 기능
- 시작부터 해당 패턴이 존재하지 않다면 None 반환

```python
re.match(r'\d\d\d', '123 is my number')
>> <re.Match object; span=(0, 3), match='123'>

# match 함수에서는 시작부터 검색하므로 반환되는 값이 없음
re.match(r'\d\d\d', 'my number is 123')
>> 

# search 함수는 해당 패턴의 위치에 무관하게 검색을 해줌
re.search(r'\d\d\d', 'my number is 123')
>> <re.Match object; span=(13, 16), match='123'>

# search 함수에 ^(틸드) 캐릭터 사용하면 match 함수와 동일한 기능
re.search(r'^\d\d\d', 'my number is 123')
>> 
```

## findall 함수
- search가 최초로 매칭되는 패턴만 반환한다면, findall은 매칭되는 전체의 패턴을 반환
- 매칭되는 모든 결과를 리스트 형태로 반환

```python
re.findall(r'[\w-]+@[\w.]+', 'test@test.com my email address your@test.com')
>> ['test@test.com', 'your@test.com']
```

## sub 함수
> subtract
{:.comment}  
`re.sub(pattern, replace, string, count[optional])`
- 주어진 string에서 일치하는 모든 pattern을 치환(replace)
- replace : 특정 문자열 또는 함수
- count
  - 0 : 전체 치환 (default)
  - 1 이상 : 해당 숫자만큼 치환 됨
- 결과를 문자열로 다시 반환

```python
re.sub('[\w-]+@[\w.]+', 'EMAIL', 'test@test.com my email address your@test.com')
>> 'EMAIL my email address EMAIL'

re.sub('[\w-]+@[\w.]+', 'EMAIL', 'test@test.com my email address your@test.com', count=1)
>> 'EMAIL my email address your@test.com'
```

## compile 함수
`re.compile(pattern)`  
`RegexObject.function(string)`  
- 동일한 정규표현식을 매번 다시 쓰기 번거로움을 해결
- compile로 해당표현식을 re.RegexObject 객체로 저장하여 사용가능

```python
email_reg = re.compile('[\w-]+@[\w.]+')

email_reg.search('test@test.com my email address your@test.com')
>> <re.Match object; span=(0, 13), match='test@test.com'>
```

# 정규식 예제

## 이메일 주소 추출 
- 아래 뉴스에서 이메일 주소를 추출해 보세요

```python
import requests
from bs4 import BeautifulSoup
# 위의 두 모듈이 없는 경우에는 pip install requests bs4 실행

def get_news_content(url):
    response = requests.get(url)
    content = response.text

    soup = BeautifulSoup(content, 'html5lib')

    div = soup.find('div', attrs = {'id' : 'harmonyContainer'})
    
    content = ''
    for paragraph in div.find_all('p'):
        content += paragraph.get_text()
        
    return content

news1 = get_news_content('https://news.v.daum.net/v/20190617073049838')
print(news1)
>> --------------------
(로스앤젤레스=연합뉴스) 옥철 특파원 = 팀 쿡 애플 최고경영자(CEO)가 16일(현지시간) 실리콘밸리 앞마당 격인 미국 서부 명문 스탠퍼드대학 학위수여식에서 테크기업들을 향해 쓴소리를 쏟아냈다.쿡은 이날 연설에서 실리콘밸리 테크기업들은 자신들이 만든 혼란에 대한 책임을 질 필요가 있다고 경고했다.근래 IT 업계의 가장 큰 이슈인 개인정보 침해, 사생활 보호 문제를 콕 집어 라이벌인 구글, 페이스북 등 IT 공룡을 겨냥한 발언이라는 해석이 나왔다.쿡은 "최근 실리콘밸리 산업은 고귀한 혁신과는 점점 더 거리가 멀어지는 것으로 알려져 있다. 책임을 받아들이지 않고도 신뢰를 얻을 수 있다는 그런 믿음 말이다"라고 꼬집었다.개인정보 유출 사건으로 미 의회 청문회에 줄줄이 불려 나간 경쟁사 CEO들을 향해 일침을 가한 것으로 보인다.그는 또 실리콘밸리에서 희대의 사기극을 연출한 바이오벤처 스타트업 테라노스(Theranos)를 직격했다.쿡은 "피 한 방울로 거짓된 기적을 만들 수 있다고 믿었느냐"면서 "이런 식으로 혼돈의 공장을 만든다면 그 책임에서 절대 벗어날 수 없다"라고 비난했다.테라노스는 손가락 끝을 찔러 극미량의 혈액 샘플만 있으면 각종 의학정보 분석은 물론 거의 모든 질병 진단이 가능한 바이오헬스 기술을 개발했다고 속여 월가 큰손들로부터 거액의 투자를 유치했다가 해당 기술이 사기인 것으로 드러나 청산한 기업이다.쿡은 애플의 경우 프라이버시(사생활) 보호에 초점을 맞춘 새로운 제품 기능들로 경쟁사들에 맞서고 있다며 자사의 데이터 보호 정책을 은근히 홍보하기도 했다.oakchul@yna.co.kr

# email 주소 추출
# email_reg = re.compile('[\w-]+@[\w.]+') # 이 패턴으로는 test@test.com.도 추출이되므로 더 디테일하게 패턴을 수정
email_reg = re.compile('[\w-]+@[\w.]+\w+')

email_reg.search(news1).group()
>> 'oakchul@yna.co.kr'
```

## 웹페이지 찾기
- 다음중 올바른 (http, https) 웹페이지만 찾으시오
  - http, https
  - ://

```python
webs = ['http://www.test.co.kr', 
        'https://www.test1.com', 
        'http://www.test.com', 
        'ftp://www.test.com',  # ftp 아님
        'http:://www.test.com',
       'htp://www.test.com', # htp 아님
       'http://www.google.com', 
       'https://www.homepage.com.'] # 마지막 .com. 아님

# 웹페이지 추출 (http, https)
list = []
for web in webs:
    if re.match('https?://[\w+].+\w+$', web):
        list.append(web)

print(list)
>> ['http://www.test.co.kr', 'https://www.test1.com', 'http://www.test.com', 'http://www.google.com']

# 다른 방법으로 추출
web_reg = re.compile('https?://[\w+].+\w+$')
list(filter(lambda w:web_reg.search(w)!=None, webs))
>> --------------------
['http://www.test.co.kr',
 'https://www.test1.com',
 'http://www.test.com',
 'http://www.google.com']
```
