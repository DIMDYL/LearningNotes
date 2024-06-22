## 配置起步依赖

web、myabtis、mysql驱动、lombok

## application.properties 配置

#### 驱动配置：

```properties
# 驱动类名称
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
# 连接数据库的url
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/demo01
# 用户名
spring.datasource.username = demo01
# 密码
spring.datasource.password = demo01
```

#### mybatis日志输出在控制台

```properties
mybatis.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
```

#### 开启xml驼峰映射

```properties
mybatis.configuration.map-underscore-to-camel-case=true
```

## XML配置

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="全类名">
</mapper>
```

## 响应规范模板

```java
package rog.studymybatis.springbootanli1.pojo;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class Result {
    private int code; // 响应码，1代表成功，0代表失败
    private String msg; // 响应信息
    private Object Data; // 返回数据
    public static Result success(){ // 增删改 响应成功
        return new Result(1,"success",null);
    }
    public static Result success(Object Data){ // 查询成功 返回数据
        return new Result(1,"success",Data);
    }
    public static Result success(String msg){ // 失败响应
        return new Result(1,msg,null);
    }
}
```