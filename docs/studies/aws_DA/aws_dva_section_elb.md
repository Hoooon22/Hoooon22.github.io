---
layout: default
title: AWS ALB (Application Load Balancer) 학습 정리
nav_order: 12
parent: AWS (DVA)
grand_parent: Study
date: 2025-07-09 22:42:00
---

# AWS ALB (Application Load Balancer) 학습 정리
{: .no_toc }

## 목차
{: .no_toc .text-delta }

1. TOC
{:toc}

## 개요

오늘 학습한 AWS ALB(Application Load Balancer)의 핵심 개념들을 정리했습니다. ALB는 HTTP/HTTPS 트래픽을 여러 EC2 인스턴스에 분산시키는 로드밸런서입니다.

## 1. Health Check 기능

### 동작 방식
- ALB가 EC2 인스턴스들의 상태를 지속적으로 확인
- 정상적인 인스턴스에만 트래픽을 전달
- 문제가 있는 인스턴스는 자동으로 트래픽에서 제외

## 2. Security Group을 통한 보안 설정

- ALB 자체에 보안 그룹을 적용할 수 있음
- 들어오는 트래픽의 소스를 제어
- 특정 포트와 프로토콜만 허용

## 3. ALB는 HTTP 전용 로드밸런서

### HTTP → HTTPS 자동 리다이렉션 기능
- HTTP로 들어온 요청을 HTTPS로 자동 전환
- ALB에서 리다이렉션 규칙을 설정
- 백엔드 서버의 부하를 줄일 수 있음

### 동작 흐름
```
Client ──HTTP──> ALB ──Load Balance──> EC2
   ↑              │         (Private IP)
   └──True IP─────┘
```

1. 클라이언트가 HTTP로 요청
2. ALB가 HTTPS로 리다이렉션 응답
3. 클라이언트가 HTTPS로 재요청
4. ALB가 백엔드 EC2로 트래픽 전달

## 4. Target Group 이란?

### 정의
- EC2 인스턴스나 다른 AWS 서비스들의 그룹
- ALB에서 트래픽을 전달받을 대상들의 논리적 그룹

### 주요 개념
- 로드밸런서가 트래픽을 분산시킬 대상들을 묶어서 관리
- 각 Target Group마다 별도의 헬스 체크 설정 가능

## 5. 애플리케이션 서버는 Client의 진짜 IP를 직접 볼 수 없다

### 문제 상황
- 로드밸런서를 통해 들어오는 요청의 경우
- 애플리케이션 서버는 로드밸런서의 Private IP만 확인 가능
- 실제 클라이언트의 IP 주소를 직접 알 수 없음

### 해결: X-Forwarded-For 헤더
- 진짜 클라이언트 IP는 **X-Forwarded-For 헤더**에 들어있음
- 애플리케이션에서 이 헤더를 읽어서 실제 클라이언트 IP를 확인해야 함

```
X-Forwarded-For: 실제클라이언트IP
```

## 6. Private IP로의 직접 접근 차단

### 보안 설정
- 클라이언트는 오직 로드밸런서를 통해서만 접근 가능
- EC2 인스턴스의 보안 그룹에서 ALB에서 오는 트래픽만 허용
- 외부에서 인스턴스로 직접 접근하는 것을 차단

### 이점
- 보안 강화: 인스턴스가 직접 노출되지 않음
- 중앙 집중식 관리: 모든 트래픽이 로드밸런서를 경유

## 7. ALB를 적절히 설정하면 서비스 배포를 더 좋게 할 수 있다

### 핵심 아이디어
- ALB의 라우팅 기능을 활용하면 다양한 서비스를 효율적으로 배포 가능
- 하나의 로드밸런서로 여러 서비스를 관리할 수 있음

## 학습 요약

오늘 ALB에 대해 학습한 핵심 내용들:

1. **Health Check**: 인스턴스 상태를 자동으로 모니터링
2. **Security Group**: ALB 자체에 보안 그룹 적용 가능
3. **HTTP 전용**: HTTP/HTTPS 트래픽만 처리하는 로드밸런서
4. **Target Group**: 트래픽을 받을 대상들의 논리적 그룹
5. **X-Forwarded-For**: 실제 클라이언트 IP를 확인하는 방법
6. **보안 강화**: Private IP 직접 접근 차단
7. **고급 배포**: ALB 설정으로 효율적인 서비스 배포 가능

ALB는 HTTP/HTTPS 애플리케이션의 로드밸런싱에 특화된 서비스로, 다양한 보안 기능과 라우팅 기능을 제공합니다. 