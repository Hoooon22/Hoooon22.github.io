---
layout: default
title: db오류
parent: SpringBoot
grand_parent: Java
date: 2024-07-22 21:12:11
category: Java
tags: [Springboot, Java, Error]
---
> [!question]
> 갑자기 잘되던 AWS RDS로의 접속이 안된다.
## 오류

```log
- [Server] Plugin mysql_native_password reported: ''mysql_native_password' is deprecated and will be removed in a future release. Please use caching_sha2_password instead'`
```
## 원인 #1
> 원인은 MySQL 8.0이상 부터의 보안 정책과 관련되었다.
### SSL/TLS
SSL/TLS은 클라이언트와 서버 프로그램이 네트워크로 통신하는 과정에서 도청 및 간섭, 위변조 방지를 위해서 **서로 신뢰할 수 있는 전자 서명이 포함된 인증서를 사용하는 암호화 통신 프로토콜** 

> [!info]
> [Content](<Deprecation and Removal Notes 
> Support for the TLS v1.0 and TLS v1.1 connection protocols is removed as of MySQL 8.0.28.
> Changes in MySQL 8.0.28 (2022–01–18, General Availability)>)

- 이 내용은 클라이언트(애플리케이션이나 PC 등)에서 MySQL을 SSL/TLS 방식으로 접속시에 **TLS1.0 또는 1.1 버전으로 접속한다면 다음과 같은 에러가 발생되면서 접속이 불가능함을 의미**

## 해결
- 이와 다른 부분이였다. 다음날 다시 접속하니 해결,,? 되었다..