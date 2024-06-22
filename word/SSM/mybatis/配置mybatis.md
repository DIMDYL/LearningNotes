## 注意

mybatis中的事务是默认开启的，所有想要自动提交事务在需要的适合再开事务需要openSession()中传入true即可

## 依赖

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.5</version>
</dependency>
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.9</version>
</dependency>
```

## xml配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!-- mybatis约束 -->
<!-- configuration根标签 -->
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!-- 设置驼峰命名 -->
    <settings>
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>
    <!-- 配置连接数据库环境 -->
    <environments default="development">
        <environment id="development">
            <!-- 事务管理器类型 -->
            <transactionManager type="JDBC"/>
            <!-- 数据源 -->
            <dataSource type="POOLED">
                <!-- 驱动 -->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://127.0.0.1:3306/cangqiongwaimai"/>
                <!-- 用户名 -->
                <property name="username" value="cangqiongwaimai"/>
                <!-- 密码 -->
                <property name="password" value="cangqiongwaimai"/>
            </dataSource>
        </environment>
    </environments>
    <!-- 引入映射文件 -->
    <mappers>
        <mapper resource="mappers/UserMapper.xml"/>
    </mappers>
</configuration>
```


## 核心配置

```java
// 核心配置文件
// 以字节输入流获取，返回一个字节输入流获取
InputStream resourceAsStream = Resources.getResourceAsStream("mybatis-config.xml");

// 提供SqlSession工厂的构建对象
SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();

// 使用SqlSessionFactoryBuilder对象从字节输入流中构建SqlSessionFactory
SqlSessionFactory build = sqlSessionFactoryBuilder.build(resourceAsStream);

// 获取mybatis操作数据库的操作对象
// SqlSession：java和数据库之间的会话
SqlSession sqlSession = build.openSession(true);

// 从SqlSession中获取mapper接口的实现
UserMapper mapper = sqlSession.getMapper(UserMapper.class);

// 调用mapper接口方法
UserEntity findbyid = mapper.Findbyid(1);
System.out.println(findbyid);

// 提交事务
sqlSession.commit();

// 关闭SqlSession
sqlSession.close();

// 关闭字节输入流
resourceAsStream.close();
```
