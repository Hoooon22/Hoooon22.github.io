---
layout: default
title: Conflux - 개인화된 통합 알림 관제 센터
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2025-12-28 16:00:00
---

# Conflux - 개인화된 통합 알림 관제 센터
{: .no_toc }

## 2025.12.28 (SAT)
{: .no_toc .text-delta }

---

## 들어가며

개발하다 보면 하루에도 수십 번씩 여러 도구들의 알림을 확인하게 된다. GitHub의 PR 알림, Jira의 티켓 업데이트, Sentry의 에러 알림, Slack 메시지까지. 브라우저 탭을 하나씩 열어가며 확인하다 보면 집중력이 흐트러지고, 정작 중요한 알림을 놓치기도 한다.

이런 문제를 해결하기 위해 **Conflux**를 만들게 되었다. Conflux는 흩어진 개발 도구의 알림을 하나의 타임라인으로 통합하는 개인화된 관제 센터다.

## 프로젝트 개요

Conflux는 "Where all streams merge"라는 슬로건처럼 여러 알림 스트림을 하나로 합치는 것을 목표로 한다. 단순한 알림함을 넘어서, Private 서버의 상태를 감시하고 배치 작업 결과를 수신하는 나만의 관제 탑 역할을 한다.

현재 Beta 버전으로 개발이 진행 중이며, 데스크톱 앱과 웹 버전 모두 지원한다.

## 주요 기능

### 통합 인박스

더 이상 브라우저 탭을 헤매지 않아도 된다. GitHub의 PR이나 Push 알림, Jira의 티켓 업데이트, Slack 메시지, Sentry의 에러 로그까지 모든 알림이 한곳에 모인다.

특히 Focus View 기능을 통해 '빌드 성공' 같은 일상적인 소음은 필터링하고, 나에게 멘션된 메시지나 Critical Error 같은 중요한 알림만 모아볼 수 있다.

### 보안 능동 감시

내가 운영하는 API 서버가 정상적으로 동작하는지 Conflux가 대신 감시한다. 등록한 API 엔드포인트를 1분마다 체크하여 상태를 모니터링하며, 서버가 응답하지 않거나 5xx 에러를 반환하는 순간 즉시 데스크톱 알림을 보낸다.

단순한 URL 호출뿐만 아니라 Authorization Header나 API Token이 필요한 Private 서버도 안전하게 설정하여 감시할 수 있다. 예를 들어 내부 Admin API처럼 인증이 필요한 엔드포인트도 Bearer Token을 설정해두면 지속적으로 헬스 체크가 가능하다.

### 크로스 플랫폼 지원

macOS와 Windows의 시스템 트레이에 상주하는 데스크톱 앱을 제공하며, 네이티브 알림으로 실시간 업데이트를 받을 수 있다. 만약 설치가 불가능한 환경이라면 브라우저만 있으면 웹 대시보드를 통해 동일한 기능을 사용할 수 있다.

## 실전 활용 예시

### 배치 작업 알림

파이썬 스크립트나 배치 작업이 끝났을 때 간단한 curl 명령으로 내 PC로 알림을 보낼 수 있다.

```bash
curl -X POST http://localhost:8080/api/webhook/custom \
  -H "Content-Type: application/json" \
  -d '{
    "title": "데이터 백업 완료",
    "message": "총 50GB 백업 성공. 소요시간: 120s",
    "status": "success"
  }'
```

이렇게 하면 장시간 걸리는 작업을 실행해두고 다른 일을 하다가도, 작업이 완료되면 바로 알림을 받을 수 있다.

### Private API 감시

보안 토큰이 필요한 내부 서버를 감시하려면 설정 메뉴에서 다음과 같이 입력한다:

- Target URL: `https://api.my-service.com/health`
- Method: `GET`
- Headers: `Authorization: Bearer my-secret-token`
- Interval: `60s`

이렇게 설정해두면 1분마다 자동으로 Health Check를 수행하고, 문제가 발생하면 즉시 알려준다.

## 기술 스택

Conflux는 현대적이고 안정적인 기술 스택으로 구성되어 있다.

- Backend: Spring Boot 3.4
- Frontend: React 18
- Desktop: Electron
- Design: Linear-style Dark Mode UI

Spring Boot로 안정적인 백엔드 API 서버를 구축하고, React로 반응형 UI를 만들었다. 그리고 Electron을 통해 데스크톱 앱으로 패키징하여 네이티브 알림 기능을 제공한다.

## 시작하기

현재는 소스 코드를 통해 직접 실행할 수 있다. 먼저 백엔드를 실행한다:

```bash
cd conflux-backend
./gradlew bootRun
```

그 다음 데스크톱 앱을 실행하거나:

```bash
cd conflux-client
npm run electron
```

웹 버전으로 실행할 수 있다:

```bash
cd conflux-client
npm start
```

로컬에서 외부 웹훅을 받으려면 ngrok을 사용하면 된다.

## 마무리

Conflux는 개발자의 집중력을 지키고 중요한 알림을 놓치지 않게 도와주는 개인 관제 센터다. 아직 Beta 버전이지만, 기본적인 통합 알림과 헬스 체크 기능은 모두 동작한다.

앞으로 더 많은 서비스 통합과 사용자 정의 필터링 규칙 등을 추가할 계획이다.

## Links

- [Conflux GitHub 저장소](https://github.com/Hoooon22/conflux)
- [데모 사이트](https://devzip.cloud/conflux)
