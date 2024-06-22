### 第一个sprigboot程序

在创建完Springboot项目后，会出来一个类叫 项目名+Application.java  是Springboot项目的启动类

### 创建一个请求处理类

创建一个请求处理类和创建一个普通类一样只不过需要使用 RestController 注解标注这时一个请求处理类

RestController：标注为求处处理类

RequestMapping：指定请求路径

启动项目运行 项目名+Application.java 即可，运行后项目会启动一个端口默认为8080

``` java
package org.example.demo01.demo01;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.HashMap;
import java.util.Map;

// 加上 RestController 表示这是一个请求处理类
@RestController
public class demo01 {
    // RequestMapping 指定亲求路径
    @RequestMapping("/hello")
    public Map hello(){
        Map<String,String> m = new HashMap<>();
        m.put("D","1");
        m.put("D1","2");
        m.put("D2","3");
        return m;
    }
}
```

