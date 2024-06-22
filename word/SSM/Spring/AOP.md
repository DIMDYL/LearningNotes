## 导入spring整合AOP依赖

注意：使用aop最终放入的对象不是原本的对象而是jdk动态代理创建的类，如果想要获取bean只能通过接口

```java
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>6.0.11</version>
</dependency>
```

## 切面优先级

@Order指定数值越大优先级越小，默认是最大值，数值越小优先级越高

```java
@Component
@Aspect
@Order(10)
public class Aop {
    @Before("execution(* cn.z2z.demo.demo01.dim())")
    public void dimd(JoinPoint joinPoint) throws Throwable {
        System.out.println("dimd");
    }
}
```

## 注解配置文件

**@EnableAspectJAutoProxy注解在Spring框架中的主要作用是启用AspectJ的自动代理功能**。这意味着，开发者可以使用AspectJ的注解（如@Aspect、@Before、@After等）在Spring Bean中实现切面编程，而不需要手动定义代理对象。

```java
@Configuration
@ComponentScan("cn.z2z")
@EnableAspectJAutoProxy
public class Config {
}
```

## 使用

声明一个切面，连接点是cn.z2z.demo.demo01.dim())在方法运行前执行

```java
@Component
@Aspect
public class Aop {
    @Before("execution(* cn.z2z.demo.demo01.dim())")
    public void dimd(JoinPoint joinPoint) throws Throwable {
        System.out.println("dimd");
    }
}
```

## 通知类型

@Around：环绕通知，在调用方法前和调用方法后都会执行

```java
@Around("execution(* org.example.spsp.conteall.*.*(..))") // 切入点
public Object d(ProceedingJoinPoint joinPoint) throws Throwable {
    log.info("方法执行前");
    Object proceed = joinPoint.proceed();
    log.info("方法执行后");
    return proceed;
}
```

@After：在调用方法后执行，无论是否有异常都会执行

```java
@After("execution(* org.example.spsp.conteall.*.*(..))") // 切入点
public void d() {
	log.info("执行了");
}
```

@Before：在调用方法前执行

```java
@Before("execution(* org.example.spsp.conteall.*.*(..))") // 切入点
public void d() {
	log.info("执行了");
}
```

@AfterReturning：返回方法后执行，有异常不会执行

```JAVA
@AfterReturning("execution(* org.example.spsp.conteall.*.*(..))") // 切入点
public void d() {
	log.info("执行了");
}
```

@AfterThrowing：在方法发生异常时执行

```java
@AfterThrowing("execution(* org.example.spsp.conteall.*.*(..))", throwing = "x")
public void dimd(JoinPoint joinPoint, Throwable x) throws Throwable {
    System.out.println("dimd");
}
 
```
