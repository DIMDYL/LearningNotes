## 生成于解析JWT

signWith：加密方式于密钥

setClaims：存储数据

setExpiration：过期时间

compact：返回一个实体jwt

parser：解析

setSigningKey：解密密钥

parseClaimsJws：解析的JWT

getBody：获取主体部分

```java
package rog.studymybatis.springbootanli1.utils;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;

import java.util.Date;
import java.util.Map;

public class Jwtutils{
    public static String getjwt(Map<String, Object> map){
        String jwt =  Jwts.builder()
                .signWith(SignatureAlgorithm.HS256, "dimdyl") // 加密方式于密钥
                .setClaims(map)
                .setExpiration(new Date(System.currentTimeMillis() + 3306 * 1000)) // 过期时间
                .compact();
        return jwt;
    }
    public static Claims parsejwt(String jwt){
        return Jwts.parser()
        .setSigningKey("dimdyl") // 解密密钥
        .parseClaimsJws(jwt) // 需要解析的token
        .getBody(); //获取jwt主体部份  ;
    }
}
```