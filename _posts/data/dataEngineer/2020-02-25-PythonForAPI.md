---
date: 2020-02-25 03:56 +09:00
title: DataEngineer 06 - Python for API
category: DataEngineer
tags: [data, dataengineer, python, api, spotify]
---
{% assign path = page.imgpath | append: page.id %}

# Python 기본 구조

```python
import sys  # python system 관련 패키지

def main():

    print('main start')

# 이 파일이 직접 실행되었을 때 수행되는 부분
# 근데 왜 __main__인 건데?? 이런 건 설명안해주네. ㅡㅡ;;
if __name__ == '__main__':
    main()

# 모듈로 임포트 될 때 수행되는 부분 (확인용)
else:
    print('This script is being imported')
```   

&dArr;   

```shell
$ python3 spotify_api.py 
python start

$ python3
Python 3.7.3 (default, Mar 27 2019, 09:23:15) 
[Clang 10.0.1 (clang-1001.0.46.3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import spotify_api
This script is being imported
```

# sys
> System
{:.comment}  
- 기본 설치되어 있는 패키지

### sys.exit([_arg_])
> **REF** [Python sys](https://docs.python.org/3/library/sys.html#sys.exit){:target='_blank'}  

- 파이썬 종료 함수
- arg : 종료 상태를 의미하는 Integer(기본값=0) 또는 객체
  - 0 : successful termination
  - 0 이외의 숫자 (0–127) : abnormal termination
    - 2 : 일반적으로 Unix에서 Command line syntax errors를 의미
    - 1 : 나머지 모든 오류를 의미

# Requests Module
> Python Library
{:.comment}  

> **REF** [Requests: HTTP for Humans > Deleoper Interface](https://requests.readthedocs.io/en/master/api/){:target='_blank'}

```python
>>> import requests
>>> req = requests.request('GET', 'https://httpbin.org/get')
>>> req
<Response [200]>
```

## 설치
- python 2.X  
```shell
$ pip install requests
```

- python 3.X : 아래 명령어 중 가능한 방법으로 설치 진행  
```shell
$ pip3 install requests
$ pip3 install requests --user
$ sudo pip3 install requests
```

## Syntax

### Request
```python
requests.request(method, url, **kwargs)
```
- method : GET, HEAD, POST, PUT, DELETE
- url : Endpoint
- \*\*kwargs : 그외 다양한 파라미터 추가 가능

### HEAD
```python
requests.head(url, **kwargs)
```

### GET
```python
requests.get(url, params=None, **kwargs)
```

### POST
```python
requests.post(url, data=None, json=None, **kwargs)
```
- data : (optional) Dictionary, list of tuples, bytes, or file-like object to send in the body of the Request.
- json : (optional) json data to send in the body of the Request.

### PUT
```python
requests.put(url, data=None, **kwargs)
```

### PATCH
```python
requests.patch(url, data=None, **kwargs)
```

# API 정보

## Authorization
> **DOC** [Client Credentials Flow](https://developer.spotify.com/documentation/general/guides/authorization-guide/){:target='_blank'} : OAuth가 아니므로 Web API 부분 참고 

- You do : Login with your Client ID and Secret Key.
- You get : Access token.

![Image]({{path}}/img01.png){:width='500px'}  
*Client Credentials Flow*

### Endpoints
`POST https://accounts.spotify.com/api/token`

### Header Fields
```python
headers = {
    "Authorization": "Basic <base64 encoded client_id:client_secret>"
}
```
- **Authorization**
  - Required
  - `Basic <base64 encoded client_id:client_secret>` 형식으로 인코딩해서 전송 입력
    - base64 : string을 인코딩하는 방식
```python
# python 2.X
Basic base.b64encode(client_id:client_secret)
# python 3.X
Basic base.b64encode(client_id:client_secret.encode('UTF-8')).decode('ascii')
```

### Body parameter
```python
data = {
    "grant_type": "client_credentials"
}
```
- application/x-www-form-urlencoded로 인코딩
- **grant_type**
  - Required
  - client_credentials로 설정 : OAuth 2.0에 따라 지정된 값

### Response
`response.text`  
- return type : string
- json으로 변환해서 사용 : `json.load(text)[key]`
  - access_token
  - token_type
  - expires_in : 사용 가능 기한
  
```json
{
   "access_token": "NgCXRKc...MzYjw",
   "token_type": "Bearer",
   "expires_in": 3600,
}
```

## Search
> **DOC** [Search for an Item](https://developer.spotify.com/documentation/web-api/reference/search/search/)  

### Endpoints  
`GET https://api.spotify.com/v1/search`  

### Request parameters

#### Header Fields
```python
headers = {
    "Authorization": "Bearer {}".format(access_token)
}
```
- **Authorization**
  - Required

#### Query Parameters
```python
params = {
    "q": "BTS",
    "type": "artist",
    "limit": "5"
}
```
- **q**	
  - Required
  - Search [query](https://developer.spotify.com/documentation/web-api/reference/search/search/#writing-a-query---guidelines) keywords and optional field filters and operators.
  - eg. `q=roadhouse%20blues`
- **type**	
  - Required
  - A comma-separated list of item types to search across.
  - Valid types : album , artist, playlist, track
- **market** : Optional. 지역
- **limit** : Optional. 결과 개수 설정
- **offset** : Optional. 데이터 호출 인덱스 설정
- **include_external**
  - Optional
  - Possible values: audio &rarr; 외부 음원 컨텐츠(?)

# API 호출

### Request API
- expires_in에 의해 토큰을 다시 요청하는 일 발생 가능
- 토큰 요청하는 기능을 별도 클래스로 분리해서 관리하는 것이 용이

```python
import sys
import requests  # http 통신
import base64  # string을 인코딩하는 방식
import json
import logging  # log를 관리하는 패키지

client_id = ""
client_secret = ""


def main():

    headers = get_headers(client_id, client_secret)
    print(headers)

    params = {
        "q": "BTS",
        "type": "artist",
        "limit": "3"
    }

    r = requests.get("https://api.spotify.com/v1/search", params=params, headers=headers)
    print(r.status_code)
    print(r.text)

    sys.exit(0)  # 코드 종료


def get_headers(client_id, client_secret):

    endpoint = "https://accounts.spotify.com/api/token"

    # python 3.X >> encode("UTF-8")과 decode('ascii') 추가 설정 필요
    encoded = base64.b64encode("{}:{}".format(
        client_id, client_secret).encode('UTF-8')).decode('ascii')

    headers = {
        "Authorization": "Basic {}".format(encoded)
    }

    payload = {
        "grant_type": "client_credentials"
    }

    # 결과 > r.status_code(결과 상태), r.text(내용)
    r = requests.post(endpoint, data=payload, headers=headers)

    # temp for check
    # print('status:', r.status_code)
    # print('text:', r.text)
    # print('headers:', r.headers)

    # string -> json
    access_token = json.loads(r.text)['access_token']

    # temp for check
    # print('access_token:', access_token)

    headers = {
        "Authorization": "Bearer {}".format(access_token)
    }

    return headers


if __name__ == '__main__':
    main()

```

### Response
- status : 200
- response.text
```json
{
    "access_token":"BQAggPn-ZRd435MxxQPbolUMoirC5UQyRMFIxgXM_Lfsv8_ORWhfnjqfodl8Kj0Kfb0R2giyi8kwJpWR5H0",
    "token_type":"Bearer",
    "expires_in":3600,
    "scope":""
}
```
- response.headers
```json
{
    'date': 'Tue, 25 Feb 2020 10:43:03 GMT', 
    'content-type': 'application/json', 
    'set-cookie': '__Host-device_id=AQBfw4T9ewXqgYbuOw3srbJZJo7OVT6QVVKqNsHoZsqYfVVc46hL1_-wJ-JZT57do3A1Kld_sNIEZWVS87R8dN37spMKOEKtr0s;Version=1;Path=/;Max-Age=2147483647;Secure;HttpOnly;SameSite=Lax', 
    'server': 'envoy', 
    'x-envoy-upstream-service-time': '3', 
    'strict-transport-security': 'max-age=31536000', 'x-content-type-options': 'nosniff', 
    'vary': 'Accept-Encoding', 
    'content-encoding': 'gzip', 
    'Via': 'HTTP/2 edgeproxy, 1.1 google', 
    'Alt-Svc': 'clear', 
    'Transfer-Encoding': 'chunked'
}
```
- access_token : BQAyzteLRRLDMl9TAV5x3fYE5LArLLqNLEXksvhmULU_5raKEa8SFV0g9F-9x-3TknJN2cvzu4IIueaAJC8
- headers
```json
{'Authorization': 'Bearer BQAK8Kt-5scwVO7YyW_N16esnIHl4t8ClRWMgQJmTOlAR7KqdIEy8WJS_TCGbPLi6VfEe5WI7jZ2e0ssArM'}
```
- search result
```json
{
  "artists" : {
    "href" : "https://api.spotify.com/v1/search?query=BTS&type=artist&offset=0&limit=3",
    "items" : [ {
      "external_urls" : {
        "spotify" : "https://open.spotify.com/artist/3Nrfpe0tUJi4K4DXYWgMUX"
      },
      "followers" : {
        "href" : null,
        "total" : 16689729
      },
      "genres" : [ "k-pop", "k-pop boy group" ],
      "href" : "https://api.spotify.com/v1/artists/3Nrfpe0tUJi4K4DXYWgMUX",
      "id" : "3Nrfpe0tUJi4K4DXYWgMUX",
      "images" : [ {
        "height" : 640,
        "url" : "https://i.scdn.co/image/0c9057cb30520f9f883a220051260fc66a2f3ffa",
        "width" : 640
      }, {
        "height" : 320,
        "url" : "https://i.scdn.co/image/34ee854082d0ea4d571e2ecf7f4aecea61270ad0",
        "width" : 320
      }, {
        "height" : 160,
        "url" : "https://i.scdn.co/image/156147697b696d4a6180e037dc1e2a33117d8d4a",
        "width" : 160
      } ],
      "name" : "BTS",
      "popularity" : 96,
      "type" : "artist",
      "uri" : "spotify:artist:3Nrfpe0tUJi4K4DXYWgMUX"
    }, {
      "external_urls" : {
        "spotify" : "https://open.spotify.com/artist/51sg5jUqKu2tkbmPlwPrNH"
      },
      "followers" : {
        "href" : null,
        "total" : 151868
      },
      "genres" : [ ],
      "href" : "https://api.spotify.com/v1/artists/51sg5jUqKu2tkbmPlwPrNH",
      "id" : "51sg5jUqKu2tkbmPlwPrNH",
      "images" : [ ],
      "name" : "BTS World",
      "popularity" : 47,
      "type" : "artist",
      "uri" : "spotify:artist:51sg5jUqKu2tkbmPlwPrNH"
    }, {
      "external_urls" : {
        "spotify" : "https://open.spotify.com/artist/1Dx8CcTQA8bWYen7zXsNW0"
      },
      "followers" : {
        "href" : null,
        "total" : 112
      },
      "genres" : [ ],
      "href" : "https://api.spotify.com/v1/artists/1Dx8CcTQA8bWYen7zXsNW0",
      "id" : "1Dx8CcTQA8bWYen7zXsNW0",
      "images" : [ {
        "height" : 640,
        "url" : "https://i.scdn.co/image/14d24eb32432f44259c618716659c713508d89db",
        "width" : 640
      }, {
        "height" : 300,
        "url" : "https://i.scdn.co/image/d03dff8d71073e3ec7e34f0bc6d0c6afa2db3996",
        "width" : 300
      }, {
        "height" : 64,
        "url" : "https://i.scdn.co/image/f8e0646093672055d9ab6f1c766fb4203b18d39e",
        "width" : 64
      } ],
      "name" : "BTSC",
      "popularity" : 32,
      "type" : "artist",
      "uri" : "spotify:artist:1Dx8CcTQA8bWYen7zXsNW0"
    } ],
    "limit" : 3,
    "next" : "https://api.spotify.com/v1/search?query=BTS&type=artist&offset=3&limit=3",
    "offset" : 0,
    "previous" : null,
    "total" : 40
  }
}
```

## Error Handling

### try except
```python
try:
    r = requests.get("https://api.spotify.com/v1/search", params=params, headers=headers)
except:
    logging.error(r.text)
    sys.exit(1)
```  
&dArr; _client_id를 임의로 변경했을 경우의 결과_  
```shell
$ python3 spotify_api.py 
Traceback (most recent call last):
  File "spotify_api.py", line 76, in <module>
    main()
  File "spotify_api.py", line 13, in main
    headers = get_headers(client_id, client_secret)
  File "spotify_api.py", line 63, in get_headers
    access_token = json.loads(r.text)['access_token']
KeyError: 'access_token'
```  

### Status Code에 따라 상황 처리
```python
r = requests.get("https://api.spotify.com/v1/search", params=params, headers=headers)

if r.status_code != 200:  # 정상 완료되지 않았을 때
    # 오류 정보를 logging을 통해 띄운다
    logging.error(json.load(r.text))

    if r.status_code == 429:  # 요청이 너무 많이 된 경우

        # sporify의 경우 Rate Limiting(같은 endpoint로 너무 많이 접속한 경우)인 경우
        # -> header의 'Retry-After' 값(초 단위의 수)을 기다린 후 재시도 가능
        retry_after = json.load(r.headers)['Retry-After']

        # 지정한 초 동안 멈춰있도록 설정
        time.sleep(int(retry_after))

        # 기다린 후 API 호출 재시도
        r = requests.get("https://api.spotify.com/v1/search", params=params, headers=headers)

    elif r.status_code == 401:  # access_token is expired

        headers = get_headers(client_id, client_secret)
        r = requests.get("https://api.spotify.com/v1/search",
                         params=params, headers=headers)
    
    else:  ## 알 수 없는 오류의 경우
        sys.exit(1)  ## 위에서 오류만 남긴 처리를 끝으로 종료
```

> **REF**  
> 패스트캠퍼스 - 데이터 엔지니어 강의 / 한승수 강사