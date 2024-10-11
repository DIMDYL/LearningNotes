## 依赖

``` xml
<!-- Swagger 2 -->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.9.2</version>
</dependency>
 
<!-- Swagger UI -->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>
```

## 配置

```java
@Configuration
@EnableSwagger2 // 开启Swagger
public class SwaggerConfig {
}
```

## 报错解决

出现引入Swagger为空异常处理方法

```java
spring.mvc.pathmatch.matching-strategy=ANT_PATH_MATCHER
```