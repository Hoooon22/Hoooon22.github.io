---
layout: default
title: AWS (DVA) - Dump 2
parent: AWS (DVA)
grand_parent: STUDY
Date: 2024-04-22 16:28:37
---

# AWS Certified Developer Associate - Dump 2
{: .no_toc }

## 2024.03.27 (WED)
{: .no_toc .text-delta }

---
    21 ~ 40

## Question #21
### 정답 (O)
A. API Gateway API에서 개발 단계를 정의합니다. 다른 개발자에게 엔드포인트가 개발 단계를 가리키도록 지시합니다.


## Question #22
### 정답 (X, 오답: (C))
A. Redis 인스턴스용 Amazon ElastiCache를 생성합니다. 전송 중인 데이터와 저장 중인 데이터의 암호화를 활성화합니다. 자주 액세스하는 데이터를 캐시에 저장합니다.


## Question #23
### 내용 체크
- AWS SDK: AWS를 프로그래밍적으로 유기적으로 다루기 위한 개발 도구
  
### 정답 (O)
C. 리포지토리를 호스팅할 Amazon S3 버킷을 생성합니다. 기존 .xml 파일을 S3 버킷으로 마이그레이션합니다. AWS SDK를 사용하여 Amazon S3에서 구성 파일을 읽고 쓰도록 애플리케이션 코드를 업데이트합니다.


## Question #24
### 내용 체크
- AWS Amplify: 사용자 인증, 실시간 데이터, AI/ML, 파일 스토리지 등 백엔드 사용사례를 지원하도록 하는 도구 및 기능 세트
- AWS Elastic Beanstalk: Java, .NET, PHP 등을 사용하여 Apache, Nginx, IIS와 같은 친숙한 서버에서 개발된 웹 애플리케이션 및 서비스를 간편하게 배포하고 조정할 수 있는 서비스
  - 코드를 업로드해서 용량 프로비저닝, 로드 밸런싱, 오토 스케일링, 애플리케이션 상태 모니터링, 배포를 자동으로 처리하도록 구성
- EB CLI: 로컬 리포지토리에서 환경 생성, 업데이트 및 모니터링을 단순화하는 대화형 명령을 제공하는 AWS Elastic Beanstalk용 명령줄 인터페이스

### 정답 (X, 오답: (B))
A. 서버리스 백엔드와 함께 AWS Amplify를 사용하여 각 웹사이트를 호스팅합니다. 원하는 각 환경에 해당하는 저장소 분기를 연결했습니다. 코드 변경 사항을 원하는 브랜치에 병합하여 배포를 시작하세요. 


## Question #25
### 정답 (X, 오답: (B))
C. 하나 이상의 읽기 전용 복제본을 사용하여 Amazon RDS를 배포합니다. 쿼리가 읽기 전용 복제본의 URL을 사용하도록 애플리케이션 코드를 수정합니다.


## Question #26
### 정답 (O)
B. Amazon DynamoDB 테이블을 생성합니다. 각 요청의 고유 식별자를 테이블에 저장합니다. 요청을 처리하기 전에 테이블에서 식별자를 확인하도록 Lambda 함수를 수정합니다. 


## Question #27
### 내용 체크
- ASW ACM: AWS 웹사이트와 애플리케이션을 보호하는 퍼블릭 및 프라이빗 SSL/TCS X.509 인증서와 키를 만들고, 저장하고, 갱신하는 복잡성을 처리

### 정답 (X, 오답: (B))
A. 새 AMI를 생성하고 암호화 매개변수를 지정합니다. 암호화된 AMI를 대상 리전에 복사합니다. 암호화되지 않은 AMI를 삭제합니다.

    암호화되지 않은 AMI에서는 암호화를 활성화할 수 없습니다.  
    AMI 복사본을 암호화하려면 소스 AMI를 먼저 암호화해야 합니다. 소스가 암호화되지 않으면 AMI 복사본을 암호화할 수 없습니다.


## Question #28
### 내용 체크
- Amazon CloudFront: AWS에서 제공하는 CDN(Content Delivery Network)
  - CDN: 콘텐츠 전송 네트워크, 물리적으로 떨어져 있는 사용자에게 컨텐츠를 더 빠르게 제공하는 시스템
  
### 정답 (O)
C. 중앙 S3 버킷에 대한 액세스를 허용하는 CORS(교차 원본 리소스 공유) 구성을 생성합니다. 중앙 S3 버킷에 CORS 구성을 추가합니다.

    자주 발생하는 문제입니다. 웹 애플리케이션은 일부 예외를 제외하고 기본적으로 다른 도메인의 리소스에 액세스할 수 없습니다. 액세스할 리소스에 CORS를 구성해야 합니다.  
    -> CORS: Cross-Origin Resource Sharing의 약자로, 출처가 다른 자원들을 공유한다는 뜻으로, 한 출처에 있는 자원에서 다른 출처에 있는 자원에 접근하도록 하는 개념


## Qustion #29
### 내용 체크
- Amazon Kinesis: 실시간으로 데이터 스트림을 수집, 처리, 분석해주는 서비스 (샤드 조절을 통해)
  - 위 서비스는 완전 관리형이라, 인프라 관리를 하지 않아도 됨
- 클릭스트림 데이터: 소비자 행동을 파악하는 데 사용할 수 있는 웹 트래픽 등
- PutRecords API
- Amazon SNS: 구독중인 Service 또는 사용자(Client)에 메시지 전달, 전송을 조정 및 관리하는 웹서비스 (알림서비스)

### 정답 (X, 오답: (B))
A. 지수 백오프로 재시도를 구현합니다.
C. 요청 빈도 및/또는 크기를 줄입니다. 


## Question #30
### 정답 (O)
B. Amazon Simple Email Service(Amazon SES)를 사용하여 이메일 알림을 보내는 AWS Lambda 함수를 생성합니다. 함수에 대한 Amazon Cognito 사후 인증 Lambda 트리거를 추가합니다.


## Question #31
### 정답 (X, 오답: (A))
B. PutObject API 작업을 호출할 때 x-amz-server-side-encryption 헤더를 설정합니다.
    