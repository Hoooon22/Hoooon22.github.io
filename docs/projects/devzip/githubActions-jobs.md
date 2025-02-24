---
layout: default
title: GitHub Actions로 4단계 배포 파이프라인 구성하기
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2025-02-24 22:16:17
---

# 🚀 GitHub Actions로 4단계 배포 파이프라인 구성하기

이번 글에서는 **GitHub Actions**를 사용하여 배포 과정을 **네 단계로 나누어 관리**하는 방법을 리뷰합니다.

## ✅ **목표**  
기존에는 배포 프로세스가 **하나의 Job**으로 구성되어 **에러 발생 시 원인 파악이 어려웠습니다.**  
👉 이를 해결하기 위해 **4단계로 분리하여 배포 파이프라인**을 구축했습니다.

---

## 🛠️ **배포 파이프라인 구조**

전체 배포 과정은 아래처럼 **4단계(Job)**로 나누어 구성했습니다.

1. **📝 Checkout Code**  
   - 코드 레포지토리에서 소스 코드 가져오기  
2. **🛑 Stop Existing Services**  
   - 기존 실행 중인 서버 및 프로세스 중지  
3. **🏗️ Clean & Build Project**  
   - 빌드 폴더 정리 및 프로젝트 빌드 수행  
4. **🚀 Deploy & Restart Services**  
   - 빌드된 코드 배포 및 PM2 서비스 재시작  

---

## 🎯 **배포 과정 플로우**

```plaintext
📝 Checkout Code ──▶ 🛑 Stop Existing Services ──▶ 🏗️ Clean & Build Project ──▶ 🚀 Deploy & Restart Services
```

- **Job별로 실행 로그가 분리되어** 문제 추적이 용이합니다.  
- 이전 단계가 실패하면 **다음 단계가 자동으로 중단**되어 안정성이 높아집니다.  

---

## 📝 **간단한 예시 코드 (YAML)**

```yaml
name: Deploy Pipeline

on:
  push:
    branches: [ master ]

jobs:
  checkout:
    name: 📝 Checkout Code
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

  stop_services:
    name: 🛑 Stop Existing Services
    runs-on: ubuntu-latest
    needs: checkout
    steps:
      - name: Stop services on server
        uses: appleboy/ssh-action@v0.1.6
        with:
          host: ${{ secrets.REMOTE_IP }}
          username: ${{ secrets.REMOTE_USER }}
          key: ${{ secrets.REMOTE_PRIVATE_KEY }}
          script: |
            pm2 stop all
            pm2 delete all
            ./gradlew --stop

  build:
    name: 🏗️ Clean & Build Project
    runs-on: ubuntu-latest
    needs: stop_services
    steps:
      - name: Build project
        uses: appleboy/ssh-action@v0.1.6
        with:
          host: ${{ secrets.REMOTE_IP }}
          username: ${{ secrets.REMOTE_USER }}
          key: ${{ secrets.REMOTE_PRIVATE_KEY }}
          script: |
            git pull origin master
            ./gradlew clean build

  deploy:
    name: 🚀 Deploy & Restart Services
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy and restart services
        uses: appleboy/ssh-action@v0.1.6
        with:
          host: ${{ secrets.REMOTE_IP }}
          username: ${{ secrets.REMOTE_USER }}
          key: ${{ secrets.REMOTE_PRIVATE_KEY }}
          script: |
            pm2 start server.json
```

---

## ✅ **변경 전과 후 비교**

| 구분 | 변경 전 | 변경 후 |
|:---:|:---|:---|
| **구조** | 단일 Job | 4단계 Job 분리 |
| **에러 추적** | 어려움 | 쉬움 (어느 단계에서 실패했는지 바로 확인) |
| **유지보수성** | 낮음 | 높음 (단계별 수정 및 테스트 용이) |
| **안정성** | 낮음 (모든 과정 일괄 실행) | 높음 (각 단계 완료 후 다음 단계 실행) |

---

## 🚀 **마무리**

🔑 **배포 과정을 단계별로 나누니:**  
✅ **디버깅이 쉬워지고**  
✅ **안정적인 배포 환경을 구축**할 수 있었습니다.

배포 자동화를 개선하고 싶다면 **Job 분리**를 적극 추천!!!
