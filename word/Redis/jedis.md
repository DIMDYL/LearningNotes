## jedis

#### 依赖

```xml
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>3.7.0</version>
</dependency>
```

## 连接

适合用BeforeEach注解的原因就是在执行test测试的时候创建好Jedis的对象

```java
@SpringBootTest
class DemoApplicationTests {
    private Jedis jedis;
    // 单元测试前执行
    @BeforeEach
    void contextLoads() {
        // 建立连接
        jedis = new Jedis("127.0.0.1",6379);
        // 密码
//        jedis.auth("123321");
        // 选择库
        jedis.select(0);
    }
    @Test
    void TextRedis(){
        jedis.set("DIM","10");
        String s = jedis.get("DIM");
        System.out.println(s);
    }
    @AfterEach // 在执行test之后
    void close(){
        // 释放
        if (jedis != null){
            jedis.close();
        }
    }
}
```

## Jedis连接池

Jedis是线程不安全的，并且频繁创建和销毁会有性能的损失，更推荐使用Jedis的连接池来操作

#### 为什么要在静态代码块中创建连接池

静态代码块中的代码只会执行一次，不管创建多少个这个对象的实例，这个代码块内的数据只属于这个类

静态代码是线程安全的

```java
public class JedsConnectionFactory {
    // 定义为final不会每次都创建一个对象，保证每次调用都是同一个对象
    private static final JedisPool jedisPool;
    static { // static代码块的代码只会执行一次，保证了唯一性不会多次创建这个对象了
        JedisPoolConfig jedisPoolConfig = new JedisPoolConfig();
        // 最大连接数
        jedisPoolConfig.setMaxTotal(8);
        // 最大空限
        jedisPoolConfig.setMaxIdle(8);
        // 最小连接数
        jedisPoolConfig.setMinIdle(0);
        // 最长等待时间 ms
        jedisPoolConfig.setMaxWaitMillis(1000);
                                 // 连接池配置     // ip // 端口  // 超时 时间
        jedisPool = new JedisPool(jedisPoolConfig,"127.0.0.1",6379,1000);
    }
    // 获取jedis对象
    public static Jedis getJedis(){
        return jedisPool.getResource();
    }
}
```

#### 使用

```java
package com.example.demo;

import com.example.demo.config.JedsConnectionFactory;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;
import redis.clients.jedis.Jedis;

import java.util.HashMap;
import java.util.Map;

@SpringBootTest
class DemoApplicationTests {
    private Jedis jedis;
    // 单元测试前执行
    @BeforeEach
    void contextLoads() {
        // 通过连接池获取jedis
        jedis = JedsConnectionFactory.getJedis();

    }
    @Test
    void TextRedis(){
        jedis.hset("s2","name","DDD");
        System.out.println(jedis.hgetAll("s2"));
    }
    @AfterEach // 在执行test之后
    void close(){
        // 释放
        if (jedis != null){
            jedis.close();
        }
    }
}
```