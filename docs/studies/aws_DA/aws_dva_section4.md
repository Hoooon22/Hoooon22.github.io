---
layout: default
title: AWS (DVA) - Section 4
parent: AWS (DVA)
grand_parent: STUDY
---

# AWS Certified Developer Associate - Section 4 (IAM)
{: .no_toc }

## 2023.09.14 (THU)
{: .no_toc .text-delta }

---

# AWS Identity & Access Management (AWS IAM)

## IAM: Users & Groups
- IAM에서는 사용자를 생성하고 그룹에 배치하기 때문에, **글로벌** 서비스이다.
- 루트 어카운트는 기본으로 만들어진다. 이후, 루트는 사용되거나 공유되면 안된다.
- 사용자와 그룹을 만들어 사용한다.

## IAM: 권한
- 사용자 또는 그룹에게 정책, 또는 IAM 정책이라고 불리는 JSON문서를 지정할 수 있다.
    ![출처 : 【한글자막】 AWS Certified Developer Associate 시험 합격을 위한 모든 것!](../../../../assets/images/aws_dva/스크린샷 2023-09-14 오후 7.16.46.png)
- AWS는 필요 이상의 권한을 사용자에게 주지 않는다.

- 그룹에게 권한을 부여하는 정책이 있으며, 개인에게는 개인에게만 적용되는 인라인 정책이라는 것을 생성할 수 있다.

- **IAM 정책 구조**  
    ![출처 : 【한글자막】 AWS Certified Developer Associate 시험 합격을 위한 모든 것!](../../../../assets/images/aws_dva/스크린샷 2023-09-14 오후 10.43.31.png)

- 그룹과 사용자들의 정보 보호
    1. 비밀번호 정책
        - ex) 길이 제한, 특수문자 등
    2. (중요) 다요소 인증 - MFA
        - AWS에서 필수적으로 사용하도록 권장
        - 적어도 root를, 최대한 IAM 사용자를 지켜야 함
        - 따라서 비밀번호 외, MFA를 이용하는 것이다.
        - ex) Alice has **Password + MFA Token**
            => 로그인 성공!

        - AWS에서 MFA 장치 옵션 (중요)
            1. 가상 MFA 장치 : 모바일이나 기타 장비로 가능 (Like 모바일 OTP)
            2. U2F 보안 키 (물리)
            3. 하드웨어 키 팝 MFA (물리)

- **유저가 AWS에 접근하는 방법**
    1. AWS Management Console (protected by password + MFA)
    2. AWS Command Line Interface (CLI): protected by access keys
    3. AWS Software Developer Kit (SDK) - for code: protected by access keys
    - 다들 각자의 키를 생성하기 때문에, 개인 키는 공유하면 안된다
        - Access Key ID ~= username
        - Secret Access Key ~= password

    - AWS CLI
        - AWS 서비스와 상호 작용할 수 있는 오픈소스 도구
        - AWS CLI를 사용하면 Pwershell이나 터미널에서도 AWS에서 제공하는 명령어 기능을 실행할 수 있다.
        -> 실습 해봄
        - CLI 권한은 IAM 권한과 같다.
        - AWS CloudShell에서도 접속할 수 있다.

    - AWS SDK
        - 소프트웨어 개발 키트
        - 코딩을 통해 애플리케이션 내에 심어두는 것

## IAM Roles  
    이는 사용자와 유사하지만, 실제 사용자가 사용하는 것이 아니라 AWS 서비스가 사용하는 것을 말한다.
    
ex) EC2 인스턴스가 AWS에서 작업을 수행할 수 있도록, EC2에게 권한을 부여하는 것이다.

## IAM Security Tools
    
- IAM 자격 증명 보고서 (계정 레벨)
    - 계정에 있는 사용자와 다양한 자격 증명의 상태를 포함
- IAM 액세스 관리자 (유저 레벨)
    - 사용자의 권한을 관리

## IAM 요약
- Users: mapped to a physical user, has a password for AWS Console
- Groups: contains users only
- Policies: JSON document that outlines permissions for users or groups 
- Roles: for EC2 instances or AWS services
- Security: MFA + Password Policy
- AWS CLI: manage your AWS services using the command-line
- AWS SDK: manage your AWS services using a programming language 
- Access Keys: access AWS using the CLI or SDK
- Audit: IAM Credential Reports & IAM Access Advisor