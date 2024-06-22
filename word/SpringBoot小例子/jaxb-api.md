## 故障

使用JDK 11.0 环境下,使用JwtUtil 生成token异常.
java.lang.NoClassDefFoundError

## 故障原因：

JAXB API是java EE 的API，因此在java SE 9.0 中不再包含这个 Jar 包。
java 9 中引入了模块的概念，默认情况下，Java SE中将不再包含java EE 的Jar包
而在 java 6/7 / 8 时关于这个API 都是捆绑在一起的

## 手动加入这些依赖Jar包

```xml
<dependency>
    <groupId>javax.xml.bind</groupId>
    <artifactId>jaxb-api</artifactId>
    <version>2.3.1</version>
</dependency>
```