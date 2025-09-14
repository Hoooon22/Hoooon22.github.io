---
layout: default
title: Live Chat 프로젝트 개발일지
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
date: 2025-09-14 17:57:40
---

# 📝 Live Chat 프로젝트 개발일지

### 1. 들어가며: 왜 실시간 채팅 프로젝트인가?

현대 웹 애플리케이션에서 실시간 상호작용은 사용자 경험을 극대화하는 핵심 요소입니다. 다양한 서비스에 손쉽게 통합할 수 있는 독립적인 실시간 채팅 기능을 구현하여, 서비스 운영자와 사용자, 또는 사용자 간의 원활한 소통 채널을 제공하는 것을 목표로 Live Chat 프로젝트를 시작했습니다. 이 프로젝트를 통해 어떤 웹 서비스든 쉽게 가져다 쓸 수 있는 범용성 높은 채팅 모듈 개발을 목표로 합니다.

### 최종 구현 화면

<img src="../../../../assets/images/devzip/스크린샷 2025-09-14 오후 6.01.06.png" alt="Live Chat 구현 화면">
<img src="../../../../assets/images/devzip/스크린샷 2025-09-14 오후 6.01.53.png" alt="Live Chat 채팅방 구현 화면">

### 2. 기술 스택 선택: WebSocket과 STOMP

실시간 양방향 통신을 위해 **WebSocket**을 기술 기반으로 선택했습니다. 하지만 순수 WebSocket API(Plain WebSocket)는 메시지 형식이나 통신 흐름을 직접 모두 구현해야 하는 부담이 있었습니다.

**고민의 지점:**

*   **구현의 복잡성:** 누가 메시지를 보내고, 누가 받는지, 어떤 종류의 메시지인지 등을 모두 직접 파싱하고 관리해야 했습니다.
*   **통신 프로토콜의 부재:** 일관성 있는 메시지 포맷을 유지하기 위한 별도의 프로토콜 설계가 필요했습니다.

**해결책:**

이러한 복잡성을 줄이고 개발 생산성을 높이기 위해, WebSocket 위에서 동작하는 상위 프로토콜인 **STOMP(Simple Text Oriented Messaging Protocol)**를 도입하기로 결정했습니다. Spring에서는 `@EnableWebSocketMessageBroker` 어노테이션 하나로 STOMP 기반의 메시지 브로커 기능을 손쉽게 활성화할 수 있었습니다.

`WebSocketConfig.java`의 핵심 설정은 다음과 같습니다.

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        // 1. 구독(Subscribe) 경로 설정
        registry.enableSimpleBroker("/topic");
        // 2. 발행(Publish) 경로 설정
        registry.setApplicationDestinationPrefixes("/app");
    }

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        // 3. 웹소켓 연결 Endpoint 설정
        registry.addEndpoint("/ws-livechat").setAllowedOriginPatterns("*").withSockJS();
    }
}
```

**고민과 결정의 결과:**

1.  **`/topic` (구독):** 클라이언트가 메시지를 수신할 채널의 prefix입니다. 특정 채팅방의 주제(topic)를 구독하면, 해당 방의 메시지를 받을 수 있습니다.
2.  **`/app` (발행):** 클라이언트가 서버로 메시지를 보낼 때 사용하는 prefix입니다. 이 경로로 들어온 메시지는 `@MessageMapping` 어노테이션이 붙은 컨트롤러 메서드로 라우팅됩니다.
3.  **`/ws-livechat` (연결):** 최초 웹소켓 연결을 위한 Endpoint입니다. `withSockJS()`를 추가하여 WebSocket을 지원하지 않는 브라우저에서도 유사한 경험을 제공할 수 있도록 호환성을 높였습니다.

이처럼 STOMP를 도입함으로써, '발행/구독(Pub/Sub)' 모델을 직관적으로 사용할 수 있게 되어 채팅방별 메시지 분리, 메시지 브로드캐스팅 등의 로직을 매우 간단하게 구현할 수 있었습니다.

### 3. 메시지 처리 흐름 설계

STOMP로 통신 기반을 다진 후, 클라이언트가 보낸 메시지를 서버에서 어떻게 처리하고 다시 클라이언트로 전달할지 구체적인 흐름을 설계했습니다.

`LiveChatMessageController.java` 와 `LiveChatMessageRequest.java` DTO는 이러한 고민의 결과물입니다.

**고민의 지점:**

*   **메시지 라우팅:** `/app/livechat/message` 경로로 들어온 메시지를 어떻게 특정 채팅방 구독자들에게만 전달할 것인가?
*   **데이터 처리:** 클라이언트가 보낸 원본 데이터를 그대로 사용할 것인가, 아니면 서버에서 필요한 형태로 가공할 것인가?
*   **메시지 영속성:** 실시간으로 주고받는 메시지를 데이터베이스에 저장해야 하는가?

**설계 및 구현:**

```java
// LiveChatMessageController.java
@MessageMapping("/livechat/message")
public void message(LiveChatMessageRequest messageRequest) {
    // 1. 채팅방 존재 여부 확인
    LiveChatRoom room = liveChatRoomRepository.findById(messageRequest.getRoomId())
            .orElseThrow(() -> new RuntimeException("Chat room not found"));

    // 2. DTO를 Entity로 변환 및 저장
    LiveChatMessage chatMessage = new LiveChatMessage();
    chatMessage.setLiveChatRoom(room);
    chatMessage.setSenderName(messageRequest.getSenderName());
    chatMessage.setMessage(messageRequest.getMessage());
    LiveChatMessage savedMessage = liveChatMessageRepository.save(chatMessage);

    // 3. 해당 채팅방 구독자들에게 메시지 브로드캐스팅
    messagingTemplate.convertAndSend("/topic/room/" + messageRequest.getRoomId(), savedMessage);
}
```

1.  **DTO 도입:** `LiveChatMessageRequest` 라는 DTO를 만들어 클라이언트와 서버 간의 데이터 규격을 명확히 했습니다. 이를 통해 API 스펙과 데이터베이스 모델(Entity)을 분리하여 유연성을 확보했습니다.
2.  **메시지 저장:** 컨트롤러 내부에 `// For simplicity, we're not creating a full service layer for this part yet.` 라는 주석을 남긴 것을 발견했습니다. 이는 MVP(Minimum Viable Product) 개발 방식으로, 우선 핵심 기능을 컨트롤러에 빠르게 구현하고 추후 서비스 레이어로 분리하여 리팩토링하겠다는 의사결정의 흔적입니다. 이런 접근은 초기 개발 속도를 높이는 데 큰 도움이 됩니다.
3.  **브로드캐스팅:** `SimpMessageSendingOperations`를 사용하여 `/topic/room/{roomId}` 경로를 구독하고 있는 모든 클라이언트에게 메시지를 전송합니다. STOMP 덕분에 이 과정이 매우 간단해졌습니다.

### 4. 인증 및 안정성 강화

초기 구현 이후, 인증(Authentication) 문제를 해결하고 안정성을 높이는 과정을 진행했습니다.

*   **`Principal` 객체 null 처리:** 웹소켓 연결 시, 인증된 사용자의 정보를 가져오는 `Principal` 객체가 null이 되는 문제를 해결했습니다. 이는 웹소켓 연결 컨텍스트에 Spring Security의 인증 정보가 제대로 전달되지 않았을 때 발생하는 문제로, JWT 토큰을 웹소켓 핸드셰이크 과정에서 검증하는 로직을 추가하여 해결했을 것으로 추측됩니다.
*   **비로그인 사용자 접근 제어:** 로그인하지 않은 사용자가 채팅방에 접근하려고 할 때, 알림을 표시하고 입장을 막는 기능을 추가하여 서비스 안정성을 높였습니다.
*   **연결 상태 표시:** 클라이언트가 웹소켓 서버와 정상적으로 연결되었는지 알 수 있도록 UI에 연결 상태를 표시하는 기능을 추가하여 사용자 경험을 개선했습니다.

### 5. 결론 및 향후 과제

이번 Live Chat 기능 개발을 통해 STOMP를 활용한 효율적인 실시간 메시징 시스템의 기반을 구축했습니다. 특히, MVP 방식으로 빠르게 핵심 기능을 구현하고 점진적으로 리팩토링하는 전략은 매우 유효했습니다.

**남은 과제:**

*   **서비스 레이어 분리:** 현재 컨트롤러에 있는 비즈니스 로직을 별도의 서비스 레이어로 분리하여 역할과 책임을 명확히 해야 합니다.
*   **보안 강화:** 개발 편의를 위해 `setAllowedOriginPatterns("*")`로 설정했던 CORS 정책을 실제 서비스 도메인에 맞게 강화해야 합니다.
*   **상태 관리 고도화:** 현재 접속자 목록, 사용자별 읽음 처리 등 실시간 상태 관리를 위한 로직을 Redis 등을 활용하여 고도화할 필요가 있습니다.
*   기타 등등 ...
