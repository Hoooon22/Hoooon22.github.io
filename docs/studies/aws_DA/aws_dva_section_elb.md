---
layout: default
title: AWS ELB (Elastic Load Balancer)
nav_order: 12
parent: AWS (DVA)
grand_parent: Study
date: 2025-07-09 22:42:00
---

# AWS ELB (Elastic Load Balancer) 완전 정복
{: .no_toc }

## 목차
{: .no_toc .text-delta }

1. TOC
{:toc}

## 개요

AWS ELB(Elastic Load Balancer)는 들어오는 애플리케이션 트래픽을 여러 대상(예: EC2 인스턴스, 컨테이너, IP 주소)에 자동으로 분산시키는 서비스입니다. ELB는 애플리케이션의 가용성과 내결함성을 향상시키는 핵심 구성 요소입니다.

## ELB의 주요 기능

### 1. Health Check 기능
- **목적**: 대상 인스턴스의 상태를 지속적으로 모니터링
- **동작 방식**: 
  - 정기적으로 대상에 헬스 체크 요청 전송 (기본 30초 간격)
  - 응답하지 않거나 비정상 응답 시 트래픽 라우팅 중단
  - 정상 상태로 복구되면 다시 트래픽 전달
  - 애플리케이션 계층 헬스 체크 권장 (HTTP/HTTPS)

### 2. Security Group을 통한 보안 설정
- ELB 자체에 보안 그룹 적용 가능 (ALB만 해당)
- 들어오는 트래픽의 IP 출처 제어
- 포트별 접근 제어 설정
- NLB는 클라이언트 IP를 직접 전달하므로 다른 보안 고려사항 존재

### 3. DDoS 보호 기능
- **AWS Shield Standard**: 모든 ELB에 자동 적용
- **계층 3, 4 공격 보호**: SYN/UDP 플러드, 리플렉션 공격 등
- **ALB 추가 보호**: HTTP 계층 7에서 비정상 요청 차단

## ALB (Application Load Balancer)

### 특징
- **HTTP 전용 로드밸런서**
- **HTTP → HTTPS 자동 리다이렉션 기능**
  - HTTP 요청을 HTTPS로 자동 전환
  - 로드밸런서에서 리다이렉션 규칙 설정
  - 백엔드 서버의 부하 감소

### 리다이렉션 동작 과정
1. **클라이언트**: HTTP 요청 전송
2. **ALB**: HTTP → HTTPS 리다이렉션 응답
3. **클라이언트**: HTTPS로 재요청
4. **ALB**: 백엔드 서버로 트래픽 전달

```
Client ──HTTP──> ALB ──Load Balance──> EC2
   ↑              │         (Private IP)
   └──True IP─────┘
```

### 주요 기능
- 경로 기반 라우팅
- 호스트 기반 라우팅
- 웹소켓 지원
- HTTP/2 지원

## Target Group 이란?

### 정의
- **EC2 인스턴스나 다른 AWS 서비스들의 그룹**
- ALB에서 트래픽을 전달받을 대상들의 논리적 그룹

### 구성 요소
- EC2 인스턴스
- IP 주소
- Lambda 함수
- 컨테이너

### 설정 가능한 항목
- 헬스 체크 설정
- 대상 포트 지정
- 프로토콜 설정
- 로드밸런싱 알고리즘

## 애플리케이션 서버는 Client의 IP를 직접 보지 못하고, 진짜 IP는 X-Forwarded-For 헤더에 살아있다

### 문제 상황
- 로드밸런서를 통해 들어오는 요청의 경우
- 애플리케이션 서버는 로드밸런서의 Private IP만 확인 가능
- 실제 클라이언트의 IP 주소를 직접 알 수 없음

### 해결 방법: X-Forwarded-For 헤더
```
X-Forwarded-For: client_ip, proxy1_ip, proxy2_ip
```

- **첫 번째 IP**: 실제 클라이언트 IP
- **이후 IP들**: 프록시 서버들의 IP

### 주의사항
- X-Forwarded-For 헤더는 쉽게 조작 가능
- 보안이 중요한 애플리케이션에서는 추가 검증 필요
- 로드밸런서 설정에서 헤더 처리 방식 확인 필요

## Private IP 즉, 인스턴스 IP의 직접적 접근을 막기위해

### 보안 아키텍처
1. **클라이언트 접근**: 오직 로드밸런서를 통해서만 가능
2. **인스턴스 보호**: Private 서브넷에 배치
3. **직접 접근 차단**: 
   - 보안 그룹 설정으로 로드밸런서에서만 트래픽 허용
   - NACL을 통한 추가 보안 계층

### 장점
- **보안 강화**: 인스턴스 직접 노출 방지
- **중앙 집중식 관리**: 모든 트래픽이 로드밸런서를 경유
- **SSL 터미네이션**: 로드밸런서에서 SSL 처리
- **로깅 및 모니터링**: 중앙화된 접근 로그

## 적절한 ALB의 설정으로 서비스를 한층 더 좋게 배포할 수 있다.

### ALB의 고급 라우팅 기능

#### 1. 경로 기반 라우팅
```
example.com/api/* → API 서버 그룹
example.com/web/* → 웹 서버 그룹
example.com/mobile/* → 모바일 서버 그룹
```

#### 2. 호스트 기반 라우팅
```
api.example.com → API 서버
web.example.com → 웹 서버
admin.example.com → 관리자 서버
```

#### 3. 조건부 라우팅
- HTTP 헤더 기반
- 쿼리 스트링 기반
- HTTP 메서드 기반

### 마이크로서비스 아키텍처 지원
- **서비스별 분리**: 각 서비스를 독립적인 Target Group으로 관리
- **버전 관리**: Blue/Green 배포 지원
- **A/B 테스팅**: 트래픽 가중치 조절을 통한 점진적 배포

## 실제 구현 예시

### 기본 ALB 설정
```yaml
# ALB 리스너 규칙 예시
Rules:
  - Priority: 1
    Conditions:
      - Field: path-pattern
        Values: ["/api/*"]
    Actions:
      - Type: forward
        TargetGroupArn: "api-target-group"
  
  - Priority: 2
    Conditions:
      - Field: host-header
        Values: ["admin.example.com"]
    Actions:
      - Type: forward
        TargetGroupArn: "admin-target-group"
```

### 보안 그룹 설정 예시
```yaml
# ALB 보안 그룹
ALB-SecurityGroup:
  Rules:
    - Protocol: HTTP
      Port: 80
      Source: 0.0.0.0/0
    - Protocol: HTTPS
      Port: 443
      Source: 0.0.0.0/0

# EC2 인스턴스 보안 그룹
Instance-SecurityGroup:
  Rules:
    - Protocol: HTTP
      Port: 80
      Source: ALB-SecurityGroup
```

## 베스트 프랙티스

### 1. 헬스 체크 최적화
- 적절한 간격 설정 (기본 30초, 최소 5초)
- 헬스 체크 경로 최적화 (`/health` 엔드포인트 권장, 가벼운 응답)
- 타임아웃 및 임계값 조정 (Healthy threshold: 2-10, Unhealthy threshold: 2-10)
- 헬스 체크 포트는 트래픽 포트와 동일하게 설정하는 것이 일반적

### 2. 보안 강화
- HTTPS 리다이렉션 활성화
- 적절한 보안 그룹 규칙 설정
- WAF 연동 고려

### 3. 모니터링
- CloudWatch 메트릭 활용 (RequestCount, TargetResponseTime, HTTPCode_Target_2XX_Count 등)
- 접근 로그 활성화 (S3에 저장)
- 주요 메트릭에 대한 CloudWatch 알람 설정

### 4. 성능 최적화
- 적절한 Target Group 크기 유지
- Cross-Zone 로드밸런싱 활성화 (ALB 기본 활성화, NLB는 선택적)
- Connection Draining/Deregistration Delay 설정 (기본 300초)
- Keep-alive 연결 최적화 (백엔드 서버에서 60초 이상 설정 권장)

## ELB 타입별 비교

| 기능 | ALB | NLB | GLB |
|------|-----|-----|-----|
| 프로토콜 | HTTP/HTTPS | TCP/UDP/TLS | IP 프로토콜 |
| 연결 지속성 | 쿠키 기반 | IP 기반 | 튜플 기반 |
| 헬스 체크 | HTTP/HTTPS | TCP/HTTP/HTTPS | TCP/HTTP/HTTPS |
| 대상 유형 | IP, 인스턴스, Lambda | IP, 인스턴스 | IP, 인스턴스 |
| Cross-Zone 로드밸런싱 | 기본 활성화 | 선택적 (비용 발생) | 기본 활성화 |
| 클라이언트 IP 보존 | X-Forwarded-For | 직접 보존 | 직접 보존 |

## 추가 보안 고려사항

### 1. SSL/TLS 설정
- **TLS 1.2 이상 사용**: TLS 1.0/1.1은 비권장
- **Perfect Forward Secrecy (PFS)**: ECDHE 암호 모음 사용
- **HSTS 헤더**: Strict-Transport-Security 헤더 설정
- **SSL 인증서 관리**: AWS Certificate Manager (ACM) 권장

### 2. WAF 연동 (ALB만 해당)
- **SQL 인젝션 방지**: OWASP Top 10 기반 규칙
- **XSS 공격 차단**: 크로스 사이트 스크립팅 방지
- **지역별 차단**: 특정 국가/지역 IP 차단
- **Rate Limiting**: 과도한 요청 제한

## 마무리

AWS ELB는 현대적인 클라우드 애플리케이션의 핵심 구성 요소입니다. 특히 ALB의 고급 라우팅 기능을 활용하면 마이크로서비스 아키텍처와 복잡한 웹 애플리케이션을 효율적으로 관리할 수 있습니다. 

적절한 보안 설정과 모니터링을 통해 안정적이고 확장 가능한 서비스를 구축할 수 있으며, X-Forwarded-For 헤더와 같은 세부사항을 이해하면 더욱 정교한 애플리케이션 개발이 가능합니다.

각 ELB 타입의 특성을 이해하고 용도에 맞는 선택을 하는 것이 중요하며, 보안과 성능 최적화를 위한 지속적인 모니터링과 튜닝이 필요합니다. 