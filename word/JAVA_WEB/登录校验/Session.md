## Session

优点：存储在服务端安全

缺点：

1. 服务器集群环境下无法直接使用Session
2. Cookie的缺点

 Session底层实现原理是基于Cookie的，浏览器第一次请求服务器会创建一个Session对象，每一个Session都有一个编号SessionID

在服务器响应的时候会设置一个Cookie，JSESSIONID=服务器会话对象SessionID

在请求服务器的时候浏览器会设置请求头JSESSIONID=服务器会话对象SessionID，与之关联

如果浏览器在拥有了Session会话对象，那么就会直接使用不需要重新创建在服务端，在请求的时候会关联于之关联的Session对象

## 服务端设置Session

 HttpSession：Session响应对象

setAttribute：存储数据

```java
@GetMapping("/s1")
public Result s1(HttpSession session){
    session.setAttribute("user","GEMDIM");
    return Result.success();
}
```

## 浏览器发起请求获取存储的Session对象相关信息

HttpServletRequest：请求对象

getSession：Session会话对象

getAttribute：获取服务端存储在Session中的数据

```java
@GetMapping("/s2")
public Result s2(HttpServletRequest request){
    HttpSession session = request.getSession();
    System.out.println(session.getAttribute("user"));
    return Result.success();
}
```