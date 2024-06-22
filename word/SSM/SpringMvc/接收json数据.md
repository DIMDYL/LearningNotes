## 依赖

1. **jackson-core**: 提供了JSON解析器和生成器的核心功能。它包含了处理JSON数据所需的基本类和接口，比如`JsonParser`和`JsonGenerator`等。
2. **jackson-databind**: 提供了将JSON数据和Java对象相互转换的功能。它包含了`ObjectMapper`类，可以方便地将Java对象序列化为JSON字符串，或将JSON字符串反序列化为Java对象。
3. **jackson-annotations**: 提供了一些注解，用于在Java类上指定如何将Java对象序列化为JSON字符串以及如何将JSON字符串反序列化为Java对象。例如，`@JsonInclude`注解可以指定在序列化时是否包含空值属性。

```java
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-core</artifactId>
      <version>2.13.0</version> <!-- 版本号根据您的需要进行调整 -->
    </dependency>
        
        <!--- 只需要导入这个即可，databind包含core，annotations-->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.13.0</version> <!-- 版本号根据您的需要进行调整 -->
    </dependency>
        
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-annotations</artifactId>
      <version>2.13.0</version> <!-- 版本号根据您的需要进行调整 -->
    </dependency>
```

## SpringMVC配置

@EnableWebMvc：可以将json格式的数据转换为对应的对象（其中的一个功能）

```java
@Configuration
@ComponentScan("cn.z2z.controll")
@EnableWebMvc // json转换对象
public class SpringMvcConfig  {
}
```

## 使用

@Controller：用于处理HTTP请求。它通常与@RequestMapping一起使用，用于标识处理请求的类。

@RequestMapping：设置类的请求统一路径

@ResponseBody：返回响应体

@RequestBody：请求体中获取参数，一个处理器只能一次

@PostMapping：POST请求，请求路径是/d

```java
@Controller
@RequestMapping("/user")
public class User {
    @PostMapping("/d")
    @ResponseBody
    public String Dim(@RequestBody UserDTO dto){
        System.out.println(dto);
        return dto.getName();
    }
}
```