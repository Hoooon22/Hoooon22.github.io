---
layout: default
title: TraceBoard 프론트엔드 및 백엔드 연동 구현
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2025-04-09 20:10:49 
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

**원인 분석**:
1. 데이터 형식 불일치: 백엔드에서 받아온 데이터 구조와 프론트엔드 컴포넌트가 기대하는 데이터 구조가 일치하지 않는 문제
2. 상태 관리 문제: 데이터를 성공적으로 가져왔으나 React 컴포넌트의 상태로 올바르게 설정되지 않는 문제
3. 렌더링 조건 문제: 데이터가 있음에도 조건부 렌더링이 잘못 적용되어 "데이터가 없습니다" 메시지가 표시되는 문제
4. 권한 정책 오류: 'browsing-topics' 기능과 관련된 Permissions-Policy 헤더 오류가 발생하여 데이터 처리에 영향을 미치는 문제

**해결 방안**:

1. **데이터 매핑 함수 수정**:
   백엔드에서 받아온 데이터를 프론트엔드 컴포넌트가 이해할 수 있는 형식으로 변환하는 매핑 함수를 개선합니다.

```jsx
// 백엔드 데이터를 프론트엔드 컴포넌트용 형식으로 변환
const mapAnalyticsData = (backendData) => {
  if (!backendData || typeof backendData !== 'object') {
    console.error('유효하지 않은 데이터 형식:', backendData);
    return null;
  }
  
  // 방문자 지표 데이터 매핑
  const visitorMetrics = {
    totalVisitors: backendData.totalEvents || 0,
    uniqueVisitors: Object.values(backendData.deviceDistribution || {}).reduce((a, b) => a + b, 0),
    pageViews: ((backendData.eventTypeDistribution || {}).pageView || 0) + ((backendData.eventTypeDistribution || {}).pageview || 0), // 대소문자 고려
    bounceRate: "0%" // 추후 계산 로직 추가 예정
  };
  
  // 시간대별 데이터 매핑 - 빈 배열이 아닌지 확인
  const hourlyData = Object.entries(backendData.hourlyDistribution || {});
  const behaviorData = hourlyData.length > 0 
    ? hourlyData.map(([time, count]) => ({
        time,
        clicks: (backendData.eventTypeDistribution || {}).click || 0,
        pageviews: ((backendData.eventTypeDistribution || {}).pageView || 0) + ((backendData.eventTypeDistribution || {}).pageview || 0)
      }))
    : [{ time: '데이터 없음', clicks: 0, pageviews: 0 }]; // 기본값 제공
  
  // 이벤트 로그 매핑 (상세 로그 데이터가 없는 경우 더미 데이터 사용)
  let eventLogs = [];
  if (backendData.events && Array.isArray(backendData.events) && backendData.events.length > 0) {
    eventLogs = backendData.events.map(event => ({
      timestamp: event.timestamp || new Date().toISOString(),
      eventType: event.type || 'unknown',
      userId: event.userId || 'anonymous',
      url: event.url || '/',
      details: JSON.stringify(event.details || {})
    }));
  } else {
    // 최소 5개의 더미 데이터 생성
    eventLogs = generateDummyLogs(5);
  }
  
  console.log('매핑된 데이터:', { visitorMetrics, behaviorData, eventLogs });
  
  return {
    visitorMetrics,
    behaviorData,
    eventLogs,
    hasData: visitorMetrics.totalVisitors > 0 || behaviorData.some(d => d.pageviews > 0 || d.clicks > 0)
  };
};
```

2. **조건부 렌더링 로직 개선**:
   데이터 존재 여부를 더 정확하게 확인하고, 빈 데이터에 대한 처리를 개선합니다.

```jsx
// Dashboard 컴포넌트 내부
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);
const [dashboardData, setDashboardData] = useState(null);
const [dataExists, setDataExists] = useState(false);

useEffect(() => {
  const fetchData = async () => {
    try {
      setLoading(true);
      const response = await fetch('/api/traceboard/analytics');
      
      if (!response.ok) {
        throw new Error(`API 오류: ${response.status} ${response.statusText}`);
      }
      
      const data = await response.json();
      console.log('서버에서 데이터를 성공적으로 가져왔습니다:', data);
      
      // 데이터 매핑 함수 적용
      const mappedData = mapAnalyticsData(data);
      setDashboardData(mappedData);
      
      // 실제 데이터 존재 여부 확인
      setDataExists(mappedData && mappedData.hasData);
      setError(null);
    } catch (err) {
      console.error('데이터 로딩 중 오류 발생:', err);
      setError('데이터를 불러오는 데 실패했습니다. 잠시 후 다시 시도해주세요.');
      setDataExists(false);
    } finally {
      setLoading(false);
    }
  };
  
  fetchData();
}, []);

// 렌더링 부분
return (
  <DashboardContainer>
    <h1>TraceBoard 대시보드</h1>
    
    <TimeRangeSelector 
      onRangeChange={handleTimeRangeChange} 
      selectedRange={selectedTimeRange}
    />
    
    {loading && <LoadingSpinner />}
    
    {error && <ErrorMessage>{error}</ErrorMessage>}
    
    {!loading && !error && dataExists && dashboardData && (
      <>
        <VisitorMetrics metrics={dashboardData.visitorMetrics} />
        <UserBehaviorChart behaviorData={dashboardData.behaviorData} />
        <EventLogTable logs={dashboardData.eventLogs} />
      </>
    )}
    
    {!loading && !error && !dataExists && (
      <NoDataMessage>
        <EmptyStateIcon />
        <h3>데이터가 없습니다</h3>
        <p>선택한 기간 동안 기록된 이벤트가 없습니다. 다른 기간을 선택하거나 나중에 다시 확인해 주세요.</p>
      </NoDataMessage>
    )}
  </DashboardContainer>
);
```

3. **권한 정책 헤더 문제 해결**:
   Permissions-Policy 헤더 오류를 해결하기 위해 Spring 서버 설정을 수정합니다.

```java
// SecurityConfig.java 또는 WebConfig.java에 추가
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new HandlerInterceptor() {
            @Override
            public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) {
                // browsing-topics 기능을 제외한 Permissions-Policy 설정
                response.setHeader("Permissions-Policy", 
                    "accelerometer=(), autoplay=(), camera=(), display-capture=(), " +
                    "encrypted-media=(), fullscreen=(), geolocation=(), gyroscope=(), " +
                    "microphone=(), midi=(), payment=(), usb=()");
                return true;
            }
        }).addPathPatterns("/**");
    }
}
```

4. **데이터 초기화 및 정리 로직 추가**:
   컴포넌트 마운트/언마운트 시 데이터를 적절히 처리하는 로직을 추가합니다.

```jsx
// 컴포넌트 마운트/언마운트 처리
useEffect(() => {
  // 컴포넌트 마운트 시 초기 데이터 로드
  fetchData();
  
  // 5분마다 데이터 갱신
  const intervalId = setInterval(fetchData, 5 * 60 * 1000);
  
  // 컴포넌트 언마운트 시 리소스 정리
  return () => {
    clearInterval(intervalId);
    // 필요시 상태 초기화
    setDashboardData(null);
    setDataExists(false);
  };
}, []);
```

5. **디버깅 도구 확장**:
   더 상세한 디버깅을 위해 개발 환경에서 사용할 수 있는 향상된 디버그 패널을 구현합니다.

```jsx
// 개발 환경에서만 표시되는 강화된 디버그 패널
const EnhancedDebugPanel = ({ data, api, state }) => {
  const [expanded, setExpanded] = useState(false);
  
  if (process.env.NODE_ENV !== 'development') return null;
  
  return (
    <DebugContainer>
      <DebugHeader onClick={() => setExpanded(!expanded)}>
        디버그 정보 {expanded ? '▼' : '▶'}
      </DebugHeader>
      
      {expanded && (
        <DebugContent>
          <DebugSection>
            <h4>API 응답 데이터</h4>
            <pre>{JSON.stringify(api, null, 2)}</pre>
          </DebugSection>
          
          <DebugSection>
            <h4>변환된 데이터</h4>
            <pre>{JSON.stringify(data, null, 2)}</pre>
          </DebugSection>
          
          <DebugSection>
            <h4>컴포넌트 상태</h4>
            <pre>{JSON.stringify(state, null, 2)}</pre>
          </DebugSection>
          
          <DebugActions>
            <button onClick={() => console.log('원본 API 데이터:', api)}>콘솔에 API 데이터 출력</button>
            <button onClick={() => console.log('변환된 데이터:', data)}>콘솔에 변환 데이터 출력</button>
          </DebugActions>
        </DebugContent>
      )}
    </DebugContainer>
  );
};

// 스타일 컴포넌트 정의
const DebugContainer = styled.div`
  margin-top: 30px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background: #f8f8f8;
`;

// 메인 컴포넌트에 추가
{process.env.NODE_ENV === 'development' && !loading && (
  <EnhancedDebugPanel 
    api={originalApiData} 
    data={dashboardData} 
    state={{ loading, error, dataExists }}
  />
)}
```

이러한 개선사항을 적용하면 다음과 같은 효과를 기대할 수 있습니다:

1. 백엔드에서 제공하는 다양한 데이터 형식에 더 강건하게 대응
2. 데이터 존재 여부를 정확하게 판단하여 적절한 UI 표시
3. 권한 정책 관련 오류 제거로 브라우저 호환성 향상
4. 개발 중 문제 원인 파악이 용이해짐

다음 개발 세션에서는 이 해결 방안들을 구현하고 실제 환경에서 테스트하여 데이터 시각화가 정상적으로 이루어지도록 하겠습니다.

## 7. 다음 단계 계획

다음 단계로는 아래 작업들을 진행할 예정입니다:

- [ ] 백엔드 API 엔드포인트 구현 (EventLog 모델, 컨트롤러, 서비스 개발)
- [ ] 실제 데이터베이스 스키마 설계 및 구현 (PostgreSQL)
- [ ] 이벤트 수집 SDK 개발 및 배포
- [ ] 테스트 페이지에 SDK 적용하여 실제 데이터 수집 테스트

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