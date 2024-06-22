## Cookie

优点：HTTP协议中支持的技术

缺点：

1. 移动端APP无法使用cookie
2. 不安全用户可以自己禁用cookie
3. Cookie不能跨域

## 服务端设置Cookie

服务端在响应头中设置cookie浏览器端会自动存储

HttpServletResponse：响应对象

Cookie：cookie对象

addHeader：添加响应头

```java
@GetMapping
public Result Getget(HttpServletResponse response){
    response.addCookie(new Cookie("token","XXXXXX"));
    response.addHeader("dimdim","DIDMI");
    return Result.success();
}
```

## 客户端返回cookie

客户端将本地的cookie请求时返回给访问端

HttpServletRequest：请求对象

Cookie：cookie对象

getCookies：获取所有cookie

```
@GetMapping("/1")
public Result get1(HttpServletRequest request){
    Cookie[] cookies = request.getCookies(); // 获取所有的Cookie
    for (Cookie cookie : cookies){
        if (cookie.getName().equals("token")){
            log.info(cookie.getName());
            log.info(cookie.getValue());
        }
    }
    return Result.success();
}
```