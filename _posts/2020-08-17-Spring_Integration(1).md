---
layout: post
title: Spring Integration (1)
categories: Spring
tags: Spring
---

#### What is Spring Integration?

- 각 서버마다 통신기법은 다를 수 있다.

1. Restful API 통신 구현1 (Jakarta HTTP Client)
```java
//1. 준비
String url = "http://example.com/point/1";
HttpClient client = new HttpClient();
GetMethod method = new GetMethod(url);
```

```java
//2. 실행
int statusCode = client.executeMethod(method);
if(statusCode != HttpStatus.SC_OK){...}
```

```java
//3. 결과반환
byte[] responseBody = method.getResponseBody();
method.releaseConnection();
```

2. Restful API 통신 구현2 (Spring Framework의 RestTemplate)

```java
//1. 준비

RestTemplate restTemplate = new RestTemplate();
String uri = "http://example.com/point/{id}";
UriComponents uriComponents = UriComponentsBuilder.fromUriString(uri);
    .build();
    .expand("41");
    .encode();
URI uri = uriComponents.toUri();
```
```java
//2. 실행 & 결과 반환
Point point = restTemplate.getForObject(url, Point.class);
```

3. Restful API 통신 구현3 (Spring Integration Framwork)

```java
public interface PointRequestGateway {
    Point getPoint(String id);
}
```
```xml
<int:channal id="requestChannel" />
<int:gateway
    id="requestGateway"
    service-interface="integration.PointRequestGateway"
    default-request-channel="requestChannel"/>
<int-http:outbound-gateway
    request-channel-"requestChannel"
    url="http://example.com/point/"
    http-method="GET"
    expected-response-type="java.lang.String"/>
```
```java
@Autowired
PointRequestGateway gateway;
Point point = gateway.getPoint("41");
```

#### -> 비지니스 로직과 통신로직을 분리할 수 있다.

#### Why Spring Integration?
1. 간편한 설정
- XML/Java DSL을 이용한 간편한 Infrastructure 구축
2. 익숙한 환경
- Spring Framwork의 IoC, DI 사용
3. 다양한 Connectivity
- 다양한 통신 기술에 대한 Adapter 및 Infrastructure 제공



출처 : https://www.slideshare.net/WangeunLee/spring-integration-47185594
