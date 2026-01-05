---
layout: default
title: Command Stack - 개발자를 위한 터미널 스타일 스케줄러
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2026-01-05 16:00:00
---

# Command Stack - 개발자를 위한 터미널 스타일 스케줄러
{: .no_toc }

## 2025.01.05 (SUN)
{: .no_toc .text-delta }

---

## 들어가며

개발자의 하루는 수많은 작업의 연속이다. 기능 구현, 버그 수정, 코드 리뷰, 문서 작성까지. 하지만 기존의 할 일 관리 앱들은 개발자의 사고방식과 맞지 않는 경우가 많다. 우리는 터미널에서 명령어를 실행하고, 프로세스 상태를 확인하며, 작업을 Context 단위로 전환하는 데 익숙하다.

그래서 **Command Stack**을 만들게 되었다. "Control your life's runtime with a project-based, developer-centric scheduler"라는 슬로건처럼, 개발자에게 친숙한 OS와 터미널 메타포를 활용한 프로젝트 기반 스케줄러다.

## 프로젝트 개요

Command Stack은 개발자의 사고방식을 그대로 반영한 개인 관리 시스템이다. 할 일을 '명령어(Command)'로, 프로젝트를 'Context'로 표현하며, Unix 스타일의 상태 시스템을 사용한다.

일반적인 투두 리스트가 아닌, 마치 작업 관리자(Task Manager)에서 프로세스를 관리하듯이 나의 작업들을 제어할 수 있다. 각 작업은 실행 중(EXECUTING), 성공(EXIT_SUCCESS), 중단(SIGKILL) 등의 상태를 가지며, Context별로 그룹화되어 관리된다.

## 주요 기능

### 터미널 중심 작업 관리

Command Stack의 핵심은 개발자에게 친숙한 터미널 메타포다. 각 작업은 '명령어(Command)'로 표현되며, Unix 스타일의 상태 시스템을 사용한다.

- **EXECUTING**: 현재 진행 중인 작업
- **EXIT_SUCCESS**: 성공적으로 완료된 작업
- **SIGKILL**: 중단되거나 취소된 작업

이런 상태 표현은 개발자에게 직관적이며, 작업의 생명주기를 명확하게 파악할 수 있게 해준다.

### Console 명령어 인터페이스

GUI 폼 대신 터미널처럼 명령어를 입력해서 작업을 관리할 수 있다. 브라우저의 개발자 도구 Console을 열고 명령어를 입력하면 즉시 일정이 추가되거나 수정된다.

```javascript
// 새로운 작업 추가
addCommand({
  title: "API 문서 작성",
  context: "backend-api",
  deadline: "2025-01-10",
  type: "documentation"
});

// 작업 상태 변경
updateCommand("cmd-123", { status: "EXIT_SUCCESS" });

// Context별 작업 조회
listCommands("backend-api");

// 오늘의 작업 목록
getTodayCommands();
```

마우스 클릭 없이 키보드만으로 빠르게 작업을 추가하고 관리할 수 있다. 반복적인 작업을 스크립트로 자동화하거나, 외부 도구와 연동하여 작업을 자동으로 생성하는 것도 가능하다.

### Context 기반 작업 분류

모든 Command는 Context로 그룹화된다. Context는 프로젝트, 업무 영역, 또는 관심사별로 작업을 묶는 단위다. 예를 들어:

- `backend-api`: 백엔드 API 개발 관련 작업
- `devops`: 배포 및 인프라 관련 작업
- `personal`: 개인 공부 및 사이드 프로젝트

Context 전환을 통해 현재 집중하고 있는 영역의 작업만 모아볼 수 있으며, 마치 터미널에서 디렉토리를 이동하듯 자연스럽게 작업 영역을 전환할 수 있다.

### 이중 스케줄 뷰

Command Stack은 두 가지 방식으로 작업을 시각화한다.

**캘린더 그리드 뷰**는 마감일을 중심으로 작업을 배치한다. 각 날짜에 어떤 작업이 예정되어 있는지 한눈에 파악할 수 있으며, 데드라인이 다가오는 작업을 놓치지 않게 해준다.

**타임라인 뷰**는 주/월/년 단위로 작업의 흐름을 보여준다. 장기 프로젝트의 진행 상황을 파악하거나, 특정 기간 동안 완료한 작업을 확인할 때 유용하다.

### 간편한 Command 생성

새로운 작업을 추가하는 것은 폼 기반 인터페이스를 통해 간단하다. 작업 내용, 마감일, Context, 타입을 선택하면 즉시 Command Stack에 추가되며, 선택한 뷰에 자동으로 반영된다.

## 실전 활용 예시

### 프로젝트별 작업 관리

새로운 프로젝트를 시작할 때 먼저 Context를 생성한다. 예를 들어 `e-commerce` Context를 만들고, 다음과 같은 Command들을 추가할 수 있다:

- `상품 목록 API 구현` - EXECUTING
- `결제 모듈 통합` - 마감일: 2025-01-15
- `배포 스크립트 작성` - 마감일: 2025-01-20

각 작업의 상태를 업데이트하면서 프로젝트 진행 상황을 한눈에 파악할 수 있다.

### 일일 스프린트 계획

매일 아침 캘린더 뷰를 확인하여 오늘 해야 할 작업들을 점검한다. EXECUTING 상태인 작업들을 우선적으로 처리하고, 완료되면 EXIT_SUCCESS로 변경한다.

타임라인 뷰로 전환하여 이번 주에 완료해야 할 작업들을 확인하고, 우선순위를 조정할 수 있다.

### Console을 활용한 빠른 작업 추가

아침 스탠드업 미팅이 끝나고 오늘 해야 할 작업이 정해졌다면, 브라우저 Console을 열고 한 줄씩 명령어를 입력한다:

```javascript
addCommand({ title: "유저 인증 버그 수정", context: "backend", deadline: "today", type: "bugfix" });
addCommand({ title: "PR 리뷰 - #342", context: "code-review", deadline: "today", type: "review" });
addCommand({ title: "성능 테스트 보고서 작성", context: "testing", deadline: "2025-01-08", type: "documentation" });
```

GUI를 클릭하는 것보다 훨씬 빠르게 여러 작업을 일괄 추가할 수 있다.

### 스크립트를 활용한 반복 작업 자동화

매주 월요일마다 주간 회의가 있다면, 스크립트로 자동화할 수 있다:

```javascript
// 다음 월요일 날짜 계산
const nextMonday = getNextMonday();

// 주간 회의 작업 자동 생성
addCommand({
  title: "주간 스프린트 미팅 참석",
  context: "meetings",
  deadline: nextMonday,
  type: "meeting"
});

// 회의 전 준비 작업도 함께 생성
addCommand({
  title: "스프린트 진행상황 정리",
  context: "meetings",
  deadline: getPreviousDay(nextMonday),
  type: "preparation"
});
```

## 기술 스택

Command Stack은 모던한 웹 기술 스택으로 구성되어 있다.

**Frontend**
- React 18 with Vite - 빠른 개발 환경과 최적화된 빌드
- TypeScript - 타입 안정성과 개발 생산성
- Tailwind CSS - 유틸리티 우선 스타일링

**Backend**
- Spring Boot 3.x - 안정적인 Java 기반 서버
- Java 17+ - 최신 Java 기능 활용
- Gradle - 의존성 관리 및 빌드 자동화

전체 코드베이스는 TypeScript가 71%로 가장 많은 비중을 차지하며, Java가 16.5%를 담당한다.

## 시작하기

### macOS 앱 빌드

macOS에서 네이티브 앱으로 사용하려면 로컬에서 빌드해야 한다:

```bash
./build.sh
```

빌드 스크립트가 자동으로 프론트엔드와 백엔드를 빌드하고, macOS 앱으로 패키징한다.

### 플랫폼별 설치

GitHub Releases 페이지에서 플랫폼별 인스톨러를 다운로드할 수 있다:

- macOS: `.dmg` 파일
- Windows: `.exe` 파일
- Linux: `.AppImage` 또는 `.deb` 파일

### 개발 환경 실행

소스 코드를 직접 실행하려면:

**Backend 실행:**
```bash
cd backend
./gradlew bootRun
```

**Frontend 실행:**
```bash
cd frontend
npm install
npm run dev
```

## 마무리

Command Stack은 개발자의 사고방식을 그대로 반영한 작업 관리 도구다. 터미널에서 명령어를 실행하듯 작업을 관리하고, Context를 전환하며 집중력을 유지할 수 있다.

Unix 스타일의 상태 시스템과 이중 스케줄 뷰를 통해 프로젝트 진행 상황을 명확하게 파악할 수 있으며, Console 명령어 인터페이스로 키보드만으로 빠르게 작업을 추가하고 관리할 수 있다.

앞으로 CLI 인터페이스 추가, 단축키 시스템 강화, Git 통합 등 개발자를 위한 더 많은 기능을 추가할 예정이다.

## Links

- [Command Stack GitHub 저장소](https://github.com/Hoooon22/Command_Stack)
- [데모 사이트](https://devzip.cloud/commandstack)
