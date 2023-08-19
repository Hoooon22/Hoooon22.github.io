---
layout: default
title: AWS 기초
parent: AWS (SAA)
grand_parent: STUDY
---

# AWS 기초
{: .no_toc }

## 2023.08.19 (SAT)
{: .no_toc .text-delta }

---

## 1. 온프라미스와 AWS 용어 비교

AWS는 아마존에서 온프레미스를 클라우드 서비스로 만든 것이다.

> 온프라미스(On-premise)란, 기업의 서버를 클라우드 같은 원격 환경에서 운영하는 방식이 아닌, 자체적으로 보유한 전산실 서버에 직접 설치해 운영하는 방식이다.  

![AWS 아마존 머신 이미지](../../../../assets/images/aws_saa/aws infra.png)

--

온프라미스 용어 = 클라우드 용어
- 방화벽 = 보안그룹
- ACL = NACL
    * ACL(Access Control List) : 허가되지 않은 이용자가 라우터나 네트워크의 특정 자원을 접근하려고 하는 것을 차단한다.
- 관리자 권한 = IAM
- L4, 로드 밸런서 = ELB(일라스틱 로드 밸런서), 탄력적인 로드 밸련서, ALB, ...
    * 로드 밸런서 : 서버에 가해지는 부사(=로드)를 분산(=밸런싱)해주는 장치 또는 기술
- 네트워크 = VPC
    * 