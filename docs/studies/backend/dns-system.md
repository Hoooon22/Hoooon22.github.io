---
layout: default
title: DNS 시스템의 작동 원리
parent: Backend
grand_parent: Studies
nav_order: 3
---

# DNS(Domain Name System)의 작동 원리
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## DNS란?

DNS(Domain Name System)는 사람이 읽을 수 있는 도메인 이름(예: www.example.com)을 컴퓨터가 읽을 수 있는 IP 주소(예: 192.168.1.0)로 변환하는 시스템입니다. 이는 마치 전화번호부와 같은 역할을 하며, 인터넷 상의 모든 도메인에 대한 주소록이라고 할 수 있습니다.

## DNS의 기본 작동 원리

<img src="../../../../assets/images/backend/dns-system.png" alt="DNS 시스템 작동 원리">
*DNS 시스템의 기본 작동 원리*

DNS의 작동 원리는 크게 두 가지 형태로 나눌 수 있습니다:

1. **작동원리의 기본적인 형태**
   - 클라이언트가 DNS 서버에 도메인에 대한 IP 주소를 요청
   - DNS 서버가 해당 도메인의 IP 주소를 가지고 있다면 응답
   - 클라이언트는 받은 IP 주소로 웹사이트에 접속

2. **좀 복잡한 형태 (네부 많은 도메인의 외부 DNS)**
   - 클라이언트가 Local DNS에 도메인 질의
   - Local DNS가 Root DNS에 질의
   - Root DNS가 TLD DNS 서버 정보 제공
   - Local DNS가 TLD DNS에 질의하여 도메인 DNS 정보 획득
   - 최종적으로 도메인의 IP 주소를 얻어 클라이언트에게 전달

## DNS 서버의 종류

DNS 시스템에는 여러 종류의 DNS 서버가 존재합니다:

1. **Local DNS 서버**
   - 기본적으로 설정된 DNS 서버
   - 도메인에 대한 IP 주소가 캐시되어 있으면 즉시 응답
   - 캐시가 없는 경우 다른 DNS 서버에 질의

2. **Root DNS 서버**
   - DNS 시스템의 최상위 서버
   - TLD DNS 서버의 정보를 제공

3. **TLD(Top Level Domain) DNS 서버**
   - .com, .net, .org 등 최상위 도메인을 관리
   - 해당 도메인의 DNS 서버 정보를 제공

4. **Domain DNS 서버**
   - 실제 도메인의 IP 주소 정보를 가지고 있는 서버
   - 최종적으로 도메인에 대한 IP 주소를 제공

## DNS Cache

DNS 시스템의 효율성을 높이기 위해 캐시 시스템을 사용합니다:

- **DNS Cache의 목적**
  - 매번 DNS에 요청을 통해 IP를 찾아야 하는 비효율 감소
  - PC에 DNS cache를 활용하여 빠른 접속 가능

## 정리

DNS는 인터넷의 핵심 인프라로, 도메인 이름과 IP 주소를 매핑하는 중요한 역할을 수행합니다. 계층적인 구조를 통해 효율적으로 도메인 정보를 관리하며, 캐시 시스템을 통해 빠른 응답 속도를 제공합니다. 이러한 시스템 덕분에 우리는 복잡한 IP 주소 대신 기억하기 쉬운 도메인 이름으로 웹사이트에 접속할 수 있습니다. 