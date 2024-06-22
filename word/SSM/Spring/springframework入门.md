## 什么是BeanFactory

BeanFactory就是bean工厂， 用来分配bean

想要使用bean就要由在配置清单中寻找这个bena类的配置

## 入门案例

在resources中创建一个beans.xml的文件用于配置bean

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="userServiceimpl" class="org.example.impl.UserServiceImpl"></bean>
</beans>
```

#### 使用：

```java
// 创建一个工厂对象
DefaultListableBeanFactory beanFactory = new DefaultListableBeanFactory();
// 创建一个xml读取器
XmlBeanDefinitionReader reader = new XmlBeanDefinitionReader(beanFactory);
// 读取配置文件给工厂
reader.loadBeanDefinitions("beans.xml");
// 根据id获取bean实例对象
UserService userServiceimpl = (UserService)beanFactory.getBean("userServiceimpl");
System.out.println(userServiceimpl);
```