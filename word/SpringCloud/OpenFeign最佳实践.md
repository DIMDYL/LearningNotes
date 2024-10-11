## 最佳实践1

在需要被查询的微服务中定义三个模块：

在需要调用的微服务中引入（dto、api）模块即可实现调用client接口进行查询该微服务中

xxx-dto：查询参数

xxx-api：client接口

xxx-biz：当前微服务的业务代码

#### 弊端

项目结构复杂，一个微服务变成了3个模块

![image-20240911090145001](../../\img\QQ20240911-090656.png)

## 最佳实践2

创建一个单独的模块去管理Client和DTO

cloent：存储每一个微服务中想要暴露的接口

DTO：存储每一个微服务中公共访问的DTO

在使用的时候直接引入通用的模块即可，耦合度会高

![image-20240911090145001](../../\img\QQ20240911-091248.png)

## 使用

在api管理模块中创建公共client、DTO

#### 依赖

在api管理模块中需要引入openfeign、loadbalancer

```xml
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

## 引入模块

在需要使用公共client的POM中引入

```xml
<dependency>
    <groupId>com.heima</groupId>
    <artifactId>hm-api</artifactId>
    <version>1.0.0</version>
</dependency>
```

## 包问题

因为公共模块中的包名和当前需要引入的模块包名是不一样的，所有需要指定扫描一下

basePackages：指定扫描包路径

```java
@MapperScan("com.hmall.mapper")
@SpringBootApplication
@EnableFeignClients(basePackages = "com.hmall.api.Client")
public class CartApplication {
    public static void main(String[] args) {
        SpringApplication.run(CartApplication.class, args);
    }
}
```