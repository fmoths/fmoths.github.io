---
layout: post
title: Spring Integration (2)
categories: Spring
tags: Spring
---

#### Spring Integration
>Message / Pipe / Filters
- Message
    - 전송할 데이터가 담긴 Wrapper Class
    - **Message**
- Pipes
    - Message Object를 발신 / 수신하기 위한 창구
    - **Message Channel**
- Filters
    - Message Object를 발신 / 수신하는 목적지
    - Message Endpoints
    - 참고로 앞에서 봤던 HTTP-outbound-gateway는 메세지 엔드포인트의 일종

    ![3main_components](https://image.slidesharecdn.com/springintegration-150420040755-conversion-gate02/95/spring-integration-36-638.jpg?cb=1429517566)

    ![main_components](https://image.slidesharecdn.com/springintegration-150420040755-conversion-gate02/95/spring-integration-37-638.jpg?cb=1429517566)

##### 1. Message
![Message_is](https://image.slidesharecdn.com/springintegration-150420040755-conversion-gate02/95/spring-integration-39-638.jpg?cb=1429517566)

- 메세지 구조
![Message_structure](https://image.slidesharecdn.com/springintegration-150420040755-conversion-gate02/95/spring-integration-40-638.jpg?cb=1429517566)

1) 직접 메세지 인스턴스화 진행
```java
import org.springframework.messaging.Message;
import org.springframework.messaging.support.GenericMessage;

Message<String> message1 = new GenericMessage<>("Hello");
Message<User> message2 = new GenericMessage<>(user);
```

2) 메세지빌더를 사용하여 메세지 오브젝트 생성
```java
Message<String> message1 = MessageBuilder.withPayload("Hello").build();

Message<User> message2 = MessageBuilder.withPayload(user).build();
```

##### 2. Message Channel

![Message_channel](https://image.slidesharecdn.com/springintegration-150420040755-conversion-gate02/95/spring-integration-43-638.jpg?cb=1429517566)
