## bean的别名配置

通过name关键字设置别名，多个别名使用  ,  隔开

```java
<bean id="userServiceimpl" class="org.example.service.UserServiceimpl">
        <!-- 需要将dao的数据给service  -->
        <!-- 所以要配置 service于dao的关系  -->
        <!-- name是指在service中Userdao创建的对象名称-->
        <!-- ref指的是将哪个bean给这个对象 -->
        <property name="userDao" ref="dyl"></property>
    </bean>
    <bean id="userDaoImpl" name="dim, dyl" class="org.example.dao.impl.UserDaoImpl"></bean>
</beans>
```

## bean 的可用范围

bean默认创建的对象是单例对(意思就是永远是同一个对象)

scope：配置所用范围

prototype：非单例

singleton：单例（默认）

```xml
<bean id="userDaoImpl" name="dim, dyl" class="org.example.dao.impl.UserDaoImpl" scope="prototype"></bean>
```

## 为什么默认是单例bean？

因为不是单例的IOC难以管理，其实IOC管理的就是那些可以复用的bean