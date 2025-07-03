---
layout: default
title: Backend
nav_order: 1
parent: Study
has_children: true
---

# 백엔드 개발자 학습 로드맵 📚

{: .no_toc }

## 목차
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 📖 개요

이 로드맵은 백엔드 개발자가 되기 위한 체계적인 학습 순서를 정리한 것입니다.  
각 단계를 완성할 때 마다, 체크리스트를 채워가며 학습할 예정입니다.  
항목에 대한 추가 글을 작성했다면, 항목에 링크를 걸어놓았습니다.  

**출처**: [roadmap.sh - Backend Developer Roadmap](https://roadmap.sh/backend)

---

## 🌟 1단계: 기초 지식 (Foundation) 

### 1.1 인터넷의 작동 원리
- [ ] 인터넷이 어떻게 작동하는지 이해
- [ ] 도메인 네임 시스템 (DNS)의 작동 원리
- [ ] 브라우저의 작동 원리
- [ ] HTTP/HTTPS 프로토콜 이해
- [ ] 호스팅의 개념과 종류

### 1.2 버전 관리 시스템
- [ ] Git 기초 명령어 학습
- [ ] GitHub 사용법 익히기
- [ ] GitLab, Bitbucket 등 다른 플랫폼 이해
- [ ] 브랜치 전략 및 협업 워크플로우

### 1.3 터미널 및 명령어 기초
- [ ] 기본 터미널 명령어 (`cd`, `ls`, `mkdir`, `rm`)
- [ ] 텍스트 처리 도구 (`grep`, `awk`, `sed`)
- [ ] 시스템 모니터링 도구 (`tail`, `head`, `less`, `find`)
- [ ] 네트워크 도구 (`curl`, `wget`, `ssh`, `dig`)
- [ ] 프로세스 관리 (`kill`, `lsof`)

---

## 🖥️ 2단계: 프로그래밍 언어 선택 (Pick a Language)

### 2.1 백엔드 언어 중 하나 선택
- [ ] **Python** (초보자 추천)
- [ ] **JavaScript (Node.js)**
- [ ] **Java**
- [ ] **C#**
- [ ] **Go**
- [ ] **Rust**
- [ ] **PHP**
- [ ] **Ruby**

### 2.2 선택한 언어 심화 학습
- [ ] 기본 문법 및 자료구조
- [ ] 객체지향 프로그래밍 (OOP)
- [ ] 함수형 프로그래밍 개념
- [ ] 예외 처리 및 에러 핸들링
- [ ] 패키지 매니저 사용법

---

## 🏠 3단계: 운영체제 및 일반 지식 (OS and General Knowledge)

### 3.1 운영체제 기본 개념
- [ ] 프로세스 관리 (Process Management)
- [ ] 스레드와 동시성 (Threads and Concurrency)
- [ ] 메모리 관리 (Memory Management)
- [ ] 입출력 관리 (I/O Management)
- [ ] 프로세스 간 통신 (Interprocess Communication)

### 3.2 네트워킹 기초
- [ ] OSI 7계층 모델
- [ ] TCP/IP 프로토콜
- [ ] 포트와 소켓
- [ ] 방화벽 및 프록시

---

## 🗄️ 4단계: 데이터베이스 (Databases)

### 4.1 관계형 데이터베이스 (RDBMS)
- [ ] SQL 기초 문법
- [ ] 데이터베이스 설계 및 정규화
- [ ] 인덱스 개념과 활용
- [ ] 트랜잭션 및 ACID 속성
- [ ] 데이터베이스 선택:
  - [ ] **PostgreSQL** (권장)
  - [ ] **MySQL**
  - [ ] **MariaDB**
  - [ ] **MS SQL Server**
  - [ ] **Oracle**

### 4.2 NoSQL 데이터베이스
- [ ] NoSQL 데이터베이스 유형 이해
- [ ] **Document DB**: MongoDB, CouchDB
- [ ] **Key-Value DB**: Redis, DynamoDB
- [ ] **Column DB**: Cassandra
- [ ] **Graph DB**: Neo4j
- [ ] **Time Series DB**: InfluxDB, TimeScale

### 4.3 ORM (Object-Relational Mapping)
- [ ] ORM의 개념과 장단점
- [ ] 선택한 언어에 맞는 ORM 학습
- [ ] N+1 문제 이해 및 해결법

---

## 🔌 5단계: API 개발 (APIs)

### 5.1 REST API
- [ ] RESTful API 설계 원칙
- [ ] HTTP 메소드 활용
- [ ] 상태 코드 이해
- [ ] JSON 데이터 처리
- [ ] API 문서화 (OpenAPI/Swagger)

### 5.2 기타 API 기술
- [ ] **GraphQL**: 쿼리 언어
- [ ] **gRPC**: 고성능 RPC 프레임워크
- [ ] **SOAP**: 엔터프라이즈 환경
- [ ] **WebSockets**: 실시간 통신
- [ ] **Server-Sent Events**: 서버 푸시

---

## 🔐 6단계: 보안 (Security)

### 6.1 인증 및 인가
- [ ] **Basic Auth**: 기본 인증
- [ ] **JWT**: JSON Web Token
- [ ] **OAuth**: 제3자 인증
- [ ] **Cookie-based Auth**: 쿠키 기반 인증
- [ ] **Session Management**: 세션 관리

### 6.2 웹 보안 지식
- [ ] **OWASP Top 10** 보안 취약점
- [ ] **HTTPS/SSL/TLS** 암호화
- [ ] **CORS**: 교차 출처 리소스 공유
- [ ] **Content Security Policy**
- [ ] **XSS/CSRF** 방어

### 6.3 해시 알고리즘
- [ ] **bcrypt**: 비밀번호 해시
- [ ] **scrypt**: 메모리 집약적 해시
- [ ] **SHA Family**: 해시 함수
- [ ] **MD5 사용 금지** 이유

---

## 🧪 7단계: 테스팅 (Testing)

### 7.1 테스트 유형
- [ ] **Unit Testing**: 단위 테스트
- [ ] **Integration Testing**: 통합 테스트
- [ ] **Functional Testing**: 기능 테스트
- [ ] **Performance Testing**: 성능 테스트

### 7.2 테스팅 전략
- [ ] **Test Driven Development (TDD)**
- [ ] **Behavior Driven Development (BDD)**
- [ ] 테스트 커버리지 관리
- [ ] Mock 및 Stub 활용

---

## ⚡ 8단계: 캐싱 (Caching)

### 8.1 캐싱 전략
- [ ] **Client-side Caching**: 클라이언트 캐시
- [ ] **Server-side Caching**: 서버 캐시
- [ ] **CDN**: Content Delivery Network
- [ ] 캐시 무효화 전략

### 8.2 캐싱 도구
- [ ] **Redis**: 인메모리 데이터 구조 저장소
- [ ] **Memcached**: 분산 메모리 캐시
- [ ] **Application-level Caching**

---

## 🌐 9단계: 웹 서버 (Web Servers)

### 9.1 웹 서버 종류
- [ ] **Nginx**: 고성능 웹 서버
- [ ] **Apache**: 전통적인 웹 서버
- [ ] **Caddy**: 자동 HTTPS
- [ ] **MS IIS**: 마이크로소프트 웹 서버

### 9.2 웹 서버 설정
- [ ] 리버스 프록시 설정
- [ ] 로드 밸런싱
- [ ] SSL/TLS 인증서 설정
- [ ] 정적 파일 서빙

---

## 📊 10단계: 확장성 (Scaling)

### 10.1 확장 유형
- [ ] **수직 확장** (Scale Up)
- [ ] **수평 확장** (Scale Out)
- [ ] **데이터베이스 확장**
- [ ] **샤딩 전략**

### 10.2 확장을 위한 설계
- [ ] **Twelve Factor App** 원칙
- [ ] **CAP 정리** 이해
- [ ] **데이터 복제** 전략
- [ ] **장애 대응** 전략

---

## 🔍 11단계: 모니터링 및 관찰 (Monitoring & Observability)

### 11.1 모니터링 개념
- [ ] **Metrics**: 지표 수집
- [ ] **Logging**: 로그 관리
- [ ] **Tracing**: 분산 추적
- [ ] **Instrumentation**: 계측

### 11.2 장애 대응
- [ ] **Circuit Breaker**: 서킷 브레이커 패턴
- [ ] **Graceful Degradation**: 우아한 성능 저하
- [ ] **Throttling**: 요청 제한
- [ ] **Backpressure**: 백프레셔 처리

---

## 📡 12단계: 메시지 브로커 (Message Brokers)

### 12.1 메시지 큐 시스템
- [ ] **RabbitMQ**: AMQP 기반 메시지 브로커
- [ ] **Apache Kafka**: 분산 스트리밍 플랫폼
- [ ] **Redis Pub/Sub**: 발행-구독 패턴

### 12.2 비동기 처리
- [ ] 메시지 패턴 이해
- [ ] 이벤트 기반 아키텍처
- [ ] 마이크로서비스 간 통신

---

## 📐 13단계: 아키텍처 패턴 (Architecture Patterns)

### 13.1 설계 패턴
- [ ] **GOF Design Patterns**: 디자인 패턴
- [ ] **Domain Driven Design (DDD)**: 도메인 주도 설계
- [ ] **CQRS**: 명령 쿼리 분리
- [ ] **Event Sourcing**: 이벤트 소싱

### 13.2 아키텍처 스타일
- [ ] **Monolithic**: 모놀리식 아키텍처
- [ ] **Microservices**: 마이크로서비스
- [ ] **SOA**: 서비스 지향 아키텍처
- [ ] **Serverless**: 서버리스 아키텍처
- [ ] **Service Mesh**: 서비스 메시

---

## 🐳 14단계: 컨테이너화 (Containerization)

### 14.1 컨테이너 기술
- [ ] **Docker**: 컨테이너 플랫폼
- [ ] **LXC**: 리눅스 컨테이너
- [ ] **컨테이너 vs 가상화** 차이점

### 14.2 컨테이너 오케스트레이션
- [ ] **Kubernetes**: 컨테이너 오케스트레이션
- [ ] **Docker Swarm**: 도커 스웜
- [ ] **컨테이너 보안** 고려사항

---

## 🔧 15단계: DevOps 및 CI/CD

### 15.1 지속적 통합/배포
- [ ] **CI/CD** 파이프라인 구축
- [ ] **Jenkins, GitLab CI, GitHub Actions**
- [ ] **Infrastructure as Code (IaC)**
- [ ] **Configuration Management**

### 15.2 클라우드 플랫폼
- [ ] **AWS, Azure, GCP** 기본 서비스
- [ ] **클라우드 네이티브** 개발
- [ ] **마이그레이션 전략**

---

## 🚀 16단계: 검색 엔진 및 고급 기술

### 16.1 검색 엔진
- [ ] **Elasticsearch**: 분산 검색 엔진
- [ ] **Apache Solr**: 검색 플랫폼
- [ ] **전문 검색** 기능 구현

### 16.2 고급 기술
- [ ] **GraphQL** 심화 (Apollo, Relay)
- [ ] **실시간 기술** (WebSockets, Server-Sent Events)
- [ ] **데이터 파이프라인** 구축
- [ ] **기계학습** 백엔드 연동

---

## 🎯 학습 팁 및 권장사항

### 💡 효과적인 학습 방법
1. **프로젝트 중심 학습**: 각 단계마다 실제 프로젝트를 만들어 보세요
2. **문서화 습관**: 학습한 내용을 정리하고 기록하세요
3. **커뮤니티 참여**: 개발자 커뮤니티에 참여하여 질문하고 답변하세요
4. **코드 리뷰**: 다른 개발자의 코드를 보고 피드백을 받으세요

### 🎨 실습 프로젝트 아이디어
- [ ] **1-5단계**: 간단한 블로그 API 만들기
- [ ] **6-10단계**: 사용자 인증이 있는 Todo 앱 API
- [ ] **11-15단계**: 실시간 채팅 애플리케이션
- [ ] **16단계**: 마이크로서비스 기반 e-commerce 플랫폼

### 📚 추가 자료
- **공식 문서**: 각 기술의 공식 문서를 꼭 읽어보세요
- **로드맵 상세 버전**: [roadmap.sh/backend](https://roadmap.sh/backend)
- **온라인 강의**: 각 기술별 온라인 강의를 활용하세요
- **오픈소스 프로젝트**: GitHub에서 관련 프로젝트를 찾아보세요

---

## ✅ 체크리스트 활용법

각 항목 앞의 `[ ]`를 `[x]`로 바꿔가며 학습 진도를 체크하세요.
단계별로 70% 이상 완료하면 다음 단계로 넘어가는 것을 권장합니다.

---