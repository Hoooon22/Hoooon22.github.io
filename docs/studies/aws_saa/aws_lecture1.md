---
layout: default
title: AWS 강의 - AWS 서버리스로 서버 없이 간단한 웹 애플리케이션 만들기
parent: AWS (SAA)
grand_parent: STUDY
---

# AWS 강의 - AWS 서버리스로 서버 없이 간단한 웹 애플리케이션 만들기
{: .no_toc }

## 2023.09.11 (MON)
{: .no_toc .text-delta }

---

# 서버리스란?

## 패러다임의 전환

1. 물리적 머신
2. Virtual machines (VM) 
    - ex) ec2
    - 컴퓨터 및 장비 별로 버전 차이 등으로 종속성 문제가 발생하는 단점이 존재
3. Containerization
    - VM의 단점을 해소
    - 필요에 따라 서버 증설 등의 여러가지 밑단의 내용들을 신경써야함
4. **Serverless**
    - AWS 차원에서 모든 리소스들을 추상화함.
    - 지속적인 스케일링
    - 사용한 만큼만 과금
    - 유지보수 ZERO
    - 때문에, 비즈니스 가치에 집중할 수 있다.

## 서버리스란?

- 서버 관리 필요없음
- 사용한 만큼만 지불
- 요청에 맞게 스케일링
- 높은 보안 수준

## 다양한 범주의 서버리스 서비스

![출처 : AWS](../../../../assets/images/aws_saa/스크린샷 2023-09-11 오전 9.29.36.png)
> 출처 : AWS

- 대표적으로 AWS Lambda
- 네모 표시는 실습 때, 살펴볼 내용


# AWS Lambda

## AWS Lambda

- 불필요한 서버 관리
- 자동 확장
- 고가용성 및 보안
- 사용한 만큼만 지불

![출처 : AWS](../../../../assets/images/aws_saa/스크린샷 2023-09-11 오전 9.34.59.png)
> 출처 : AWS

## AWS Lambda 사용 사례

- Web Apps
    - 정적 웹사이트
    - 복합적 웹앱
- Backends
    - 앱 & 서비스
    - 모바일
    - IoT
- Data Processing
    - Real  time
    - MaoReduce
    - Batch
- Chatbots
    - Powering chatbot loginc
- etc

# Amazon API Gateway

## API Gateway는 API 기반 아키텍처의 관문

API : 응용프로그램과 운영체제 간의 통신을 연결해주는 인터페이스

API Gateway : 서비스가 많아지면, 버전 관리 및 관리가 매우 힘들어진다. 이를 해소시켜주는 것. (like 정문 역할)

# Amazon DynamoDB

## Amazon DynamoDB

대규모 성능에 최적화된 완전 관리형 NoSQL 데이터베이스 서비스

- 서버리스
    - 유지관리 불필요
    - 오토 스케일링
    - 고가용성 및 내결함성
- 높은 성능
    - 초당 수백만의 요청 처리 및 짧은 지연시간
    - 다른 AWS 서비스와 통합
- 보안 및 엑세스
    - 전송 중 및 저장 시 암호화

## Core Concepts - Tables, Items, Attributes, Indexes

![출처 : AWS](../../../../assets/images/aws_saa/스크린샷 2023-09-11 오전 9.53.58.png)
> 출처 : AWS

- Primary Key를 잘 설계하는 것이 중요.
    - Unique하게

## 데이터 베이스 확장

- SQL
    - 수직정 확장
- NoSQL
    - 수평적 확장 : 다수의 샤드로 수평확장

# 실습

## 실습 과정
1. Lambda 생성
2. DynamoDB, API Gateway 생성

https://catalog.us-east-1.prod.workshops.aws/workshops/600420b7-5c4c-498f-9b80-bc7798963ba3/ko-KR/serverless