## 介绍

面向切面编程、面向方面编程，其实就是面对特定的方法编程

## 引入依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

## 核心概念

连接点：joinPoint可以被AOP控制的方法

通知：重复的逻辑，共用的功能实现的方法

切入点：那些方法可以被AOP控制就是切入点

## 编写AOP程序

@Around：切入点，就是哪些包的类或者接口需要执行公共代码

@Aspect：表示当前类是一个AOP类

ProceedingJoinPoint：表示当前方法对象

joinPoint.proceed()：调用当前方法

joinPoint.getSignature()：获取当前方法的方法名，返回类型，参数

```java
@Component
@Aspect // 表示当前类是一个AOP类
@Slf4j
public class ddemo01 {
    //    通用逻辑
    @Around("execution(* org.example.spsp.conteall.*.*(..))") // 切入点
    public Object recordTIme(ProceedingJoinPoint joinPoint) throws Throwable {
        // 记录开始时间
        Long start = System.currentTimeMillis();
        // 调用原始方法
        Object result = joinPoint.proceed();
        // 记录结束时间
        Long end = System.currentTimeMillis();
        log.info(joinPoint.getSignature()+"程序执行使用了{}毫秒",end-start);
        return result;
    }
}
```

## 连接点：

在Around中使用ProceedingJoinPoint，在其他通知类型中使用JoinPoint

```java
public Object d(ProceedingJoinPoint joinPoint) throws Throwable {
     // 获取目标对象的类型
     // getTarget：获取目标对象
     log.info("类名：{}", joinPoint.getTarget().getClass().getName());
     // 获取目标独享的方法名
     // getSignature：获取方法签名
     log.info("方法名{}",joinPoint.getSignature().getName());
     // 获取方法运行传递的参数
     log.info("传递的参数{}",joinPoint.getArgs());
     // joinPoint.proceed() 调用目标方法
     return joinPoint.proceed();
 }
```
