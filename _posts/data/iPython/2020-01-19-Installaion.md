---
date: 2020-01-19 16:14 +09:00
title: Python & Jupyter Notebook 설치
category: iPython
tags: [python, jupyternotebook]
---
{% assign path = page.imgpath | append: page.id %}

# Python 설치

데이터 분석이 목적인 경우 **아나콘다(Anaconda)로 설치**하기를 권장한다. 아나콘다로 설치하면 파이썬과 데이터 분석 관련 패키지의 설치 및 관리가 가능하다.

## Anaconda

**설치 파일 다운로드**

\- [https://www.anaconda.com/distribution/#download-section](https://www.anaconda.com/distribution/#download-section){:target='_blank'}  
\- version : 3.7  
![install]({{path}}/img01.png){:width='500px'}

**설치**

\- Anaconda3-2019.10-MacOSX-x86\_64.pkg 실행  
\- 기본 설정값으로 설치 진행  
![install]({{path}}/img02.png){:width='500px'}  

![install]({{path}}/img03.png){:width='500px'}  
*[https://www.jetbrains.com/pycharm/](https://www.jetbrains.com/pycharm/){:target='_blank'}*  

![install]({{path}}/img04.png){:width='500px'}  
*[https://anaconda.org/](https://anaconda.org/){:target='_blank'}*  

**※ Windows의 경우**

- Select Installation Type : Just Me로 선택해서 로컬 계정에 설치하라고 한다. 단, 사용자 이름이 한글일 경우 All Users로 C 드라이브에 설치 진행. 다만 All Users로 설치할 경우 권한 문제가 발생할 수 있으니 주의할 것.
- Advanced Option : Add Anaconda to my PATH environment variables와 Register Anaconda as my default Python3.7 둘 다 체크

# Jupyter Notebook

- markdown 기능 제공
- python의 print 함수를 사용하지 않아도 출력 기능 동작  
    _※ 마지막에 위치한 값 하나만 output으로 출력됨_

## 실행 방법

#### 1\. terminal

`jupyter notebook`을 입력해서 실행

![jupyter]({{path}}/img05.png)

#### 2\. Anaconda Navigator

Applications > Anaconda Navigator 실행 > Launch Jupyter Notebook
![jupyter]({{path}}/img06.png)

**Jupyter Notebook 실행 화면**

![jupyter]({{path}}/img07.png)

## 사용 방법

웹 브라우저에서 구글 드라이브를 사용하듯이 로컬 스토리지를 브라우저에서 탐색한다고 생각하면 이해가 쉬울 듯 하다.

### Jupyter Notebook 시작

\- python 파일 생성 : New > Python 3 > Untitled.ipynb가 생성됨 (_※ ipynb 파일은 일반 탐색기에서는 실행되지 않음_)  
\- 동일 경로에 사용할 데이터 파일 준비
![jupyter]({{path}}/img08.png)

### Jupyter Notebook 실행

**파일명 변경**

\- Rename : File > Rename으로 파일명 변경
![jupyter]({{path}}/img09.png)

> **Cell**  
> \- 박스 하나를 셀이라고 부름  
> \- 코드(code) 또는 마크다운(markdown) 등 작성 가능  
> \- 각 셀마다 실행(run)  
> \- 상태 표시  
> · 파란색 : 선택된 상태를 의미. Enter 키를 누르거나 마우스 클릭하면 녹색으로 바뀌며 편집 모드로 변경됨  
> · 녹색 : 코드 작성 가능. Esc 키를 누르거나 셀 바깥을 클릭하면 파란색 선택 모드로 변경됨

**단축키 도움말 확인**

Command Mode에서 h를 눌러 확인
![jupyter]({{path}}/img10.png)

**코드 입력 및 실행**

\- 편집 모드로 선택 후 코드 입력 후 실행
![jupyter]({{path}}/img11.png)

### csv file 사용하기

**파일 로딩**

\- 파이썬의 패키지인 판다스(pandas)의 read\_csv()라는 기능을 사용하여 로딩 가능  
\- 동일 경로의 train.csv 로딩

```
import pandas as pd
pd.read_csv("train.csv")
```

![jupyter]({{path}}/img12.png)

> **상대 경로 설정 방법**  
> \- ../ 상위 폴더로 이동해서 파일의 해당 경로로 이동

### Jupyter Notebook 재실행

파일 종료 후 재실행 시 상위 코드부터 순차적으로 실행을 시켜줘야 정상 작동한다. 예를 들어, 상위 코드에서 pandas를 import해줘야 아래 코드에서 csv file 로딩이 가능하다.

## 단축키

> **\<Edit Mode : 셀 선택 상태\>**  
> **Enter** : 셀 선택 상태(명령 모드)를 편집 상태(입력 모드)로 전환  
> **Esc** : 셀 편집 모드(입력 모드)를 선택 모드(명령 모드)로 전환  
> **h** : 단축키 도움말  
> **a** : 선택된 셀을 위에 새로운 셀 추가  
> **b** : 선택된 셀을 아래에 새로운 셀 추가  
> **f** : 찾기/바꾸기  
> **m** : 선택된 셀을 markdown 상태로 전환  
> **y** : 선택된 셀을 code 편집 상태로 전환  
> **x** : 셀 잘라내기  
> **c** : 셀 복사하기  
> **v** : 셀 붙여넣기  
> **z** : 되돌리기  
> **dd**: 셀 제거하기  
> **x**: 셀 잘라내기
> 
> **\<Command Mode : 셀 편집 상태\>**  
> **Ctrl + Enter** : 셀 실행  
> **Shift + Enter** : 셀 실행 후 아래 셀 선택  
> **Alt + Enter** : 셀 실행 후 아래에 새로운 셀 추가  
> **Tab** : 함수 리스트 호출  
> **Shift + Tab** : 함수 내에서 도움말 호출  
> **Ctrl + /** : 주석 설정/해제

## Jupyter Notebook html 출력 설정

### 1\. Cell 넓이 설정

손쉽게 넓이 조절이 가능하지만 막상 html로 출력해서 블로그에 업로드하기에 적합하지 않아 보인다.

```
from IPython.core.display import display, HTML
display(HTML("<style>.container { width: 100% !important; }</style>"))
```

### 2\. CSS 설정

해당 CSS 설정 삭제하기

- 화면 넓이 설정 : 아래 코드 전체 삭제

```
@media (min-width: 768px) {
  .container {
    width: 768px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 940px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
```

- 배경에서 그림자 효과 제거

```
@media not print {
  #notebook-container {
    padding: 15px;  # - 삭제
    ...
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);  # - 삭제
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);  # - 삭제
  }
}
```

- 프롬프트 넓이 조절  
    : 14ex로 검색해서 11ex로 변경

```
    .prompt {
      /* This needs to be wide enough for 3 digit prompt numbers: In[100]: */
      min-width: 14ex;  # >> 11ex;로 수정
      font-size: 11px;  # 새로 추가
      /* This padding is tuned to match the padding on the CodeMirror editor. */
      padding: 0.4em;
      margin: 0px;
      ...
    }

    /* This class is for the output subarea inside the output_area and after
   the prompt div. */
    div.output_subarea {
      overflow-x: auto;
      padding: 0.4em;
      ...
      max-width: calc(100% - 14ex);  # >> 11ex로 수정
    }
```

- 데이터 테이블 넓이 설정 : 아래 코드 전체 새로 추가

```
    .dataframe {
      width: auto !important;
    }
```