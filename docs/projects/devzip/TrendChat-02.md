---
layout: default
title: JSON 데이터를 API로 변환
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2025-02-11 21:56:47
---

# TrendChat 페이지 _02
{: .no_toc }

## 2025.02.11 (TUE)
{: .no_toc .text-delta }

---

# JSON 데이터를 API로 변환하는 과정

이 문서는 JSON 파일을 읽어 Java 객체로 변환하고, 이를 REST API를 통해 제공하는 과정입니다.

## 1. JSON 파일 (`trending_keywords.json`)

먼저, 아래와 같은 JSON 파일을 준비합니다:

```json
{
  "updated_at": "2025-02-11 20:54:42",
  "top_keywords": [
    "**** ** ******** **",
    "****",
    "*************",
    "*****",
    "*****",
    "*****",
    "************",
    "***** *****",
    "****",
    "****11158****",
    "*****",
    "****",
    "*****",
    "**** ** *****를 *****!",
    "*****",
    "*****",
    "*****",
    "****",
    "****",
    "***의 **"
  ]
}
```

## 2. Java 모델 클래스 (`TrendingKeywords`)

JSON 데이터를 Java 객체로 변환하기 위해, 아래와 같은 Java 클래스를 정의합니다:

```java
package com.hoooon22.devzip.Model;

import java.util.List;
import com.fasterxml.jackson.annotation.JsonProperty;

public class TrendingKeywords {
    
    @JsonProperty("updated_at")
    private String updatedAt;

    @JsonProperty("top_keywords")
    private List<String> topKeywords;

    // 기본 생성자
    public TrendingKeywords() {}

    // Getter, Setter
    public String getUpdatedAt() {
        return updatedAt;
    }

    public void setUpdatedAt(String updatedAt) {
        this.updatedAt = updatedAt;
    }

    public List<String> getTopKeywords() {
        return topKeywords;
    }

    public void setTopKeywords(List<String> topKeywords) {
        this.topKeywords = topKeywords;
    }
}
```

## 3. 서비스 클래스 (`TrendService`)

`trending_keywords.json` 파일을 읽고 `TrendingKeywords` 객체로 변환하는 서비스 클래스를 작성합니다:

```java
package com.hoooon22.devzip.Service;

import java.io.IOException;
import java.io.InputStream;

import org.springframework.core.io.ClassPathResource;
import org.springframework.stereotype.Service;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.hoooon22.devzip.Model.TrendingKeywords;

@Service
public class TrendService {

    public TrendingKeywords getTrendingKeywords() throws IOException {
        // ClassPathResource를 사용하여 JSON 파일 읽기
        ClassPathResource resource = new ClassPathResource("trending_keywords.json");

        // InputStream을 얻어 JSON 파일 읽기
        InputStream inputStream = resource.getInputStream();

        // ObjectMapper로 JSON 파일을 Java 객체로 변환
        ObjectMapper objectMapper = new ObjectMapper();
        return objectMapper.readValue(inputStream, TrendingKeywords.class);
    }
}
```

## 4. REST 컨트롤러 (`TrendController`)

REST API를 제공하는 컨트롤러를 작성합니다:

```java
package com.hoooon22.devzip.Controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.hoooon22.devzip.Model.TrendingKeywords;
import com.hoooon22.devzip.Service.TrendService;

@RestController
@RequestMapping("/api/trend")
public class TrendController {

    @Autowired
    private TrendService trendService;

    // /api/trend/timestamp - 시간 반환
    @GetMapping("/timestamp")
    public String getTimestamp() throws IOException {
        TrendingKeywords trendingKeywords = trendService.getTrendingKeywords();
        return trendingKeywords.getUpdatedAt();
    }

    // /api/trend/keywords - 키워드 리스트 반환
    @GetMapping("/keywords")
    public List<String> getTopKeywords() throws IOException {
        TrendingKeywords trendingKeywords = trendService.getTrendingKeywords();
        return trendingKeywords.getTopKeywords();
    }
}
```

## 5. API 호출

- **/api/trend/timestamp**: `updated_at` 시간을 반환합니다.
- **/api/trend/keywords**: `top_keywords` 리스트를 반환합니다.

---

이 과정을 통해, JSON 파일을 읽고 Java 객체로 변환하여 REST API에서 필요한 정보를 제공합니다. 이 방법은 Spring Boot와 Jackson 라이브러리를 활용하여 간단하고 효과적으로 구현할 수 있습니다.
