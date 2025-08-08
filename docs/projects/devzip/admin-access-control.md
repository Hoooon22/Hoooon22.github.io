---
title: "DevZip의 보안과 관리자 권한 시스템 설계"
nav_order: 2
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
layout: default
---

# DevZip 프로젝트의 보안: 관리자 권한 및 접근 제어 시스템

## 개요

DevZip 프로젝트에서는 애플리케이션의 보안을 최우선으로 고려하여 세밀하고 안전한 사용자 권한 및 접근 제어 시스템을 구현했습니다. 이 글에서는 구현된 주요 보안 메커니즘과 설계 철학을 소개합니다.

## 사용자 역할 기반 인증 시스템

### 역할 구분
- **일반 사용자 (USER)**: 기본 서비스 이용 권한
- **관리자 (ADMIN)**: 시스템 전체 관리 및 특별한 접근 권한

### 주요 특징
- 공개 사용자 등록 시 기본적으로 `USER` 권한 부여
- 관리자 계정은 오직 `/api/auth/admin/create-user` 엔드포인트를 통해서만 생성 가능
- JWT 토큰에 역할 정보 포함
- 프론트엔드 컴포넌트에서 사용자 권한에 따른 접근 제어

## 안전한 관리자 계정 자동 생성 시스템

### 환경 변수 기반 구성
- `APP_ADMIN_USERNAME`: 관리자 계정명 (기본값: admin)
- `APP_ADMIN_PASSWORD`: 관리자 비밀번호 (지정하지 않으면 자동 생성)
- `APP_ADMIN_EMAIL`: 관리자 이메일 (기본값: admin@devzip.cloud)
- `APP_ADMIN_AUTO_CREATE`: 자동 생성 활성화 여부 (기본값: true)

### 보안 기능
- 환경 변수 미설정 시 안전한 임시 비밀번호 자동 생성
- 중복 관리자 계정 생성 방지
- Docker Compose 환경 변수와의 원활한 통합

## CORS 및 인증 보안 개선

### CORS 구성
- 와일드카드 대신 `allowedOriginPatterns` 사용
- 로컬호스트 및 프로덕션 도메인에 대한 세분화된 패턴 지원
- 자격 증명(Credentials) 지원을 위한 설정

### 보안 이점
- 악의적인 도메인의 요청 차단
- 도메인별 세분화된 접근 제어
- 보안 취약점 최소화

## 구현 예시

### 사용자 역할 확인 미들웨어 (예시 코드)

```typescript
function checkAdminRole(req, res, next) {
  const userRole = req.user.role;
  
  if (userRole !== 'ADMIN') {
    return res.status(403).json({ 
      message: '접근 권한이 없습니다.' 
    });
  }
  
  next();
}

// 관리자 전용 라우트
router.post('/admin/create-user', 
  authenticateJWT, 
  checkAdminRole, 
  createAdminUserHandler
);
```

## 결론

DevZip 프로젝트의 보안 시스템은 다음과 같은 원칙을 따릅니다:
- 최소 권한의 원칙
- 안전한 기본값 제공
- 세분화된 접근 제어
- 투명하고 감사 가능한 인증 메커니즘

지속적인 보안 개선을 통해 사용자 데이터와 시스템을 보호합니다.