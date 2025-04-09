---
layout: default
title: TraceBoard 프론트엔드 및 백엔드 연동 구현
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2025-04-06 11:04:23
---

# TraceBoard 개발 과정 _01
{: .no_toc }

## 2025.04.06 (SAT)
{: .no_toc .text-delta }

---

# TraceBoard 프론트엔드 및 백엔드 연동 구현

이번 포스트에서는 DevZip 프로젝트의 서브 모듈인 TraceBoard의 프론트엔드 구현과 백엔드 연동 작업 과정을 기록합니다. TraceBoard는 웹사이트 방문자의 행동과 이벤트를 분석하고 시각화하는 대시보드 도구입니다.

## 1. 프론트엔드 구현

React를 기반으로 사용자 행동 분석을 위한 대시보드 UI를 개발했습니다. 대시보드는 다음 세 가지 핵심 컴포넌트로 구성되어 있습니다:

### 1.1 핵심 컴포넌트

#### VisitorMetrics
방문자 관련 주요 지표를 시각적으로 보여주는 컴포넌트로, 총 방문자 수, 고유 방문자 수, 페이지뷰, 이탈률 등의 정보를 카드 형태로 표시합니다.

```jsx
import React from 'react';
import styled from 'styled-components';

const MetricCard = styled.div`
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
`;

const MetricValue = styled.h2`
  font-size: 24px;
  color: #3498db;
  margin: 10px 0;
`;

const VisitorMetrics = ({ metrics }) => {
  return (
    <div>
      <h3>방문자 통계</h3>
      <div className="metrics-container">
        <MetricCard>
          <h4>총 방문자</h4>
          <MetricValue>{metrics.totalVisitors}</MetricValue>
        </MetricCard>
        <MetricCard>
          <h4>고유 방문자</h4>
          <MetricValue>{metrics.uniqueVisitors}</MetricValue>
        </MetricCard>
        {/* 추가 지표들... */}
      </div>
    </div>
  );
};

export default VisitorMetrics;
```

#### UserBehaviorChart
사용자 행동 패턴을 시간대별로 분석하여 차트로 표시하는 컴포넌트입니다. 페이지 체류 시간, 클릭 이벤트, 스크롤 깊이 등의 정보를 시각화합니다.

```jsx
import React from 'react';
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer } from 'recharts';
import PropTypes from 'prop-types';
import styled from 'styled-components';

// CustomTooltip 컴포넌트를 분리하여 외부에 정의
const CustomTooltip = ({ active, payload, label }) => {
  if (active && payload && payload.length) {
    return (
      <div className="custom-tooltip">
        <p className="label">{`시간: ${label}`}</p>
        <p className="value">{`클릭 수: ${payload[0].value}`}</p>
        <p className="value">{`페이지뷰: ${payload[1].value}`}</p>
      </div>
    );
  }
  return null;
};

// PropTypes 추가
CustomTooltip.propTypes = {
  active: PropTypes.bool,
  payload: PropTypes.array,
  label: PropTypes.string
};

const ChartContainer = styled.div`
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
  height: 400px;
`;

const UserBehaviorChart = ({ behaviorData }) => {
  return (
    <ChartContainer>
      <h3>사용자 행동 분석</h3>
      <ResponsiveContainer width="100%" height="85%">
        <LineChart data={behaviorData}>
          <CartesianGrid strokeDasharray="3 3" />
          <XAxis dataKey="time" />
          <YAxis />
          <Tooltip content={<CustomTooltip />} />
          <Legend />
          <Line type="monotone" dataKey="clicks" stroke="#8884d8" activeDot={{ r: 8 }} />
          <Line type="monotone" dataKey="pageviews" stroke="#82ca9d" />
        </LineChart>
      </ResponsiveContainer>
    </ChartContainer>
  );
};

export default UserBehaviorChart;
```

#### EventLogTable
시스템에서 수집한 이벤트 로그를 테이블 형태로 표시하는 컴포넌트입니다. 이벤트 타입, 시간, 사용자 ID, URL 등의 상세 정보를 제공합니다.

```jsx
import React from 'react';
import styled from 'styled-components';

const TableContainer = styled.div`
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  overflow-x: auto;
`;

const Table = styled.table`
  width: 100%;
  border-collapse: collapse;
  
  th, td {
    padding: 12px 15px;
    text-align: left;
    border-bottom: 1px solid #eee;
  }
  
  th {
    background-color: #f8f9fa;
    color: #495057;
  }
  
  tbody tr:hover {
    background-color: #f6f8ff;
  }
`;

const EventLogTable = ({ logs }) => {
  return (
    <TableContainer>
      <h3>이벤트 로그</h3>
      <Table>
        <thead>
          <tr>
            <th>시간</th>
            <th>이벤트 타입</th>
            <th>사용자 ID</th>
            <th>URL</th>
            <th>세부 정보</th>
          </tr>
        </thead>
        <tbody>
          {logs.map((log, index) => (
            <tr key={index}>
              <td>{log.timestamp}</td>
              <td>{log.eventType}</td>
              <td>{log.userId}</td>
              <td>{log.url}</td>
              <td>{log.details}</td>
            </tr>
          ))}
        </tbody>
      </Table>
    </TableContainer>
  );
};

export default EventLogTable;
```

### 1.2 반응형 디자인 적용

styled-components를 사용하여 모든 컴포넌트에 반응형 디자인을 적용했습니다. 이를 통해 다양한 화면 크기와 디바이스에서 최적의 사용자 경험을 제공할 수 있게 되었습니다.

```jsx
// 반응형 그리드 레이아웃 예시
const DashboardGrid = styled.div`
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
  margin: 20px 0;
  
  @media (max-width: 768px) {
    grid-template-columns: 1fr;
  }
`;
```

## 2. 발생한 문제점과 해결 방법

### 2.1 의존성 오류

**문제**: styled-components 라이브러리가 설치되어 있지 않아 컴포넌트 렌더링 실패

**해결방법**: npm을 통해 styled-components 패키지를 설치하고 레거시 피어 의존성 옵션 사용

```bash
npm install styled-components --save --legacy-peer-deps
```

### 2.2 ESLint 오류

**문제**: UserBehaviorChart 컴포넌트에서 사용하는 CustomTooltip 컴포넌트의 prop-types가 누락되어 ESLint 경고 발생

**해결방법**: CustomTooltip 컴포넌트를 분리하고 PropTypes 정의 추가

```jsx
import PropTypes from 'prop-types';

// CustomTooltip 컴포넌트 분리
const CustomTooltip = ({ active, payload, label }) => {
  // ... 컴포넌트 내용
};

// PropTypes 추가
CustomTooltip.propTypes = {
  active: PropTypes.bool,
  payload: PropTypes.array,
  label: PropTypes.string
};
```

### 2.3 SPA 라우팅 오류

**문제**: React Router를 사용한 SPA 라우팅에서 "/traceboard" 경로에 접근 시 "Internal Server Error: No static resource traceboard" 오류 발생

**해결방법**: Spring Boot의 WebController 및 application.properties 설정 수정

#### WebController.java 수정

```java
@Controller
public class WebController {
    
    // 기존 경로 외에 traceboard 경로 추가
    @GetMapping({"/", "/index", "/guestbook", "/traceboard/**"})
    public String forward() {
        return "forward:/index.html";
    }
}
```

#### application.properties 설정 추가

```properties
# 정적 리소스 설정 최적화
spring.resources.chain.strategy.content.enabled=true
spring.resources.chain.strategy.content.paths=/**
```

## 3. Spring Boot 백엔드 연동 작업

### 3.1 WebController 설정

SPA 라우팅을 지원하기 위해 WebController에서 `/traceboard/**` 경로를 처리하도록 설정 추가:

```java
@Controller
public class WebController {
    
    @GetMapping({"/", "/index", "/guestbook", "/traceboard/**"})
    public String forward() {
        return "forward:/index.html";
    }
}
```

### 3.2 정적 리소스 설정 최적화

Spring Boot의 정적 리소스 처리를 최적화하기 위해 application.properties 파일에 다음 설정을 추가했습니다:

```properties
# 정적 리소스 설정
spring.web.resources.static-locations=classpath:/static/
spring.web.resources.cache.cachecontrol.max-age=365d
spring.web.resources.chain.strategy.content.enabled=true
spring.web.resources.chain.strategy.content.paths=/**
```

### 3.3 더미 데이터 테스트

현재는 백엔드 API가 완전히 구현되지 않아 50개의 샘플 이벤트 로그 데이터로 프론트엔드 기능을 테스트하고 있습니다:

```javascript
// 테스트용 더미 데이터 생성
const generateDummyLogs = (count) => {
  const eventTypes = ['pageview', 'click', 'scroll', 'form_submit', 'error'];
  const urls = ['/home', '/about', '/products', '/contact', '/blog'];
  
  return Array.from({ length: count }, (_, i) => ({
    id: i + 1,
    timestamp: new Date(Date.now() - Math.floor(Math.random() * 86400000)).toISOString(),
    eventType: eventTypes[Math.floor(Math.random() * eventTypes.length)],
    userId: `user_${Math.floor(Math.random() * 1000)}`,
    url: urls[Math.floor(Math.random() * urls.length)],
    details: `Event details ${i+1}`
  }));
};

const dummyLogs = generateDummyLogs(50);
```

## 4. CI/CD 파이프라인 개선

### 4.1 GitHub Actions 자동 빌드 설정

GitHub Actions를 사용하여 프로젝트 빌드 자동화 파이프라인을 설정했습니다:

```yaml
name: Build and Deploy

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    
    - name: Set up JDK 11
      uses: actions/setup-java@v2
      with:
        java-version: '11'
        distribution: 'adopt'
        
    - name: Build with Gradle
      run: ./gradlew build
      
    - name: Install npm dependencies
      run: npm install --legacy-peer-deps
      
    - name: Build React app
      run: npm run build
```

### 4.2 빌드 실패 디버깅 및 해결

GitHub Actions에서 발생한 빌드 실패 문제를 디버깅하고 해결했습니다:

1. 의존성 이슈: `--legacy-peer-deps` 옵션 추가
2. ESLint 오류: 컴포넌트 PropTypes 추가 및 코드 리팩토링

## 5. 코드 변경사항

주요 변경사항은 다음과 같습니다:

1. TraceBoard 컴포넌트 import 경로 수정
2. UserBehaviorChart 컴포넌트의 CustomTooltip 분리 및 PropTypes 추가
3. WebController SPA 라우팅 설정 개선
4. application.properties 파일에 리소스 체인 전략 설정 추가

## 6. 다음 단계 계획

다음 단계로는 아래 작업들을 진행할 예정입니다:

- [ ] 백엔드 API 엔드포인트 구현 (EventLog 모델, 컨트롤러, 서비스 개발)
- [ ] 실제 데이터베이스 스키마 설계 및 구현 (PostgreSQL)
- [ ] 이벤트 수집 SDK 개발 및 배포
- [ ] 테스트 페이지에 SDK 적용하여 실제 데이터 수집 테스트

## 7. 마일스톤

현재까지의 진행 상황은 다음과 같습니다:

- [x] 프론트엔드 대시보드 UI 개발
- [x] styled-components 적용
- [x] SPA 라우팅 설정
- [ ] 백엔드 API 개발
- [ ] 실제 데이터 연동
- [ ] SDK 배포

## 8. 참고 자료

- [React 공식 문서](https://reactjs.org/docs/getting-started.html)
- [Spring Boot 정적 리소스 설정](https://docs.spring.io/spring-boot/docs/current/reference/html/web.html#web.servlet.spring-mvc.static-content)
- [styled-components 문서](https://styled-components.com/docs)
- [React Router 문서](https://reactrouter.com/web/guides/quick-start)

---

다음 포스트에서는 백엔드 API 개발과 실제 데이터베이스 연동에 대해 다루겠습니다. 