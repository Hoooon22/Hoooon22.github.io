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

## 2024.07.10 (수)
### 새로운 목표?
- 처음 프로젝트로 게시판 프로젝트
	- 그런데, 게시판 + @ 느낌으로
	- 전송한 ip의 앞부분을 잘라 표시?

- 그 전에, AWS에 심어볼까
	- AWS으로 프로젝트 Clone 완료
	- npm install 후, npm start 테스트 - 완료
	- 스프링 부트 빌드 중 -> 시간 오래 걸림

## 2024.07.11 (목)
### 오늘은?
1. AWS에서 스프링 부트 빌드 확인 및 8080 접속 확인
	- 확인 완료
2. 게시판 만들기

## 2024.07.12 (금)
### 게시판 제작
- 페이지 Guestbook.js 생성
- 페이지 디자인 완료

- 프록시서버를 활성화 해야, 클라이언트의 IP를 가져올 수 있음

- 도메인 구매: https://my.freenom.com/clientarea.php?action=domaindetails
	- devzip.site
- 로드밸런서 문제 해결
	- 대상 그룹을 8080포트를 오픈
![](https://i.imgur.com/6AEFcqf.png)

- devzip.site에 접속 가능!!!

#### 프록시 서버 설정 확인

프록시 서버에서 X-Forwarded-For 헤더를 올바르게 전달하고 있는지 확인해야 합니다. 특히 AWS Elastic Load Balancer (ELB)를 사용할 경우, 다음과 같은 설정을 확인합니다:

- **Load Balancer 설정**: AWS 콘솔에서 사용 중인 ELB의 설정을 확인합니다. 다음과 같은 단계를 따라 확인할 수 있습니다:
    - AWS Management Console에 로그인합니다.
    - EC2 대시보드로 이동하고, "Load Balancers"를 클릭합니다.
    - 사용 중인 ELB를 선택하고, "Listeners" 탭을 클릭합니다.
    - 사용하는 프로토콜(일반적으로 HTTP 또는 HTTPS)에 따라서 "Add"를 클릭하여 X-Forwarded-For을 선택하고 "Update"를 클릭하여 적용합니다.

-> or
```embed
title: "Fetching"
image: "data:image/svg+xml;base64,PHN2ZyBjbGFzcz0ibGRzLW1pY3Jvc29mdCIgd2lkdGg9IjgwcHgiICBoZWlnaHQ9IjgwcHgiICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxMDAgMTAwIiBwcmVzZXJ2ZUFzcGVjdFJhdGlvPSJ4TWlkWU1pZCI+PGcgdHJhbnNmb3JtPSJyb3RhdGUoMCkiPjxjaXJjbGUgY3g9IjgxLjczNDEzMzYxMTY0OTQxIiBjeT0iNzQuMzUwNDU3MTYwMzQ4ODIiIGZpbGw9IiNlMTViNjQiIHI9IjUiIHRyYW5zZm9ybT0icm90YXRlKDM0MC4wMDEgNDkuOTk5OSA1MCkiPgogIDxhbmltYXRlVHJhbnNmb3JtIGF0dHJpYnV0ZU5hbWU9InRyYW5zZm9ybSIgdHlwZT0icm90YXRlIiBjYWxjTW9kZT0ic3BsaW5lIiB2YWx1ZXM9IjAgNTAgNTA7MzYwIDUwIDUwIiB0aW1lcz0iMDsxIiBrZXlTcGxpbmVzPSIwLjUgMCAwLjUgMSIgcmVwZWF0Q291bnQ9ImluZGVmaW5pdGUiIGR1cj0iMS41cyIgYmVnaW49IjBzIj48L2FuaW1hdGVUcmFuc2Zvcm0+CjwvY2lyY2xlPjxjaXJjbGUgY3g9Ijc0LjM1MDQ1NzE2MDM0ODgyIiBjeT0iODEuNzM0MTMzNjExNjQ5NDEiIGZpbGw9IiNmNDdlNjAiIHI9IjUiIHRyYW5zZm9ybT0icm90YXRlKDM0OC4zNTIgNTAuMDAwMSA1MC4wMDAxKSI+CiAgPGFuaW1hdGVUcmFuc2Zvcm0gYXR0cmlidXRlTmFtZT0idHJhbnNmb3JtIiB0eXBlPSJyb3RhdGUiIGNhbGNNb2RlPSJzcGxpbmUiIHZhbHVlcz0iMCA1MCA1MDszNjAgNTAgNTAiIHRpbWVzPSIwOzEiIGtleVNwbGluZXM9IjAuNSAwIDAuNSAxIiByZXBlYXRDb3VudD0iaW5kZWZpbml0ZSIgZHVyPSIxLjVzIiBiZWdpbj0iLTAuMDYyNXMiPjwvYW5pbWF0ZVRyYW5zZm9ybT4KPC9jaXJjbGU+PGNpcmNsZSBjeD0iNjUuMzA3MzM3Mjk0NjAzNiIgY3k9Ijg2Ljk1NTE4MTMwMDQ1MTQ3IiBmaWxsPSIjZjhiMjZhIiByPSI1IiB0cmFuc2Zvcm09InJvdGF0ZSgzNTQuMjM2IDUwIDUwKSI+CiAgPGFuaW1hdGVUcmFuc2Zvcm0gYXR0cmlidXRlTmFtZT0idHJhbnNmb3JtIiB0eXBlPSJyb3RhdGUiIGNhbGNNb2RlPSJzcGxpbmUiIHZhbHVlcz0iMCA1MCA1MDszNjAgNTAgNTAiIHRpbWVzPSIwOzEiIGtleVNwbGluZXM9IjAuNSAwIDAuNSAxIiByZXBlYXRDb3VudD0iaW5kZWZpbml0ZSIgZHVyPSIxLjVzIiBiZWdpbj0iLTAuMTI1cyI+PC9hbmltYXRlVHJhbnNmb3JtPgo8L2NpcmNsZT48Y2lyY2xlIGN4PSI1NS4yMjEwNDc2ODg4MDIwNyIgY3k9Ijg5LjY1Nzc5NDQ1NDk1MjQxIiBmaWxsPSIjYWJiZDgxIiByPSI1IiB0cmFuc2Zvcm09InJvdGF0ZSgzNTcuOTU4IDUwLjAwMDIgNTAuMDAwMikiPgogIDxhbmltYXRlVHJhbnNmb3JtIGF0dHJpYnV0ZU5hbWU9InRyYW5zZm9ybSIgdHlwZT0icm90YXRlIiBjYWxjTW9kZT0ic3BsaW5lIiB2YWx1ZXM9IjAgNTAgNTA7MzYwIDUwIDUwIiB0aW1lcz0iMDsxIiBrZXlTcGxpbmVzPSIwLjUgMCAwLjUgMSIgcmVwZWF0Q291bnQ9ImluZGVmaW5pdGUiIGR1cj0iMS41cyIgYmVnaW49Ii0wLjE4NzVzIj48L2FuaW1hdGVUcmFuc2Zvcm0+CjwvY2lyY2xlPjxjaXJjbGUgY3g9IjQ0Ljc3ODk1MjMxMTE5NzkzIiBjeT0iODkuNjU3Nzk0NDU0OTUyNDEiIGZpbGw9IiM4NDliODciIHI9IjUiIHRyYW5zZm9ybT0icm90YXRlKDM1OS43NiA1MC4wMDY0IDUwLjAwNjQpIj4KICA8YW5pbWF0ZVRyYW5zZm9ybSBhdHRyaWJ1dGVOYW1lPSJ0cmFuc2Zvcm0iIHR5cGU9InJvdGF0ZSIgY2FsY01vZGU9InNwbGluZSIgdmFsdWVzPSIwIDUwIDUwOzM2MCA1MCA1MCIgdGltZXM9IjA7MSIga2V5U3BsaW5lcz0iMC41IDAgMC41IDEiIHJlcGVhdENvdW50PSJpbmRlZmluaXRlIiBkdXI9IjEuNXMiIGJlZ2luPSItMC4yNXMiPjwvYW5pbWF0ZVRyYW5zZm9ybT4KPC9jaXJjbGU+PGNpcmNsZSBjeD0iMzQuNjkyNjYyNzA1Mzk2NDE1IiBjeT0iODYuOTU1MTgxMzAwNDUxNDciIGZpbGw9IiNlMTViNjQiIHI9IjUiIHRyYW5zZm9ybT0icm90YXRlKDAuMTgzNTUyIDUwIDUwKSI+CiAgPGFuaW1hdGVUcmFuc2Zvcm0gYXR0cmlidXRlTmFtZT0idHJhbnNmb3JtIiB0eXBlPSJyb3RhdGUiIGNhbGNNb2RlPSJzcGxpbmUiIHZhbHVlcz0iMCA1MCA1MDszNjAgNTAgNTAiIHRpbWVzPSIwOzEiIGtleVNwbGluZXM9IjAuNSAwIDAuNSAxIiByZXBlYXRDb3VudD0iaW5kZWZpbml0ZSIgZHVyPSIxLjVzIiBiZWdpbj0iLTAuMzEyNXMiPjwvYW5pbWF0ZVRyYW5zZm9ybT4KPC9jaXJjbGU+PGNpcmNsZSBjeD0iMjUuNjQ5NTQyODM5NjUxMTc2IiBjeT0iODEuNzM0MTMzNjExNjQ5NDEiIGZpbGw9IiNmNDdlNjAiIHI9IjUiIHRyYW5zZm9ybT0icm90YXRlKDEuODY0NTcgNTAgNTApIj4KICA8YW5pbWF0ZVRyYW5zZm9ybSBhdHRyaWJ1dGVOYW1lPSJ0cmFuc2Zvcm0iIHR5cGU9InJvdGF0ZSIgY2FsY01vZGU9InNwbGluZSIgdmFsdWVzPSIwIDUwIDUwOzM2MCA1MCA1MCIgdGltZXM9IjA7MSIga2V5U3BsaW5lcz0iMC41IDAgMC41IDEiIHJlcGVhdENvdW50PSJpbmRlZmluaXRlIiBkdXI9IjEuNXMiIGJlZ2luPSItMC4zNzVzIj48L2FuaW1hdGVUcmFuc2Zvcm0+CjwvY2lyY2xlPjxjaXJjbGUgY3g9IjE4LjI2NTg2NjM4ODM1MDYiIGN5PSI3NC4zNTA0NTcxNjAzNDg4NCIgZmlsbD0iI2Y4YjI2YSIgcj0iNSIgdHJhbnNmb3JtPSJyb3RhdGUoNS40NTEyNiA1MCA1MCkiPgogIDxhbmltYXRlVHJhbnNmb3JtIGF0dHJpYnV0ZU5hbWU9InRyYW5zZm9ybSIgdHlwZT0icm90YXRlIiBjYWxjTW9kZT0ic3BsaW5lIiB2YWx1ZXM9IjAgNTAgNTA7MzYwIDUwIDUwIiB0aW1lcz0iMDsxIiBrZXlTcGxpbmVzPSIwLjUgMCAwLjUgMSIgcmVwZWF0Q291bnQ9ImluZGVmaW5pdGUiIGR1cj0iMS41cyIgYmVnaW49Ii0wLjQzNzVzIj48L2FuaW1hdGVUcmFuc2Zvcm0+CjwvY2lyY2xlPjxhbmltYXRlVHJhbnNmb3JtIGF0dHJpYnV0ZU5hbWU9InRyYW5zZm9ybSIgdHlwZT0icm90YXRlIiBjYWxjTW9kZT0ic3BsaW5lIiB2YWx1ZXM9IjAgNTAgNTA7MCA1MCA1MCIgdGltZXM9IjA7MSIga2V5U3BsaW5lcz0iMC41IDAgMC41IDEiIHJlcGVhdENvdW50PSJpbmRlZmluaXRlIiBkdXI9IjEuNXMiPjwvYW5pbWF0ZVRyYW5zZm9ybT48L2c+PC9zdmc+"
description: "Fetching https://repost.aws/ko/knowledge-center/elb-capture-client-ip-addresses"
url: "https://repost.aws/ko/knowledge-center/elb-capture-client-ip-addresses"
```

### Guestbook.js
구글 검색 후, 처음부터 다시 개발