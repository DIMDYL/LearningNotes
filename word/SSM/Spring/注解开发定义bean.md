## 定义bean

在实现类上使用@Component("userimpl")，可以不写名称，不写名称在获取bean的时候需要按类型来获取bean

 @Autowired：表示此处需要注入

```java
@Component("userimpl")
public class Userimpl implements User {
    @Autowired
    private Userdao userpl;
    @Override
    public void getuser() {
        System.out.println(userpl.userdap());
    }
}
```

## @Component 三个衍生注解

|    注解     |         说明         |            位置            |
| :---------: | :------------------: | :------------------------: |
| @Component  | 声明 bean的基础注解  | 不属于一下三类时，用此注解 |
| @Controller | @Component的衍生注解 |           控制器           |
|  @Service   | @Component的衍生注解 |           业务类           |
| @Repository | @Component的衍生注解 |         访问数据类         |

## XML配置

使用新开辟的context空间扫描bean

base-package：扫描bean范围

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd">
    <context:component-scan base-package="org.example"></context:component-scan>
</beans>
```

## 通过配置文件替换xml配置

#### 配置

@Configuration：配置类

@ComponentScan：扫描bean路径

```java
@Configuration // 表示为配置类
@ComponentScan("org.example") // 扫描bean路径
public class SpringConfig {
}
```

#### 使用

AnnotationConfigApplicationContext：注解配置

```java
public class Main {
    public static void main(String[] args) {
        // 加载配置类
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        Userimpl u =  ctx.getBean(Userimpl.class);
        u.getuser();
    }
}
```

## 在一个接口有两种实现方式的时候，并且都交给了IOC容器管理那么在运行的时候会报错 

解决：

bean名称默认是类型首字母小写

1. @Primary：表示优先级，在service逻辑处理类加上@Primary即可
2. @Qualifier("bean名")：指定注入的bean，在@Autowired 上方指定
3. @Resource(name = "userservice")：@Autowired 替换为@Resource，name指定注入的bean

## 读取配置文件

#### 配置文件配置

@PropertySource：需要读取的配置文件名可以多个用 , 隔开，不支持通配符

```java
@Configuration // 表示为配置类
@ComponentScan("org.example") // 扫描bean路径
@PropertySource("classpath:dim.properties") // 配置文件
public class SpringConfig {
}
```

#### dim.properties

```properties
user.name=dim
```

## 使用

 @Value：值，${user.name}的值映射到name这个属性中

```java
public class UserdaoImpl implements Userdao {
    @Value("${user.name}")
    private String name;
}
```