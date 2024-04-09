---
layout: default
title: AWS (DVA) - Dump 1
parent: AWS (DVA)
grand_parent: STUDY
Date: 2024-03-27 17:24:14
---

# AWS Certified Developer Associate - Dump 1
{: .no_toc }

## 2024.03.27 (WED)
{: .no_toc .text-delta }

---

## Question #1
### 문제
```
한 회사가 Amazon EC2 인스턴스에 애플리케이션을 구현하고 있습니다. 애플리케이션은 들어오는 트랜잭션을 처리해야 합니다. 애플리케이션이 유효하지 않은 거래를 감지하면 애플리케이션은 회사 지원팀에 채팅 메시지를 보내야 합니다. 메시지를 보내려면 애플리케이션이 채팅 API를 사용하여 인증할 액세스 토큰을 검색해야 합니다.  
개발자는 액세스 토큰을 저장하는 솔루션을 구현해야 합니다. 액세스 토큰은 저장 및 전송 중에 암호화되어야 합니다. 액세스 토큰은 다른 AWS 계정에서도 액세스할 수 있어야 합니다.  
최소한의 관리 오버헤드로 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?
```
```
A. AWS Key Management Service(AWS KMS) AWS 관리형 키를 사용하는 AWS Systems Manager Parameter Store SecureString 매개변수를 사용하여 액세스 토큰을 저장합니다. 다른 계정의 액세스를 허용하려면 매개변수에 리소스 기반 정책을 추가하세요. Parameter Store에 액세스할 수 있는 권한으로 EC2 인스턴스의 IAM 역할을 업데이트합니다. 암호 해독 플래그가 활성화된 상태로 Parameter Store에서 토큰을 검색합니다. 해독된 액세스 토큰을 사용하여 메시지를 채팅에 보냅니다.  

B. AWS Key Management Service(AWS KMS) 고객 관리형 키를 사용하여 액세스 토큰을 암호화합니다. Amazon DynamoDB 테이블에 액세스 토큰을 저장합니다. DynamoDB 및 AWS KMS에 액세스할 수 있는 권한으로 EC2 인스턴스의 IAM 역할을 업데이트합니다. DynamoD에서 토큰 검색EC2 인스턴스에서 AWS KMS를 사용하여 토큰을 해독합니다. 해독된 액세스 토큰을 사용하여 메시지를 채팅에 보냅니다.  

C. AWS Key Management Service(AWS KMS) 고객 관리형 키와 함께 AWS Secrets Manager를 사용하여 액세스 토큰을 저장합니다. 다른 계정의 액세스를 허용하려면 보안 비밀에 리소스 기반 정책을 추가하세요. Secrets Manager에 액세스할 수 있는 권한으로 EC2 인스턴스의 IAM 역할을 업데이트합니다. Secrets Manager에서 토큰을 검색합니다. 해독된 액세스 토큰을 사용하여 메시지를 채팅에 보냅니다.  

D. AWS Key Management Service(AWS KMS) AWS 관리형 키를 사용하여 액세스 토큰을 암호화합니다. Amazon S3 버킷에 액세스 토큰을 저장합니다. 다른 계정의 액세스를 허용하려면 S3 버킷에 버킷 정책을 추가하세요. Amazon S3 및 AWS KMS에 액세스할 수 있는 권한으로 EC2 인스턴스의 IAM 역할을 업데이트합니다. S3 버킷에서 토큰을 검색합니다. EC2 인스턴스에서 AWS KMS를 사용하여 토큰을 해독합니다. 해독된 액세스 토큰을 사용하여 메시지를 채팅에 보냅니다.
```

### 내용 정리
- AWS KMS(암호화 암호 서명): 데이터를 암호화 할때 사용되는 암호화 Key를 안전하게 관리하는데 목적을 둔 서비스

- AWS Secrets Manager: 다른 AWS 서비스와 통합되어 암호의 사용을 안전하게 저장

### 정답
정답: D
    -> 그런데 커뮤니티 투표 분배는 C가 84%다..


## Question #2
### 모르는 내용
- Amazon SQS: 서버들끼리 사용할 수 있는 메세지 큐를 제공하는 서비스
- 시스템이 처리해야 할 To-Do List

### 정답 (O)
D. 모든 계정에서 이벤트를 수신하도록 기본 계정 이벤트 버스에 대한 권한을 구성합니다. 각 계정에서 Amazon EventBridge 규칙을 생성하여 모든 EC2 인스턴스 수명 주기 이벤트를 기본 계정 이벤트 버스로 보냅니다. 모든 EC2 인스턴스 수명 주기 이벤트와 일치하는 기본 계정 이벤트 버스에 EventBridge 규칙을 추가합니다. SQS 대기열을 규칙의 대상으로 설정합니다. 최다 투표

## Question #3
### 모르는 내용
- Amazon Cognito: 웹 및 모바일 앱에 대한 인증과 권한 부여 그리고 사용자 관리를 제공하고 기존의 아이디, 패스워드 방식 이외에도 Facebook, Google 등의 여러 글로벌 회사의 소셜 로그인 기능을 제공하는 서비스.
  - Cognito는 사용자 풀(user pool)과 자격 증명 풀(identity pool)로 구성되어 있다.
    - 사용자 풀: 사용자의 가입과 로그인을 제공하는 사용자 저장소
    - 자격 증명 풀: 사용자 풀에 저장된 정보를 바탕으로 AWS 인프라의 여러 서비스에 대한 권한을 부여할 수 있는 서비스
- Amazon S3: 업계 최고의 확장성, 데이터 가용성 및 보안과 성능을 제공하는 객체 스토리지 서비스

### 정답 (O)
D. Amazon Cognito 자격 증명 접두사 내의 IAM 정책을 사용하여 사용자가 Amazon S3에서 자신의 폴더를 사용하도록 제한합니다. 최다 투표

## Question #4
### 모르는 내용
