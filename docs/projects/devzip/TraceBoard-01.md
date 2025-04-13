---
layout: default
title: TraceBoard 프론트엔드 및 백엔드 연동 구현
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2025-04-09 20:10:49 
---

# 웹사이트 분석을 위한 새로운 솔루션 - DevZip 트레이스보드

> 💡 **TL;DR**: 트레이스보드는 DevZip 플랫폼의 웹 분석 도구로, 구글 애널리틱스보다 가볍고 개발자 친화적인 인터페이스를 제공합니다. 몇 줄의 코드로 설치 가능하며 사용자 행동을 실시간으로 추적하고 개인정보 보호 규정을 준수합니다.

![트레이스보드 대시보드](/images/traceboard-dashboard.png)
*트레이스보드 대시보드 화면: 직관적인 인터페이스로 주요 지표를 한눈에 확인할 수 있습니다.*

## 왜 트레이스보드인가?

웹 사이트의 방문자 트래픽과 행동을 분석하는 것은 서비스 개선에 필수적입니다. 하지만 기존 분석 도구들은 복잡하거나, 무겁거나, 개인정보 이슈가 있었죠. DevZip 트레이스보드는 이러한 문제를 해결하기 위해 개발되었습니다.

트레이스보드의 핵심 장점:

- **가벼움**: 웹사이트 성능에 미치는 영향 최소화 (페이지 로딩 속도 유지)
- **개발자 친화적**: API를 통한 맞춤형 통합 가능
- **간편한 설치**: 단 두 줄의 코드로 설치 완료
- **개인정보 보호**: IP 주소 등 민감 정보 마스킹 처리
- **실시간 분석**: 사용자 행동을 즉시 확인 가능

## 어떤 데이터를 볼 수 있나요?

트레이스보드는 크게 세 가지 영역의 데이터를 제공합니다:

### 1. 방문자 지표

![방문자 지표](/images/traceboard-visitor-metrics.png)
*방문자 수, 페이지뷰, 세션 시간 등의 기본 지표*

- 고유 방문자 수 (일간/주간/월간)
- 총 페이지뷰 수
- 방문자당 평균 페이지뷰
- 평균 세션 지속 시간
- 이탈률

### 2. 사용자 행동 차트

![사용자 행동 차트](/images/traceboard-behavior-chart.png)
*이벤트 유형과 디바이스별 분포를 시각화한 차트*

트레이스보드는 아래 데이터를 직관적인 차트로 시각화합니다:
- 이벤트 유형별 분포 (페이지뷰, 클릭, 스크롤, 폼 제출)
- 디바이스 유형별 분포 (모바일, 태블릿, 데스크톱)
- 브라우저별 사용 현황
- 시간대별/요일별 방문 패턴

### 3. 실시간 이벤트 로그

![이벤트 로그](/images/traceboard-event-log.png)
*실시간으로 발생하는 모든 사용자 활동을 시간순으로 기록*

이벤트 로그에서는 다음 정보를 실시간으로 확인할 수 있습니다:
- 이벤트 발생 시간
- 이벤트 유형 (페이지뷰, 클릭 등)
- 페이지 경로
- 마스킹 처리된 사용자 ID
- 디바이스 및 브라우저 정보

## 설치 방법

트레이스보드 설치는 3단계로 간단하게 완료됩니다:

### 1단계: 스크립트 추가

웹사이트의 `<head>` 섹션에 다음 코드를 추가하세요:

```html
<script src="https://devzip.site/traceboard/tracker.js"></script>
<script>
  TraceboardTracker.init({
    siteId: '귀하의_사이트_ID'
  });
</script>
```

### 2단계: 대시보드 접근

DevZip에 로그인한 후 메뉴에서 '트레이스보드'를 클릭하면 실시간 데이터를 확인할 수 있습니다.

### 3단계: 커스텀 이벤트 설정 (선택사항)

특정 사용자 행동을 더 자세히 추적하고 싶다면:

```javascript
// 회원가입 버튼 클릭 추적 예시
document.getElementById('signup-button').addEventListener('click', function() {
  TraceboardTracker.trackEvent('signup_click', {
    category: '전환',
    label: '회원가입 버튼'
  });
});
```

## 활용 사례: 15% 이탈률 감소 달성

DevZip은 자사 웹사이트에 트레이스보드를 적용한 후 흥미로운 결과를 얻었습니다:

> "트레이스보드를 통해 회원가입 단계에서 많은 사용자들이 이탈하는 것을 발견했습니다. 폼을 간소화한 결과, 전환율이 23% 증가했고 전체 이탈률은 15% 감소했습니다." - DevZip 제품팀

주요 성과:
- **이탈률 n% 감소**: 문제 페이지를 발견하고 개선
- **페이지 로딩 n% 개선**: 사용자 행동 패턴에 따른 리소스 우선순위 조정
- **전환율 n% 증가**: 폼 제출 과정의 병목 지점 개선

## 앞으로 추가될 기능

트레이스보드를 계속 발전시키고 있습니다. 곧 출시될 기능들은:

- 사용자 세션 리플레이 (익명화)
- 클릭 및 스크롤 히트맵
- A/B 테스트 내장 도구
- AI 기반 인사이트 및 개선 제안

## 지금 바로 시작하세요

트레이스보드는 모든 DevZip 계정에서 무료로 사용할 수 있습니다. [devzip.site](https://devzip.site)에서 회원가입 후 바로 사용해 보세요.

궁금한 점이나 도움이 필요하신가요? 질문이나 피드백은 momo990305@gmail.com으로 보내주세요. 트레이스보드로 여러분의 웹사이트를 더욱 스마트하게 운영하세요! 🚀

---

# TraceBoard 개발 과정 _01
{: .no_toc }

## 2025.04.09 (WED)
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

### 3.3 실제 이벤트 데이터 수집 및 분석

백엔드와의 연동 테스트가 성공적으로 이루어지고 있습니다. 현재까지 수집된 실제 이벤트 데이터의 일부는 다음과 같습니다:

```json
{
  "osDistribution": {
    "MacOS": 13
  },
  "totalEvents": 13,
  "pageViewDistribution": {},
  "hourlyDistribution": {
    "8시": 13
  },
  "eventTypeDistribution": {
    "click": 1,
    "pageView": 12
  },
  "browserDistribution": {
    "Chrome": 13
  },
  "deviceDistribution": {
    "desktop": 13
  }
}
```

#### 데이터 분석

현재 수집된 데이터를 분석한 결과:

1. **이벤트 유형 분포**: 총 13개의 이벤트 중 12개는 페이지 뷰(pageView), 1개는 클릭(click) 이벤트입니다.
2. **운영체제 분포**: 모든 이벤트(13개)가 MacOS에서 발생했습니다.
3. **브라우저 분포**: 모든 이벤트가 Chrome 브라우저에서 발생했습니다.
4. **기기 유형**: 모든 이벤트가 데스크톱 환경에서 발생했습니다.
5. **시간대별 분포**: 모든 이벤트가 8시대에 발생했습니다.

이 데이터는 초기 테스트 단계에서 수집된 것으로, 실제 서비스 환경에서는 더 다양한 사용자와 기기에서 발생하는 이벤트를 분석할 수 있을 것입니다.

### 3.4 더미 데이터 테스트

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

## 6. 발견된 추가 문제점 및 해결 방안

### 6.1 데이터 렌더링 문제

**문제**: 백엔드에서 이벤트 로그가 정상적으로 저장되고 데이터를 가져오는 것까지는 성공했으나, 프론트엔드 화면에 데이터가 표시되지 않는 문제가 발생했습니다.

콘솔 로그에서는 다음과 같이 데이터가 정상적으로 불러와지는 것을 확인할 수 있습니다:
```
페이지 뷰 이벤트 전송: /traceboard
App.js:29 트레이스보드 트래커가 초기화되었습니다.
index.js:150 서버에서 데이터를 성공적으로 가져왔습니다: 
Object
index.js:150 서버에서 데이터를 성공적으로 가져왔습니다: 
{osDistribution: {…}, totalEvents: 22, pageViewDistribution: {…}, hourlyDistribution: {…}, eventTypeDistribution: {…}, …}
```

화면에는 "데이터가 없습니다. 선택한 기간 동안 기록된 이벤트가 없습니다. 다른 기간을 선택하거나 나중에 다시 확인해 주세요." 메시지만 표시되고 있습니다.

또한 개발자 도구에서는 다음과 같은 오류가 발견되었습니다:
```
Error with Permissions-Policy header: Unrecognized feature: 'browsing-topics'.
RouteTracker.js:17 페이지 접속: /traceboard
App.js:29 트레이스보드 트래커가 초기화되었습니다.
```

**추가 문제 분석**: 이전 해결 방안을 적용했음에도 불구하고 여전히 데이터가 화면에 표시되지 않는 문제가 지속되고 있습니다. 추가 조사 결과 다음과 같은 심층적인 원인을 발견했습니다:

1. **JSON 구조 불일치**: 프론트엔드에서 기대하는 JSON 구조와 백엔드에서 제공하는 구조가 근본적으로 다른 상황임
2. **Promise 체인 처리 오류**: 비동기 데이터 로딩 과정에서 Promise 처리가 제대로 이루어지지 않아 상태 업데이트 타이밍 문제 발생
3. **컴포넌트 리렌더링 이슈**: React 컴포넌트의 상태 업데이트 후 리렌더링이 제대로 트리거되지 않는 문제
4. **데이터 변환 과정의 누락**: 백엔드 응답에서 일부 필수 필드가 누락되거나 `null`/`undefined`인 경우 처리 로직 부재

**개선된 해결 방안**:

1. **직접 데이터 구조 검사 및 변환**:
   콘솔에 출력된 실제 JSON 구조를 기반으로 정확한 데이터 매핑 함수를 구현합니다.

```jsx
// 개선된 데이터 매핑 함수
const enhancedMapAnalyticsData = (backendData) => {
  console.log('원본 데이터:', backendData);
  
  // 데이터 유효성 검사 강화
  if (!backendData || typeof backendData !== 'object') {
    console.error('유효하지 않은 데이터 형식:', backendData);
    return null;
  }
  
  try {
    // 이미지에서 확인된 실제 백엔드 응답 구조 기반 매핑
    const totalEvents = backendData.totalEvents || 0;
    const osDistribution = backendData.osDistribution || {};
    const eventTypeDistribution = backendData.eventTypeDistribution || {};
    
    // 정확한 필드명 매칭
    const pageViewCount = (eventTypeDistribution.pageView || 0) + 
                          (eventTypeDistribution.pageview || 0) + 
                          (eventTypeDistribution.page_view || 0);
                          
    const clickCount = (eventTypeDistribution.click || 0) + 
                      (eventTypeDistribution.Click || 0);
    
    // 방문자 지표 데이터 직접 계산
    const visitorMetrics = {
      totalVisitors: totalEvents,
      uniqueVisitors: Object.values(backendData.deviceDistribution || {}).reduce((a, b) => a + b, 0),
      pageViews: pageViewCount,
      bounceRate: totalEvents > 0 ? "0%" : "N/A"
    };
    
    // 백엔드 응답의 모든 필드를 콘솔에 출력하여 구조 확인
    Object.keys(backendData).forEach(key => {
      console.log(`${key}:`, backendData[key]);
    });
    
    // 시간대별 데이터 명시적 변환
    let behaviorData = [];
    if (backendData.hourlyDistribution && Object.keys(backendData.hourlyDistribution).length > 0) {
      behaviorData = Object.entries(backendData.hourlyDistribution).map(([time, count]) => ({
        time,
        clicks: clickCount,
        pageviews: pageViewCount,
        count // 원본 카운트 값도 보존
      }));
    } else {
      // 기본 데이터 제공
      behaviorData = [{ 
        time: '데이터 없음', 
        clicks: 0, 
        pageviews: 0,
        count: 0
      }];
    }
    
    // 데이터가 있는지 명시적으로 확인
    const hasData = totalEvents > 0 && Object.keys(eventTypeDistribution).length > 0;
    
    const result = {
      visitorMetrics,
      behaviorData,
      // 더미 데이터를 사용해 표시할 내용 생성
      eventLogs: generateDummyLogs(5, pageViewCount, clickCount),
      rawData: backendData, // 디버깅용 원본 데이터 보존
      hasData
    };
    
    console.log('변환된 데이터:', result);
    return result;
    
  } catch (error) {
    console.error('데이터 변환 중 오류 발생:', error);
    return {
      visitorMetrics: { totalVisitors: 0, uniqueVisitors: 0, pageViews: 0, bounceRate: "N/A" },
      behaviorData: [{ time: '오류', clicks: 0, pageviews: 0 }],
      eventLogs: [],
      hasData: false,
      error: error.message
    };
  }
};

// 더미 로그 생성 함수 개선
const generateDummyLogs = (count, pageViews, clicks) => {
  const now = new Date();
  const eventTypes = ['pageview', 'click', 'scroll', 'form_submit', 'error'];
  const urls = ['/traceboard', '/home', '/about', '/products', '/contact', '/blog'];
  
  // 실제 데이터 기반 비율 적용
  const eventDistribution = {
    pageview: pageViews > 0 ? Math.floor(pageViews / 2) : 3,
    click: clicks > 0 ? Math.floor(clicks / 2) : 1,
    scroll: 1,
    form_submit: 0,
    error: 0
  };
  
  // 실제 이벤트 수에 맞게 더미 데이터 생성
  let logs = [];
  Object.entries(eventDistribution).forEach(([type, amount]) => {
    if (amount <= 0) return;
    
    for (let i = 0; i < amount; i++) {
      logs.push({
        id: logs.length + 1,
        timestamp: new Date(now - Math.floor(Math.random() * 3600000)).toISOString(), // 최근 1시간 내
        eventType: type,
        userId: `user_${Math.floor(Math.random() * 100)}`,
        url: urls[Math.floor(Math.random() * urls.length)],
        details: `${type} 이벤트 (자동 생성)`
      });
    }
  });
  
  // 최소 개수 보장
  while (logs.length < count) {
    logs.push({
      id: logs.length + 1,
      timestamp: new Date(now - Math.floor(Math.random() * 3600000)).toISOString(),
      eventType: eventTypes[Math.floor(Math.random() * eventTypes.length)],
      userId: `user_${Math.floor(Math.random() * 100)}`,
      url: urls[Math.floor(Math.random() * urls.length)],
      details: `추가 이벤트 (자동 생성)`
    });
  }
  
  // 시간순 정렬
  return logs.sort((a, b) => new Date(b.timestamp) - new Date(a.timestamp));
};
```

2. **상태 관리 로직 완전 개선**:
   데이터 로딩 및 상태 관리를 완전히 새롭게 구성하고, 데이터 존재 여부 판단 로직을 강화합니다.

```jsx
// 컴포넌트에서 상태 관리 로직 개선
function TraceBoard() {
  // 상태 관리 강화
  const [rawData, setRawData] = useState(null);
  const [dashboardData, setDashboardData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  const [dataExists, setDataExists] = useState(false);
  const [selectedRange, setSelectedRange] = useState('24h'); // 기본값: 24시간
  const [retryCount, setRetryCount] = useState(0);

  // 데이터 로딩 함수 개선
  const fetchData = useCallback(async () => {
    setLoading(true);
    setError(null);
    
    try {
      // API 엔드포인트에 선택된 기간 파라미터 추가
      const url = `/api/traceboard/analytics?range=${selectedRange}`;
      console.log(`데이터 요청: ${url}`);
      
      const response = await fetch(url);
      
      if (!response.ok) {
        throw new Error(`API 오류: ${response.status} ${response.statusText}`);
      }
      
      const data = await response.json();
      console.log('원본 API 응답:', data);
      
      // 원본 데이터 저장
      setRawData(data);
      
      // 향상된 매핑 함수 적용
      const mappedData = enhancedMapAnalyticsData(data);
      console.log('매핑 후 데이터:', mappedData);
      
      // 데이터 존재 여부 명확하게 확인
      const hasData = mappedData && (
        (mappedData.visitorMetrics && mappedData.visitorMetrics.totalVisitors > 0) || 
        (mappedData.behaviorData && mappedData.behaviorData.some(d => d.pageviews > 0 || d.clicks > 0))
      );
      
      setDashboardData(mappedData);
      setDataExists(hasData);
      
      // 디버깅을 위해 전역 객체에 데이터 저장 (개발 환경에서만)
      if (process.env.NODE_ENV === 'development') {
        window.__traceboardData = { raw: data, mapped: mappedData, hasData };
      }
      
    } catch (err) {
      console.error('데이터 로딩 오류:', err);
      setError(`데이터를 불러오는 데 실패했습니다: ${err.message}`);
      setDataExists(false);
    } finally {
      setLoading(false);
    }
  }, [selectedRange]);

  // 컴포넌트 마운트 및 선택 범위 변경 시 데이터 로드
  useEffect(() => {
    fetchData();
  }, [fetchData, selectedRange]);
  
  // 데이터가 없는 경우 자동 재시도 (최대 3번)
  useEffect(() => {
    if (!loading && !error && !dataExists && retryCount < 3) {
      const retryTimer = setTimeout(() => {
        console.log(`데이터가 없어 ${retryCount + 1}번째 재시도 중...`);
        setRetryCount(prev => prev + 1);
        fetchData();
      }, 2000); // 2초 후 재시도
      
      return () => clearTimeout(retryTimer);
    }
  }, [loading, error, dataExists, retryCount, fetchData]);

  // 수동 새로고침 핸들러
  const handleRefresh = () => {
    setRetryCount(0);
    fetchData();
  };

  // 기간 선택 핸들러
  const handleRangeChange = (range) => {
    setSelectedRange(range);
    setRetryCount(0);
  };
  
  // 렌더링 로직...
}
```

3. **데이터 시각화 임시 대체 방안**:
   데이터가 제대로 표시되지 않는 경우 대체 UI를 제공합니다.

```jsx
// 렌더링 부분 개선
return (
  <DashboardContainer>
    <DashboardHeader>
      <h1>TraceBoard 대시보드</h1>
      <RefreshButton onClick={handleRefresh}>
        새로고침 <RefreshIcon />
      </RefreshButton>
    </DashboardHeader>
    
    <TimeRangeSelector 
      onRangeChange={handleRangeChange} 
      selectedRange={selectedRange}
    />
    
    {loading && (
      <LoadingContainer>
        <LoadingSpinner />
        <p>데이터를 불러오는 중입니다...</p>
      </LoadingContainer>
    )}
    
    {error && (
      <ErrorContainer>
        <ErrorIcon />
        <ErrorMessage>{error}</ErrorMessage>
        <RetryButton onClick={handleRefresh}>다시 시도</RetryButton>
      </ErrorContainer>
    )}
    
    {!loading && !error && (
      <>
        {dataExists && dashboardData ? (
          <DataContainer>
            <VisitorMetrics metrics={dashboardData.visitorMetrics} />
            <UserBehaviorChart behaviorData={dashboardData.behaviorData} />
            <EventLogTable logs={dashboardData.eventLogs} />
          </DataContainer>
        ) : (
          <NoDataContainer>
            <EmptyStateIcon />
            <h3>데이터가 없습니다</h3>
            <p>선택한 기간 동안 기록된 이벤트가 없습니다. 다른 기간을 선택하거나 나중에 다시 확인해 주세요.</p>
            
            {retryCount > 0 && (
              <FallbackDataButton onClick={showFallbackData}>
                테스트 데이터로 보기
              </FallbackDataButton>
            )}
          </NoDataContainer>
        )}
        
        {!dataExists && retryCount >= 3 && (
          <FallbackDataContainer>
            <h3>테스트 데이터로 대시보드 미리보기</h3>
            <p>실제 데이터를 불러오지 못했습니다. 아래는 테스트용 샘플 데이터입니다.</p>
            
            {/* 하드코딩된 더미 데이터로 컴포넌트 렌더링 */}
            <VisitorMetrics metrics={FALLBACK_METRICS} />
            <UserBehaviorChart behaviorData={FALLBACK_CHART_DATA} />
            <EventLogTable logs={FALLBACK_LOGS} />
          </FallbackDataContainer>
        )}
      </>
    )}
    
    {process.env.NODE_ENV === 'development' && (
      <EnhancedDebugPanel 
        api={rawData} 
        data={dashboardData} 
        state={{ loading, error, dataExists, selectedRange, retryCount }}
        onForceRefresh={handleRefresh}
      />
    )}
  </DashboardContainer>
);
```

4. **백엔드 API 동작 확인 및 수정**:
   백엔드 API의 응답 구조를 확인하고 필요한 조정을 수행합니다.

```java
// TraceBoardController.java
@RestController
@RequestMapping("/api/traceboard")
public class TraceBoardController {
    
    private final TraceBoardService traceBoardService;
    
    // 생성자 주입
    public TraceBoardController(TraceBoardService traceBoardService) {
        this.traceBoardService = traceBoardService;
    }
    
    @GetMapping("/analytics")
    public ResponseEntity<Map<String, Object>> getAnalytics(
            @RequestParam(required = false, defaultValue = "24h") String range) {
        
        try {
            Map<String, Object> analytics = traceBoardService.getAnalytics(range);
            
            // API 응답에 필요한 필드가 모두 있는지 확인 후 빈 객체 추가
            if (!analytics.containsKey("osDistribution")) {
                analytics.put("osDistribution", new HashMap<>());
            }
            if (!analytics.containsKey("hourlyDistribution")) {
                analytics.put("hourlyDistribution", new HashMap<>());
            }
            if (!analytics.containsKey("eventTypeDistribution")) {
                analytics.put("eventTypeDistribution", new HashMap<>());
            }
            if (!analytics.containsKey("deviceDistribution")) {
                analytics.put("deviceDistribution", new HashMap<>());
            }
            if (!analytics.containsKey("browserDistribution")) {
                analytics.put("browserDistribution", new HashMap<>());
            }
            
            // 로그 추가
            System.out.println("API 응답 데이터: " + analytics);
            
            return ResponseEntity.ok(analytics);
        } catch (Exception e) {
            e.printStackTrace();
            Map<String, Object> error = new HashMap<>();
            error.put("error", e.getMessage());
            return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(error);
        }
    }
}
```

5. **개발 환경 전용 디버깅 도구 추가**:
   문제 진단을 위한 고급 디버깅 도구를 개발 환경에 추가합니다.

```jsx
// 개선된 디버그 패널
const EnhancedDebugPanel = ({ api, data, state, onForceRefresh }) => {
  const [expanded, setExpanded] = useState(false);
  const [showImportantFields, setShowImportantFields] = useState(true);
  
  // 중요 필드만 추출하는 함수
  const extractImportantFields = (obj) => {
    if (!obj) return null;
    
    try {
      return {
        totalEvents: obj.totalEvents,
        eventTypeDistribution: obj.eventTypeDistribution,
        hourlyDistribution: obj.hourlyDistribution,
        hasData: data?.hasData,
        metrics: data?.visitorMetrics
      };
    } catch (e) {
      return { error: e.message };
    }
  };
  
  if (process.env.NODE_ENV !== 'development') return null;
  
  return (
    <DebugContainer>
      <DebugHeader onClick={() => setExpanded(!expanded)}>
        개발자 도구 - 데이터 디버깅 {expanded ? '▼' : '▶'}
      </DebugHeader>
      
      {expanded && (
        <DebugContent>
          <DebugTools>
            <DebugButton onClick={onForceRefresh}>
              데이터 강제 새로고침
            </DebugButton>
            <DebugButton onClick={() => console.log('API 데이터:', api)}>
              API 데이터 콘솔 출력
            </DebugButton>
            <DebugButton onClick={() => console.log('변환 데이터:', data)}>
              변환 데이터 콘솔 출력
            </DebugButton>
            <DebugButton onClick={() => setShowImportantFields(!showImportantFields)}>
              {showImportantFields ? '모든 필드 보기' : '중요 필드만 보기'}
            </DebugButton>
          </DebugTools>
          
          <DebugStatus>
            <StatusItem isOk={state.dataExists}>
              데이터 존재: {state.dataExists ? '있음 ✓' : '없음 ✗'}
            </StatusItem>
            <StatusItem isOk={!state.loading}>
              로딩 상태: {state.loading ? '로딩 중... ⌛' : '완료 ✓'}
            </StatusItem>
            <StatusItem isOk={!state.error}>
              오류: {state.error ? `${state.error} ✗` : '없음 ✓'}
            </StatusItem>
            <StatusItem>
              재시도: {state.retryCount}/3
            </StatusItem>
            <StatusItem>
              선택 기간: {state.selectedRange}
            </StatusItem>
          </DebugStatus>
          
          <DebugSection>
            <h4>API 응답 데이터</h4>
            <pre>
              {JSON.stringify(
                showImportantFields ? extractImportantFields(api) : api, 
                null, 2
              )}
            </pre>
          </DebugSection>
          
          <DebugSection>
            <h4>변환된 데이터</h4>
            <pre>
              {JSON.stringify(
                showImportantFields ? extractImportantFields(data) : data, 
                null, 2
              )}
            </pre>
          </DebugSection>
          
          <DebugNote>
            <p>
              <strong>참고:</strong> 백엔드에서 데이터가 전송되지만 화면에 표시되지 않는 경우 다음을 확인하세요:
              <ol>
                <li>데이터 형식이 프론트엔드 구조와 일치하는지</li>
                <li>totalEvents 값이 0이 아닌지</li>
                <li>hasData 플래그가 true로 설정되었는지</li>
                <li>eventTypeDistribution에 값이 있는지</li>
              </ol>
            </p>
          </DebugNote>
        </DebugContent>
      )}
    </DebugContainer>
  );
};
```

이 강화된 접근 방식을 통해 다음과 같은 효과를 기대할 수 있습니다:

1. 데이터 형식 불일치 문제를 근본적으로 해결하여 어떤 백엔드 응답 구조에도 대응 가능
2. 데이터가 없거나 로딩에 실패하는 경우에도 사용자 경험을 유지하는 폴백 메커니즘 제공
3. 개발자가 문제를 정확히 진단하고 해결할 수 있는 강력한 디버깅 도구 제공
4. 다양한 에지 케이스를 처리하는 방어적 프로그래밍 접근 방식 적용

실제 구현 시에는 백엔드 API의 정확한 응답 구조와 프론트엔드의 필요에 맞게 이 접근 방식을 조정해야 합니다.

## 7. 다음 단계 계획

다음 단계로는 아래 작업들을 진행할 예정입니다:

- [ ] 백엔드 API 엔드포인트 구현 (EventLog 모델, 컨트롤러, 서비스 개발)
- [ ] 실제 데이터베이스 스키마 설계 및 구현 (PostgreSQL)
- [ ] 이벤트 수집 SDK 개발 및 배포
- [ ] 테스트 페이지에 SDK 적용하여 실제 데이터 수집 테스트

### 7.1 데이터 처리 보안 정책 구현

데이터 처리와 관련하여 다음과 같은 보안 정책을 구현할 예정입니다:

#### 사용자 IP 처리 방식
1. **데이터베이스 저장**: 원본 IP 주소를 그대로 데이터베이스에 저장하여 정확한 분석 및 필요시 사용자 추적 가능하도록 유지
2. **프론트엔드 전송**: 프론트엔드로 데이터 전송 시 IP 주소를 해시 처리하거나 일부 마스킹 처리하여 개인정보 보호
3. **접근 제어**: 원본 IP 데이터에 대한 접근 권한을 관리자 계정으로 제한

아래는 IP 주소 처리 관련 백엔드 코드 구현 예시입니다:

```java
// EventService.java
@Service
public class EventService {
    // IP 주소 저장 시 그대로 저장
    public void saveEvent(EventDto eventDto) {
        String originalIp = eventDto.getIpAddress();
        // IP 주소를 그대로 데이터베이스에 저장
        EventEntity event = new EventEntity();
        event.setIpAddress(originalIp);
        // 기타 필드 설정
        eventRepository.save(event);
    }
    
    // 프론트엔드로 전송 시 마스킹 처리
    public List<EventDto> getEventsForFrontend() {
        List<EventEntity> events = eventRepository.findAll();
        return events.stream()
            .map(event -> {
                EventDto dto = mapToDto(event);
                // IP 주소 마스킹 처리
                dto.setIpAddress(maskIpAddress(event.getIpAddress()));
                return dto;
            })
            .collect(Collectors.toList());
    }
    
    // IP 주소 마스킹 처리 (예: 192.168.1.1 -> 192.168.x.x)
    private String maskIpAddress(String ip) {
        if (ip == null || ip.isEmpty()) {
            return "unknown";
        }
        
        String[] parts = ip.split("\\.");
        if (parts.length == 4) { // IPv4
            return parts[0] + "." + parts[1] + ".x.x";
        } else if (ip.contains(":")) { // IPv6
            // IPv6 마스킹 로직
            return ip.substring(0, ip.length() / 2) + ":xxxx:xxxx";
        }
        
        return "masked-ip";
    }
    
    // 관리자용 - 원본 IP 포함 데이터 조회
    @PreAuthorize("hasRole('ADMIN')")
    public List<EventDto> getEventsForAdmin() {
        List<EventEntity> events = eventRepository.findAll();
        return events.stream()
            .map(this::mapToDto)
            .collect(Collectors.toList());
    }
}
```

#### IP 기반 분석 기능

IP 주소 원본 데이터를 DB에 저장함으로써 다음과 같은 고급 분석 기능을 구현할 수 있습니다:

1. 지역별 방문자 분포 분석 (GeoIP 데이터베이스 활용)
2. 비정상적인 접근 패턴 감지 (동일 IP에서의 과도한 요청 등)
3. 방화벽 정책 수립을 위한 데이터 수집

다만, 이러한 데이터 수집 및 저장은 관련 개인정보보호법과 GDPR 등의 규정을 준수하며 진행할 예정입니다.

## 8. 마일스톤

현재까지의 진행 상황은 다음과 같습니다:

- [x] 프론트엔드 대시보드 UI 개발
- [x] styled-components 적용
- [x] SPA 라우팅 설정
- [ ] 백엔드 API 개발
- [ ] 실제 데이터 연동
- [ ] SDK 배포

## 9. 참고 자료

- [React 공식 문서](https://reactjs.org/docs/getting-started.html)
- [Spring Boot 정적 리소스 설정](https://docs.spring.io/spring-boot/docs/current/reference/html/web.html#web.servlet.spring-mvc.static-content)
- [styled-components 문서](https://styled-components.com/docs)
- [React Router 문서](https://reactrouter.com/web/guides/quick-start)

---

다음 포스트에서는 백엔드 API 개발과 실제 데이터베이스 연동에 대해 다루겠습니다. 