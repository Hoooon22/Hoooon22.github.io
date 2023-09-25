---
layout: default
title: AWS (DVA) - Section 6
parent: AWS (DVA)
grand_parent: STUDY
---

# AWS Certified Developer Associate - Section 6 (EC2 인스턴스 스토리지 / EBS)
{: .no_toc }

## 2023.09.25 (MON) ~
{: .no_toc .text-delta }

---

# EC2 인스턴스 스토리지

## EBS 볼륨
    Elastic Block Store Volume

- 인스턴스가 실행 중인 동안 연결 가능한 네트워크 드라이브
- 인스턴스 종류된 후에도 데이터를 지속할 수 있다.
- EBS 볼륨을 생성할 때는 특정 가용 영역에서만 가능하다.
    - 스냅샷을 이용하면 다른 가용 영역으로 볼륨 옮기기 가능

EBS 볼륨 = 네트워크 USB 스틱

- 네트워크 드라이브로 EC2 인스턴스에서 분리될 수 있다.
- 볼륨이기에 용량을 미리 결정해야 한다.
- 인스턴스에 연결할 수 있어, 필요한 경우에만 연결한다.