---
layout: default
title: HTTP/HTTPS 프로토콜 이해
parent: Backend
grand_parent: Study
nav_order: 4
date: 2025-09-16 15:51:00
---

# HTTP/HTTPS 프로토콜 이해

---

## HTTP란?

HTTP는 HyperText Transfer Protocol의 약자  
웹 브라우저와 웹 서버가 서로 통신할 때, 사용되는 약속  
즉, 웹에서 데이터를 주고받기 위한 통신 규약이다.

HTTP의 통신과정: 클라이언트의 요청 -> 서버의 응답  
이 요청 메시지에는 무엇을(naver.com, index.html, ...), 어떻게(GET,POST, ...), 누가(브라우저에 대한 정보) 등이 적혀있다.  

서버의 응답은 크게 두가지가 있다.  
1. 처리 결과 (Status Code)
   - 200 OK, 404 Not Found, ...
2. 실제 데이터 (Body)
   - 요청한 웹페이지의 실제 내용(HTML, CSS, Javascript 파일 등)을 보여준다.  

이렇게 간단한 요청과 응답의 반복.

## HTTPS의 등장

HTTP는 평문 통신이기 때문에, 중간에 패킷을 가로채면 내용이 노출되는 보안 이슈가 있다.  
이러한 보안 문제를 해결하기 위해 등장한 것이 HTTPS이다.  

HTTPS는 SSL/TLS라는 특별한 기술을 사용해서 주고받는 데이터를 안전하게 암호화 한다.  

그럼 여기서, 서버와 브라우저는 어떻게 서로만 알아볼 수 있는 암호화를 할 수 있을까?  

## SSL/TLS Handshake

1. Client Hello
   - 브라우저가 서버에게 (너 진짜임?) 증명을 요구함.
2. Server Hello & Certificate
   - 서버는 신뢰할 수 있는 기관에서 발급받은 인증서(SSL 인가?)를 보여줌.
   - 이 인증서 안에는 웹사이트의 정보와 데이터를 암호화할 수 있는 공개키(Public key)가 있음.
3. Key Exchange
   - 브라우저는 서버가 준 인증서를 검증하고, 서버의 공개키를 사용하여 둘만 사용할 **대칭키**를 만듬.
   - 서버의 공개키로 잠겨있기 때문에, 그에 맞는 서버만 확인할 수 있음.
4. Secure Communication
   - 이제 브라우저와 서버는 둘만 아는 비밀 암호로 모든 데이터를 암호화해서 주고받음.

## HTTPS 필수인 시대

데이터의 중요성이 높아지는 만큼, 기본적인 웹사이트 보안은 HTTPS에서 시작한다.