## Knife4j

java mvc框架继承Swagger生成API文档的增强解决方案

## 依赖

```
<dependency>
    <groupId>com.github.xiaoymin</groupId>
    <artifactId>knife4j-spring-boot-starter</artifactId>
</dependency>
```

## 注解使用

@Api(tags = "xxx")：用在类上例如controller类上，表示对类的说明

@ApiOperation(value = "xxx")：在controller的方法上使用表示方法的用途和作用

@ApiModel(description = "xxx")：在类上使用，DTO、VO、Entity

@ApiModelProperty("XXX")：在方法上使用，表示方法的用途、作用