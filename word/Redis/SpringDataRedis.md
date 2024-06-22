## SpringDataRedis

支持JDK、json、字符串、Spring对象的数据序列化和反序列化

## 依赖

SpringDataRedis依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

连接池依赖

```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-pool2</artifactId>
</dependency>
```

## 配置

```yml
spring:
  redis:
    host: 127.0.0.1 # ip
    port: 6379 # 端口
    lettuce: # 连接池
      pool:
        max-active: 8 # 最大连接数
        max-idle: 8 # 最大空闲连接
        min-idle: 0 # 最小空闲连接
        max-wait: 100 # 连接等待时间
```

## redis类型封装

```java
ValueOperations value = redisTemplate.opsForValue(); // 字符串
HashOperations hashOperations = redisTemplate.opsForHash(); // hash
ListOperations listOperations = redisTemplate.opsForList(); // 列表
SetOperations setOperations = redisTemplate.opsForSet(); // set
ZSetOperations zSetOperations = redisTemplate.opsForZSet(); // 有序列表
```

## 序列化器

#### 依赖

SpringDataRedis使用的时jackson序列化工具

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
</dependency>
```

redisTemplate默认的序列化时转换为字节，所以存储的时候不易识别，查询

在从redis中获取值的时候可以将数据反序列化为对应的对象

```java

@Configuration
public class RedisConfig {
    @Bean
    public RedisTemplate redisTemplate(RedisConnectionFactory factory){
        RedisTemplate redisTemplate = new RedisTemplate();
        redisTemplate.setConnectionFactory(factory); // 设置工厂
        // 序列化字符串和hash的key为字符串
        redisTemplate.setKeySerializer(new StringRedisSerializer());
        redisTemplate.setHashKeySerializer(new StringRedisSerializer());
        // 序列化字符串和hash的val为json
        redisTemplate.setHashValueSerializer(new GenericJackson2JsonRedisSerializer());
        redisTemplate.setValueSerializer(new GenericJackson2JsonRedisSerializer());
        return redisTemplate;
    }
}
```

在写入redis的时候会写入对象的类型的包（将value序列化为json的情况下）

``` json
{
    "@class":"java.util.HashMap",
    "name":"DIM"
}
```

