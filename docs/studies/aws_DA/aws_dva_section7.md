---
layout: default
title: AWS (DVA) - Section 7
parent: AWS (DVA)
grand_parent: STUDY
---

# AWS Certified Developer Associate - Section 7 (AWS 기초: ELB + ASG)
{: .no_toc }

## 2023.11.21 (TUE) ~
{: .no_toc .text-delta }

---

# 고가용성 및 확장성


## 확장성
    애플리케이션 시스템이 조정을 통해 더 많은 양을 처리할 수 있다는 의미

- 수직 확장성
  - 인스턴스 크기 확장
  - 하드웨어 제한이 있기 때문에, 한계가 있다.
- 수평 확장성(탄력성)
  - 인스턴스나 시스템의 수를 늘리는 방법

## 고가용성
    애플리케이션 또는 시스템을 적어도 둘 이상의 AWS의 AZ나 데이터 센터에서 가동중인 것을 의미

---

# 일래스틱 로드 밸런싱(ELB)

## 로드 밸런서
    서버 혹은 서버셋으로 트래픽을 백엔드나 다운스트림 EC2 인스턴스 또는 서버들로 전달하는 역할  
    = 관리형 로드 밸런서

- 부하를 다수의 다운스트림 인스턴스로 분산하기 위해 사용