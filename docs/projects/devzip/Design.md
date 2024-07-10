---
layout: default
title: DevZip 디자인 및 메인 설계
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2024-07-03 18:45:37
---

# DevZip 디자인
{: .no_toc }

## 2024.07.03 (TUE)
{: .no_toc .text-delta }

---

> [!info]
> 이 프로젝트는 개인 프로젝트 등을 담는 웹사이트를 제작합니다.

# 2024.07.01
## AWS 계정 생성
AWS를 활용한 서버를 구축하여, 해당 서버에 프로젝트를 이식시킨다.

- 프리티어 계정 생성 완료
- EC2 생성 완료

> 기본적인 세팅은 끝났으며, 구체적인 프로젝트의 디자인을 우선 진행한다.

## 프로젝트 디자인
전반적인 최종 목표들은 제3자가 보았을 때, 
1. 프로젝트가 눈에 잘 보이며
2. 어떤 기능 등이 핵심인지 잘 보여야 하며
3. 버튼 등을 누르면 사이트 또는 기능에 접근할 수 있어야한다. (프로젝트를 시도하기 위한 tmp 프로젝트를 간단히 만들어 테스트 해본다.)


## 2024.07.03
### SpringBoot + React 개발환경 세팅
1. Springboot 프로젝트 생성 및 실행테스트 - Done
2. 리액트 설치
```null
cd src/main
npx create-react-app frontend	# npx create-reeact {프로젝트명}
```
3. 아래 링크 따라 진행 (Springboot, React 연동)

#### title: "Spring Boot + React.js 개발환경 연동하기"

![Spring Boot + React.js](https://velog.velcdn.com/images/u-nij/post/c249f0e8-677b-4734-933f-289247034a2d/spring%20boot%20react.png)

Spring Boot와 React.js를 연동해 개발환경을 만들고, 빌드해서 jar 파일로까지 만들어보는 과정입니다. 자세한 내용은 아래 링크를 클릭하세요:

[Spring Boot + React.js 개발환경 연동하기](https://velog.io/@u-nij/Spring-Boot-React.js-%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD-%EC%84%B8%ED%8C%85)


## 2024.07.06 (토)
### 메인 페이지 연결
- React-router 서드파티 라이브러리를 이용

## 2024.07.08 (월)
### 목표..
- 메인페이지 틀만 완성
- 데이터베이스에 웹페이지 제목, 사이트 링크, 이미지(?) 넣으면 자동으로 불러와 리스트 만들게

1. 풀페이지를 활용하여 메인 페이지 만들기
	- 현재까지 완성한 부분
![](https://i.imgur.com/OZ9p3y8.png)

- 이제 할 것
	- 박스 사이 간격
	- 화면 축소 시, 박스 및 전체 콘텐츠 크기 줄이기?

## 2024.07.09 (화)
### 오늘
- [x] 박스 사이 간격 ✅ 2024-07-09
- [x] 화면 축소 시, 박스 및 전체 콘텐츠 크기 줄이기 ✅ 2024-07-09
- Footer 추가
- 날짜 추가
- 비활성화 시각효과 수정
- 마우스 오버레이 수정
![](https://i.imgur.com/xAokfMU.png)

