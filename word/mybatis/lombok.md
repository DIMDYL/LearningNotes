## 介绍

Lombok是一个实用的java类，能通过注解的形式来自动创建构造器、gteer/seter、equals、hashcode、tostring等方法。并可以自动生成日志变量简化java开发提升效率

| 注解                     | 作用                                                         |
| ------------------------ | ------------------------------------------------------------ |
| @Getter @Setter          | 为变量赋予get、set方法。默认生成public方法                   |
| @ToString                | 该注解应用在类上，为我们生成Object的toString方法，而该注解里面的几个属性能更加丰富我们想要的内容，exclude属性禁止在toString方法中使用某字段，而of可以指定需要使用的字段： @ToString(exclude = {“a”, “b”}, of = {“c”, “lombok”}) |
| @EqualsAndHashCode       | 自动重写equals和hashcode方法                                 |
| @Data                    | 提高了更综合的生成代码功能（@Geter+@Seter+@Tostring+@EqualsAndHashCode） |
| @RequiredArgsConstructor | 为实体类生成无参的构造器方法                                 |
| @AllArgsConstructor      | 为实体类生成除了static修饰的字段之外的个参数的构造器方法     |

## 引入依赖

```xml
<dependency>
  <groupId>org.projectlombok</groupId>
   <artifactId>lombok</artifactId>
</dependency>
```

## 使用

```java 
@Data
public class User {
    private int id;
    private String username;
    private String password;
}
```