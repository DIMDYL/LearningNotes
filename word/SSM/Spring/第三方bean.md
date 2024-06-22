## 管理第三方bean

@Bean：返回一个bean

如果注入简单类型可以直接使用@Value()

如果是引用类型需要在对应方法上传入引用类型形参

spring在运行的时候会去根据形参类型需要对应的bean，如果能找到对应类型的bean直接使用不然就会报错

```java
@PropertySource("classpath:dim.properties") // 配置文件
public class JdbcConfig {
    @Value("${Driver}")
    private String driverClassName;
    @Value("${jdbc}")
    private String url;
    @Value("${jdbcUser}")
    private String password;
    @Value("${jdbcpass}")
    private String username;
    // @bean表示返回一个bean
    @Bean
    public DataSource dataSource(UserdaoImpl userdao){
        System.out.println(userdao.userdap());
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName(driverClassName);
        dataSource.setUrl(url);
        dataSource.setPassword(password);
        dataSource.setUsername(username);
        return dataSource;
    }
}

```
@Import：导入配置

```java
@Configuration
@ComponentScan("org.example")
@PropertySource("classpath:dim.properties") // 配置文件
@Import(JdbcConfig.class)
public class SpringConfig {
}
```

配置文件

```properties
user.name=dim
user.role=1
user.password=123321
Driver = com.mysql.jdbc.Driver
jdbc=jdbc:mysql://locahost:3306/spring_db
jdbcUser=root
jdbcpass=123321
```