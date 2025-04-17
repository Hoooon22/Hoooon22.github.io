---
layout: default
title: 사이드 프로젝트 - DevZip
nav_order: 2
has_children: true
parent: Projects
---

# Project - DeverZip
{: .no_toc }

## Project has been written since July 3, 2024.
{: .fs-4 .fw-300 }

<br>

DevZip은 제가 개발한 프로젝트들의 모음Zip입니다!

## 프로젝트 개요
{: .fs-5 .fw-500 }

DevZip은 개발자를 위한 통합 대시보드 및 커뮤니티 플랫폼입니다. 시스템 모니터링, 로그 분석, 사용자 행동 추적 등 여러 도구를 하나의 대시보드에서 관리할 수 있으며, 개발자들이 지식을 공유하고 소통할 수 있는 커뮤니티 기능을 제공합니다.

<img src="../../../../assets/images/devzip/logdashboard.png" alt="DEV ZIP 대시보드">
*DevZip 로그 대시보드 화면*

## 주요 기능
{: .fs-5 .fw-500 }

### 1. 트레이스보드
웹사이트 분석을 위한 경량화된 솔루션으로, 구글 애널리틱스보다 가볍고 개발자 친화적인 인터페이스를 제공합니다.
- 방문자 지표: 고유 방문자 수, 페이지뷰, 세션 지속 시간, 이탈률 등
- 사용자 행동 차트: 이벤트 유형별, 디바이스별 사용 분포 시각화
- 실시간 이벤트 로그: 사용자 활동을 시간순으로 확인

<img src="../../../../assets/images/devzip/events.png" alt="이벤트 로그 분석">
*실시간 이벤트 로그 화면*

### 2. TrendChat
- Python 스크립트를 이용한 트렌드 데이터 자동 수집
- 수집된 트렌드 정보를 REST API로 제공
- 개발자들이 관심 있는 주제와 기술 트렌드를 한눈에 파악

### 3. API 목록 페이지
- DevZip에서 제공하는 모든 API 엔드포인트를 카테고리별로 정리
- 반응형 디자인과 웹 접근성을 고려한 사용자 친화적 인터페이스
- 직관적인 HTTP 메서드 구분으로 빠른 API 이해 가능

<img src="../../../../assets/images/devzip/apipage.png" alt="API 목록 페이지">
*DevZip API 목록 페이지*

## 개발 타임라인
{: .fs-5 .fw-500 }

| 시기 | 주요 내용 |
|------|----------|
| 2024년 7월 초 | 프로젝트 시작, AWS 환경 구축(EC2, RDS), 도메인 구매(devzip.site), SpringBoot + React 개발환경 설정 |
| 2024년 7월 중순 | 메인 페이지 레이아웃 디자인, 게스트북 기능 구현, 데이터베이스 연동 |
| 2024년 12월 | 대시보드 기본 UI 구현 및 1차 개발 완료 |
| 2025년 2월 | TrendChat 개발: Python 스크립트 자동화로 트렌드 데이터 수집, JSON 파일 저장 시스템 구현 |
| 2025년 4월 | 트레이스보드 개발: 방문자 지표, 사용자 행동 차트, 실시간 이벤트 로그 기능 구현 |
| 2025년 7월 | API 목록 페이지 개발: 반응형 디자인과 접근성 개선 |

## 기술 스택
{: .fs-5 .fw-500 }

- **프론트엔드**: React, Next.js, CSS
- **백엔드**: SpringBoot, Node.js, Express
- **데이터베이스**: MongoDB, MySQL(RDS)
- **인프라**: AWS EC2, AWS RDS, GitHub Actions
- **기타 도구**: Python, pm2

## 주요 도전 과제와 해결책
{: .fs-5 .fw-500 }

1. **IP 주소 수집 이슈** - AWS 로드 밸런서 설정 조정으로 X-Forwarded-For 헤더를 활용해 해결
2. **데이터 수집 자동화** - GitHub Actions와 pm2를 활용한 Python 스크립트 자동화로 해결
3. **배포 프로세스 안정성** - 단일 작업에서 4단계 파이프라인으로 개선하여 에러 추적 용이
4. **사용자 행동 추적 개인정보 보호** - IP 주소 마스킹 처리 등 개인정보 보호 방안 구현

## Links
{: .fs-4 .fw-300 }

- [DevZip 사이트 방문](https://devzip.site)
- [GitHub 저장소](https://github.com/Hoooon22/)