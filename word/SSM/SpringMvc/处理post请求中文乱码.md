## 设置编码

在servlet容器中重写getServletFilters并设置编码格式

```javas
// 定义一个Servlet容器启动配置类，加载Spring的配置
public class ServletConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    // Spring配置类
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0];
    }
    // SpringMVC配置
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class};
    }
    // 设置那些请求归SpringMVC管理
    @Override
    protected String[] getServletMappings() {
        return new String[]{"/"};
    }
    // 处理中文乱码
    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter d = new CharacterEncodingFilter();
        d.setEncoding("UTF-8");
        return new Filter[]{d};
    }
}
```

## tomcat这只编码

 < uriEncoding>UTF-8< /uriEncoding>：设置编码，在控制台

```java
<build> 
  <plugins> 
    <plugin> 
      <groupId>org.apache.tomcat.maven</groupId>  
      <artifactId>tomcat7-maven-plugin</artifactId>  
      <version>2.1</version>  
      <configuration> 
        <port>90</port>  
        <path>/</path>
        <uriEncoding>UTF-8</uriEncoding>
      </configuration> 
    </plugin> 
  </plugins> 
</build> 
```