## 依赖

```xml
<!-- mysql驱动 -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.9</version>
</dependency>
<!-- mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.1</version>
</dependency>
<!-- spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.5.RELEASE</version>
</dependency>
<!-- spring整合mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>1.3.0</version>
</dependency>
<!-- 阿里的连接池 -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.12</version>
</dependency>
```

## SpringConfig

spring配置类
ComponentScan：扫描cn.z2z的bean

PropertySource：读取配置文件

Import：引入配置

```java
@Configuration
@ComponentScan("cn.z2z")
@PropertySource("jdbcconfig.properties")
@Import({JdbcConfig.class,MybatisConfig.class})
public class SpringConfig {
}
```

## JdbcConfig

整合durid数据源

```java
public class JdbcConfig {
    @Value("${db.Driver}")
    private String Driver;
    @Value("${db.username}")
    private String username;
    @Value("${db.password}")
    private String password;
    @Value("${db.url}")
    private String url;
    @Bean
    public DataSource dataSource(){
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setUsername(username);
        dataSource.setPassword(password);
        dataSource.setDriverClassName(Driver);
        dataSource.setUrl(url);
        return dataSource;
    }
}
```

## MybatisConfig

使用mybatis整合包的SqlSessionFactoryBean整合mybatis

将数据源DataSource注入返回

```java
public class MybatisConfig {
    @Bean
    public SqlSessionFactoryBean sqlSessionFactory(DataSource dataSource){
        // spring整合mybatis
        SqlSessionFactoryBean ssfb = new SqlSessionFactoryBean();
        // 于数据库对应的实体包名
        ssfb.setTypeAliasesPackage("cn.z2z.pojo");
        // 设置MyBatis配置
        org.apache.ibatis.session.Configuration configuration = new org.apache.ibatis.session.Configuration();
        configuration.setMapUnderscoreToCamelCase(true); // 设置驼峰命名规则
        sqlSessionFactoryBean.setConfiguration(configuration);
        // 设置数据库连接信息
        ssfb.setDataSource(dataSource);
        return ssfb;
    }
    // 扫描mapper操作数据库的xml文件
    @Bean
    public MapperScannerConfigurer mapperScannerConfigurer(){
        MapperScannerConfigurer m = new MapperScannerConfigurer();
        // mapper全类名
        m.setBasePackage("cn.z2z.mapper");
        return m;
    }
}
```