## 介绍

是一个声明式HTTP客户端，通过注解就可以发送HTTP请求

## 依赖

之前的负载均衡用的是Ribbon现在用的是loadbalancer

负载均衡中就包含了各种选服务的算法，不需要手写负载均衡了

```xml
<!-- openfegin -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
    <version>3.0.1</version>
</dependency>
<!-- 负载均衡器 -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-loadbalancer</artifactId>
</dependency>
```

## 启动类开启OpenFeign功能

EnableFeignClients：开启openFeign功能

```java
@MapperScan("com.hmall.mapper")
@SpringBootApplication
@EnableFeignClients
public class CartApplication {
    public static void main(String[] args) {
        SpringApplication.run(CartApplication.class, args);
    }
}
```

## 写接口

写一个请求接口，需要和调用的接口传参，url接口请求路径保持一致。

```java
@FeignClient("item-service")
public interface ItemClient {
    @GetMapping("/items")
    List<ItemDTO> getitems(@RequestParam("ids") Collection<Long> ids );
}
```

## 调用

调用这个接口，将需要的参数传入，OpenFeign会通过负载均衡选择调用的url，去请求这个接口

```java
private void handleCartItems(List<CartVO> vos) {
    Set<Long> itemIds = vos.stream().map(CartVO::getItemId).collect(Collectors.toSet());
    List<ItemDTO> items = itemClient.getitems(itemIds);
}
```

## 优化

OpenFeign是使用HTT PURLConnection实现的发送请求，是不支持连接池的

如果不使用连接池，每次请求都需要建立新的连接，无法使用之前的连接，浪费资源需要频繁的创建和销毁了连接。

## 整合OkHttp

#### 依赖

```xml
<dependency>
    <groupId>io.github.openfeign</groupId>
    <artifactId>feign-okhttp</artifactId>
</dependency>
```

#### 配置

开启连接池

```yml
feign:
  autoconfiguration:
    jackson:
      enabled: true
```