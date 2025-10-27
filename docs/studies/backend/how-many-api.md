---
layout: default
title: 모든 유형의 API에 대해 알아보자.
parent: Backend
grand_parent: Study
nav_order: 5
date: 2025-10-21 20:28:00
---

# 모든 유형의 API에 대해 알아보자.

---

## REST

REST API: 인터넷을 통해 애플리케이션이 서로 통신할 수 있는 기본적인(?) 방법  

- REST API는 웹 브라우징에서 우리가 익히 알고 있는 HTTP 메서드를 사용한다.
  - GET, POST, PUT, DELETE
  - (GET)API를 요청하면 깔끔한 JSON 형태로~
- REST는 **Stateless**로 각 요청이 완전히 독립적
  - 누가 무엇을 요청했는지 혼동하지 않고, 수백만명의 사용자를 처리할 수 있다.
- 플랫폼에도 독립적
- 하지만, 은행이나 기업 시스템에 사용하기엔 공식적이지 않다.


## SOAP

SOAP: Simple Object Access Protocol  

- 시스템 간 통신 중 가장 오래되고 **공식**적인 방법 중 하나 (Like 비즈니스 계약)
- 모든 메시지는 엄격한 규칙을 따라야함.
- XML을 기반으로 정해진 구조의 봉투를 주고 받는 느낌

```XML
   POST /CalculatorService.asmx HTTP/1.1
   Host: example.com
   Content-Type: text/xml; charset=utf-8
   Content-Length: [본문 길이]
   SOAPAction: "http://example.com/calculator/Add"

   <?xml version="1.0" encoding="utf-8"?>
   <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
   <soap:Body>
      <Add xmlns="http://example.com/calculator/">
         <intA>3</intA>
         <intB>5</intB>
      </Add>
   </soap:Body>
   </soap:Envelope>
```

- 프로토콜의 독립적인 것이 장점.
  - HTTP, HTTPS 뿐만 아니라, SMTP, TCP, 등등..
- 오류 처리, 보안, 트랜잭션 지원에 대한 표준이 내장되어 있기 때문에, 정확성이 중요한 산업에서 널리 쓰임.


## gRPC

RPC란, 원격 프로시저 호출. 네트워크로 연결된 [서버]에 있는 함수를 마치 [클라이언트]에 있는 로컬 함수처럼 호출할 수 있는 기술.  
-> 이게 무슨 소리지? 
--> 개발자가 네트워크 통신의 복잡한 과정(소켓 열기, 데이터 전송 등)을 신경 쓰지 않고, 그냥 add(3, 5)와 같이 함수를 호출하는 데만 집중할 수 있도록 추상화 해줌.

- 아무튼, RPC는 현대 대규모 실시간 앱에 맞지 않게 느리고 텍스트가 많은 Low 버전 느낌

gRPC: Google RPC
- 구글에서 RPC를 현대적으로 더 높은 성능으로 구현한 것.
- REST는 텍스트 기반 JSON을 전송하는 반면, 