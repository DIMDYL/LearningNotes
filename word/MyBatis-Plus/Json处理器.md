## Json处理器

将表中存储的字符串转换为java对应的实体对象

autoResultMap：自动映射，不需要自己自定义返回类型了

typeHandler：类型抓器

UserInfo：是一个对象

```java
@TableName(value = "user", autoResultMap = true)
public class User implements Serializable {
    @TableField(value = "info", typeHandler = JacksonTypeHandler.class)
    private UserInfo info;
}
```