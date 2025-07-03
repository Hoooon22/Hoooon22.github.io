---
layout: default
title: 퐁당 웹 매거진 프로젝트
nav_order: 1
has_children: true
parent: Projects
---

# Project - 퐁당 웹 매거진 프로젝트
{: .no_toc }

## Project has been written since July 1, 2023.
{: .fs-4 .fw-300 }

<br>

퐁당 웹 매거진은 온라인 매거진 플랫폼으로, 다양한 기사와 인터뷰를 웹에서 쉽게 접근할 수 있도록 제작된 프로젝트입니다.

## 프로젝트 개요
{: .fs-5 .fw-500 }

퐁당은 웹 매거진 플랫폼으로, 사용자들에게 큐레이션된 콘텐츠를 제공합니다. 특히 인터뷰 중심의 콘텐츠를 쉽게 접근하고 검색할 수 있는 인터페이스를 제공하여 사용자 경험을 향상시키는 데 중점을 두었습니다.

<img src="../../../../assets/images/pongdang/1_퐁당로고.png" alt="퐁당 매거진 로고">
*퐁당 웹 매거진 로고*

## 주요 기능
{: .fs-5 .fw-500 }

### 1. 반응형 메인 페이지
- 모바일과 데스크톱 모두에서 최적화된 사용자 경험 제공
- 콘텐츠 슬라이더를 통한 주요 기사 하이라이트
- 직관적인 카테고리 내비게이션

<img src="../../../../assets/images/pongdang/screenshot1.png" alt="메인 페이지 레이아웃">
*메인 페이지 레이아웃*

### 2. 고급 검색 기능
- 키워드 기반 콘텐츠 검색
- 타이틀 및 내용 기반 검색 알고리즘
- 검색 결과 실시간 정렬

<img src="../../../../assets/images/pongdang/스크린샷 2023-12-04 오후 8.16.06.png" alt="검색 결과 화면">
*검색 결과 화면*

### 3. 인터뷰 페이지
- 인터뷰 콘텐츠 전용 레이아웃
- 인터뷰이별 카테고리화
- 관련 인터뷰 추천 시스템

### 4. 보안 및 접근성
- 국내 사용자 접근 최적화를 위한 해외 IP 차단
- AWS WAF 활용한 보안 시스템 구축
- 웹 접근성 가이드라인 준수

## 개발 타임라인
{: .fs-5 .fw-500 }

| 시기 | 주요 내용 |
|------|----------|
| 2023년 7월 초 | 프로젝트 시작, 기본 레이아웃 및 CSS 설계 |
| 2023년 7월 중순 | 폰트 적용 및 부트스트랩 라이브러리 통합 |
| 2023년 8월 | 메인페이지 1차 완성, 슬라이드 및 애니메이션 효과 구현 |
| 2023년 10월 | 검색 기능 개발, 검색용 DB 설계 및 구현 |
| 2023년 12월 | 검색 페이지 완성, 라우팅 구현 |
| 2024년 1월 | 보안 강화 - AWS WAF 적용하여 해외 IP 차단 |

## 기술 스택
{: .fs-5 .fw-500 }

- **프론트엔드**: React, CSS, Bootstrap
- **백엔드**: Spring Boot
- **데이터베이스**: MySQL
- **인프라**: AWS EC2, AWS WAF
- **버전 관리**: Git, GitHub

## 주요 도전 과제와 해결책
{: .fs-5 .fw-500 }

1. **반응형 디자인 구현** - 다양한 디바이스 크기에 맞춘 CSS 미디어 쿼리 적용
2. **검색 알고리즘 최적화** - MySQL 쿼리 튜닝을 통한 검색 속도 향상
3. **그라데이션 효과와 클릭 이벤트 충돌** - pointer-events CSS 속성을 활용하여 이미지 위에서의 이벤트 처리 문제 해결
4. **보안 강화** - AWS WAF의 Web ACLs를 활용하여 해외 IP 차단 구현

## Links
{: .fs-4 .fw-300 }

[퐁당 웹 매거진 사이트](https://stoneinwell.com/)

[퐁당 웹 매거진 Instagram](https://www.instagram.com/j.ihoon22/)

[퐁당 웹 매거진 프로젝트 Ver.01 제작 일지](https://congruous-wildebeest-c9e.notion.site/99993255375249b7b058141b0ffbcb13?pvs=4)

[퐁당 웹 매거진 프로젝트 Ver.01 Github(private)](https://github.com/Hoooon22/Pongdang_WebServer)

[퐁당 웹 매거진 프로젝트 Ver.02 제작 일지](https://congruous-wildebeest-c9e.notion.site/Spring-647a8f3c507a42f58cd608bf4c0341bd?pvs=4)

[퐁당 웹 매거진 프로젝트 Ver.02 Github(public)](https://github.com/Hoooon22/Pongdang_Server2)
