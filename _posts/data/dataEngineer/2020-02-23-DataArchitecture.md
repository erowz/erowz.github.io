---
date: 2020-02-23 00:18 +09:00
title: DataEngineer 01 - 데이터 아키텍처
category: DataEngineer
tags: [data, dataengineer, dataarchitecture]
---
{% assign path = page.imgpath | append: page.id %}

# 데이터 엔지니어의 필요성

### 문제 해결을 위한 가설 검증 단계

- 모든 비지니스가 동일한 데이터 분석 환경을 갖출 수가 없다
- 성장 단계에 따라 선택 집중해야 하는 분석 환경이 다르다

![Image]({{path}}/img01.png)  
*데이터 기반 가설 검증단계*

# 데이터 아키텍처 시 고려사항

1. 비지니스 모델 상 가장 중요한 데이터는 무엇?
   - 비용 대비 비지니스 임팩트가 높은 데이터 확보

2. 데이터 거버넌스(Data Governance)  

   |원칙(Principle)|조직(Organization)|프로세스(Process)|
   |:--|:--|:--|
   |- 데이터를 유지하기 위한 가이드<br/>- 보안, 품질, 변경관리|- 데이터를 관리할 조직의 역할과 책임<br/>- 데이터 관리자, 데이터 아키텍트 담당자 지정|- 데이터 관리를 위한 시스템<br/>- 작업절차, 모니터 및 측정|

3. 유연하고 변화 가능한 환경 구축
- 새로운 기술을 빠르게 반영할 수 있도록 구축

4. Real Time(실시간) 데이터 핸들링이 가능한 시스템
- 데이터 아키텍쳐는 모든 스피드의 데이터를 핸들링
  - Real Time Streaming Data Processing
  - Cronjob : 스케쥴링을 통해서 데이터를 처리하는 시스템
  - Serverless Triggered Data Processing 

5. 시큐리티
- 데이터를 안전하게 보관

6. 셀프 서비스 환경 구축
- BI Tools
- Query System for Analysis
- Front-end data applications

# 데이터 시스텝 옵션

### API
- 마케팅, CRM, ERP 등 다양한 플랫폼 및 소프트웨어들은 API를 통해 데이터를 주고 받을 수 있는 환경을 구축하여 생태계를 생성

### Relational Database
- 대부분의 서비스들이 가장 많이 쓰고 있는 데이터 시스템

### NoSQL Database
- Not Only SQL
- Unstructured, Schema Less Data
- Scale horizontally (예: 메신저)
- Highly scalable / Less expensive to maintain

### Hadoop, Spark, Presto 등의 빅데이터 처리
- Distributed Storage System / MapReduce를 통한 병렬 처리
  - 나눠서 처리한 저장 시스템
- Spark:
  - Hadoop의 진화된 버전으로 빅데이터 분석 환경에서 Real Time 데이터를 프로세싱하기에 더 최적화
  - Java, Python, Scala를 통한 API를 제공하여 애플리케이션 생성 가능
  - SQL Query 환경을 서포트하여 분석가들에게 더 각광

### Serverless Framework
- Triggered by http requests, database events, queuing services
- 장점
  - Pay as you use
  - Form of functions
  - $3^{rd}$ Party 앱들 및 다양한 API를 통해 데이터를 수집 정제하는데 유용

# 데이터 파이프라인
- 데이터를 옮기는 개념
- eg.
  - API &rarr; database
  - database &rarr; database
  - API &rarr; BI Tool

![Image]({{path}}/img02.png)  
*데이터 파이프라인 예시*

### 데이터 파이프라인이 필요한 경우
- 다양한 데이터 소스들로부터 많은 데이터를 생성하고 저장하는 서비스
- 데이터 사일로 : 마케팅, 어카운팅, 세일즈, 오퍼레이션 등 각 영역의 데이터가 서로 고립되어 있는 경우 &rarr; 데이터 통합 필요
- 실시간 혹은 높은 수준의 데이터 분석이 필요한 비지니스 모델
- 클라우드 환경으로 데이터 저장

### 데이터 파이프라인 구축 시 고려사항
1. Scalability : 데이터가 기하급수적으로 급증해도 작동하는가
2. Stability : Error, Data Flow 등 다양한 모니터링
3. Security : 데이터 이동 간 보안 관련 리스크

# 데이터 프로세싱 자동화
- 필요한 데이터의 추출/수집/정제의 과정을 자동으로 머신이 처리하도록 하는 것
- eg. 자동으로 정해진 시간에 API를 통해 정보를 가져와 Database에 저장하도록 설정

![Image]({{path}}/img03.png){:width='600px'}  
*AWS Data Pipeline, AWS Step Functions 등*

### 자동화 고려사항
1. Data Processing Steps
   - API로 정보를 가져와서 정제하고 저장한 후 알고리즘을 적용하는 등의 단계 설정
2. Error Handling 및 Monitoring
   - 오류 발생으로 실패 시 재시도 횟수 설정 등
   - Performance 등을 지속적으로 관찰
     - Python Logging Package
        ![Image]({{path}}/img04.png){:width='600px'}  
     - Cloud Logging Systems
       - AWS Cloudwatch
       - AWS Data Pipeline Errors
3. Trigger / Scheduling  
![Image]({{path}}/img05.png){:width='600px'}  

# 빅데이터 처리를 위한 데이터 레이크

[![Image]({{path}}/img06.png){:width='600px'}]({{path}}/img06.png)
- Amazon S3 : 빅데이터 저장소
- Amazon EMR : Spark에 특화된 컴퓨팅 시스템
- Amazon RedShift : 대용량 데이터 저장소 (RDB)
- Amazon Athena : Spark 기반의 Presto라느 엔진 위에 올려진 서버리스 프레임워크
- Amazon RDS : Relational Database

![Image]({{path}}/img07.png){:width='600px'}  
*넷플릭스 데이터 시스템 예시*

# AD hoc vs Automated

### AD hoc
- 원할 때 분석하도록 환경을 구축하는 것
- Ad hoc 분석 환경 구축은 서비스를 지속적으로 빠르게 변화시키기 위해 필수 적인 요소
- 이니셜 데이터 삽입, 데이터 Backfill 등을 위해 Ad hoc 데이터 프로세싱 시스 템 구축 필요

### Automated
- 이벤트, 스케쥴 등 트리거를 통해 자동화 시스템 구축

# Spotify 프로젝트

### 데이터 수집 프로세스

![Image]({{path}}/img08.png){:width='600px'}  
- 아티스트 관련 데이터 수집
  - 자동화된 프로세스 : 챗봇 메시지로 시작해서 데이터 수집
  - Ad hoc으로 데이터 수집

### 데이터 분석 환경 구축
- 데이터를 어떻게 compute해서 사용할 지

![Image]({{path}}/img09.png){:width='600px'}  

### 서비스 관련 데이터 프로세스
![Image]({{path}}/img10.png){:width='600px'}  
- Compute Engine : Spark 사용
- Service Data : DynamoDB 
  - NoSQL 사용 이유 : performance, schema가 없는 NoSQL의 데이터의 확장성

> **REF**  
> 패스트캠퍼스 - 데이터 엔지니어 강의 / 한승수 강사