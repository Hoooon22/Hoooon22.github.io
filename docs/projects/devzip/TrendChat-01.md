---
layout: default
title: AWS EC2 시간대 설정 및 Python(pm2) 데몬 반복 실행
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2025-02-11 20:10:33
---

# TrendChat 페이지 _01
{: .no_toc }

## 2025.02.11 (TUE)
{: .no_toc .text-delta }

---

# AWS EC2 시간대 설정 및 Python 자동 실행

이번 포스트에서는 AWS EC2 인스턴스의 시간대를 한국 시간으로 설정하고, Python 스크립트를 주기적으로 실행하는 방법에 대해 설명합니다. 또한, Python 스크립트를 이용해 트렌드 데이터를 가져오고 이를 JSON 파일로 저장하는 방법도 다룹니다.

## 1. AWS EC2 시간대 한국 시간으로 변경

EC2 인스턴스의 시간대는 기본적으로 UTC로 설정되어 있습니다. 이를 한국 시간(KST, UTC+9)으로 변경하려면 아래 명령어를 사용합니다:

```bash
sudo timedatectl set-timezone Asia/Seoul
```

변경 후 확인하려면:

```bash
timedatectl
```

## 2. Python 스크립트 2시간마다 자동 실행

`pm2`를 사용해 Python 스크립트를 2시간마다 자동으로 실행할 수 있습니다. 아래 명령어를 사용하면 됩니다:
해당 코드는 Github Actions로 실행됩니다.

```bash
pm2 start python3 --name "python-script" --cron "0 */2 * * *" -- /path/to/your/script.py
```

## 3. Python 코드: 트렌드 키워드 JSON으로 저장

`pytrends`를 이용해 한국의 트렌드 데이터를 가져와 JSON 파일로 저장하는 간단한 코드입니다:

```python
import json
import os
from pytrends.request import TrendReq

# pytrends 초기화
pytrends = TrendReq(hl='ko', tz=540)

# 트렌드 키워드 가져오기
pytrends.build_payload([], geo='KR', timeframe='now 1-d')
top_keywords = pytrends.trending_searches(pn='south_korea')[0].tolist()

# 결과를 JSON으로 저장
result = {"top_keywords": top_keywords}
json_file_path = os.path.join(os.path.dirname(os.path.abspath(__file__)), 'trending_keywords.json')
with open(json_file_path, 'w', encoding='utf-8') as json_file:
    json.dump(result, json_file, ensure_ascii=False, indent=2)
```

---

이 코드를 통해 EC2 인스턴스에서 한국 시간대를 설정하고, Python 스크립트를 주기적으로 실행하며, 현재 날짜의 트렌드 검색어 데이터를 저장하는 방법을 간단히 구현할 수 있습니다.
