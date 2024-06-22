## controller加载控制于业务bean加载控制

SpringMVC只加载controller的bean

而Spring需要加载servidce、mybatis整合、dao等bean（Spring扫描的包范围一般很大）

所以要避免Spring在扫描bean的时候需要避免加载SpringMVC的Bean

## 解决

SpringMVC依然加载controller包内的bean

Spring的解决：

1. Spring加载的时候设定范围为cn.z2z，排除掉 cn.z2z.controller这个包
   ```java
   @Configuration
   @ComponentScan(value = "cn.z2z",excludeFilters = @ComponentScan.Filter( // 过滤
           type = FilterType.ANNOTATION, // 过滤类型，以注解的形式
           classes = Controller.class // 指定注解
   ))
   ```

   

2. Spring加载的时候设置更精准的扫描，例如：service、dao包等
   ```java
   @ComponentScan({"cn.z2z.service","cn.z2z.dao"}) // 精准扫描指定的包
   ```

   



