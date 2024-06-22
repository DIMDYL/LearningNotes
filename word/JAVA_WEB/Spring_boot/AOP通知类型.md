## 意事项

@Around需要自己调用joinPoint.proceed()来执行原始方，其他通知不需要考虑原始方法执行

@Around环绕通知的返回值必须是Object，来接收原始原始方法的返回值，将原始方法的返回值返会后才能完成响应

## 通知执行顺序

不同切面中，默认是按照切面类的名称字母排序，目前方法的通知方法字母排名越靠前就越先执行

使用@Order来指定执行顺序，数字越小越先执行

```java
@Component
@Aspect // 表示当前类是一个AOP类
@Slf4j
@Order(1)
public class ddemo01 {
    @Pointcut("execution(* org.example.spsp.conteall.*.*(..))")
    private void pt(){}
    //    通用逻辑
    @Around("pt()") // 切入点
   public Object d(ProceedingJoinPoint joinPoint) throws Throwable {
        log.info("方法执行前");
        Object proceed = joinPoint.proceed();
        log.info("方法执行后");
        return proceed;
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
@AfterThrowing("execution(* org.example.spsp.conteall.*.*(..))") // 切入点
public void d() {
	log.info("执行了");
}
 
```

