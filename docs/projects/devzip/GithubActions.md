---
layout: default
title: Github Actions를 활용한 프로젝트 무중단 배포
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2024-10-23 15:46:36
---

# Github Actions를 활용한 프로젝트 무중단 배포
{: .no_toc }

## 2024.10.23 (WED)
{: .no_toc .text-delta }

---

Devzip 프로젝트를 진행하면서, 매번 console에 접속하여 git pull 및 빌드, 재시작하는 것이 굉장히 비효율적으로 느껴졌다.

그 때, 현재 Github.io 블로그에서 깃헙 커밋 변화에 따른 자동 빌드 시스템이 생각나서 이를 활용해보기로 하였다.

## Github Actions
Github Actions는 빌드, 테스트 및 배포 파이프라인을 자동화할 수 있는 CI/CD 플랫폼이다.

GitHub Actions를 사용하면 자동으로 코드 저장소에서 **어떤 이벤트(event)가 발생했을 때** 특정 작업이 일어나게 하거나 주기적으로 어떤 작업들을 반복해서 실행시킬 수 있다.

.github/workflows 내부의 나의 설정 파일은 아래와 같다.


```yml
name: dev branch auto ci process script

on: # 아래 job을 실행시킬 상황

push:

branches: [ master ]

jobs:

deploy:

name: deploy

runs-on: ubuntu-latest # 실행될 인스턴스 OS와 버전

  

steps:

- name: excuting remote ssh commands

uses: appleboy/ssh-action@v0.1.6 # ssh 접속하는 오픈소스

with:

host: ${{ secrets.REMOTE_IP }} # 인스턴스 IP

username: ${{ secrets.REMOTE_USER }} # 우분투 아이디

key: ${{ secrets.REMOTE_PRIVATE_KEY }} # ec2 instance pem key

port: ${{ secrets.REMOTE_SSH_PORT }} # 접속포트

script: | # 실행할 스크립트

# ~~~
```

5번째 줄: **push**이벤트가 발생할 때, 실행 시킨다.

이외의 코드는 AWS EC2에 접속하고 명령을 실행하는 코드로 이루어져 있다.

![](https://i.imgur.com/qLQdLmQ.png)
- push 시, 자동 실행된 모습