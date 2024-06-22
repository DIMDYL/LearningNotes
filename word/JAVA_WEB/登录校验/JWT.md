## 令牌技术

优点：

1. 支持PC端、移动端
2. 解决集群环境下的认证问题
3. 减轻服务器端存储压力

缺点：需要自己实现

## 引入依赖

```xml
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.9.1</version>
</dependency>
```

## 生成Token：

signWith：加密算法于密钥

setClaims：设置map参数对象

setExpiration：有效期

System.currentTimeMillis()：当前系统时间

compact：压缩为JWT字符串

```java
@GetMapping("/jwt")
public Result token(){
    Map<String,Object> user = new HashMap<>();
    user.put("id",1);
    user.put("name","邓紫棋");
    String jwt =  Jwts.builder()
            .signWith(SignatureAlgorithm.HS256,"dimdim") // 签名算法
            .setClaims(user) // 设置数
            .setExpiration(new Date(System.currentTimeMillis() + 3600 * 1000)) // 设置有效期为1小时
            .compact();
    return Result.success(jwt);
}
```

## 解析Token

 HttpServletRequest：请求对象

getHeader：获取请求头

setSigningKey：加密密钥

parseClaimsJws：需要解析的token字符串

getBody：获取JWT主体部分

```java
@GetMapping("/token")
public Result jwt(HttpServletRequest request){
    String token =  request.getHeader("token");
    Claims c = Jwts.parser().setSigningKey("dimdim").parseClaimsJws(token).getBody();
    return Result.success(c);
}
```