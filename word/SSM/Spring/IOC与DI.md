## IOC

IOC是将对象交给IOC容器管理，通过获取对应的bean来使用该对象从而降低耦合性

#### 配置XML

id表示bean的名称
class表示实现类的全类名

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="userServiceimpl" class="org.example.service.UserServiceimpl"></bean>
    <bean id="userDaoImpl" class="org.example.dao.impl.UserDaoImpl"></bean>
</beans>
```

#### 使用IOC容器中的对象

这里没有创建userServiceimpl的对象

而是通过获取userServiceimpl的bean来使用userServiceimpl对象

ApplicationContext：管理bean的接口

ClassPathXmlApplicationContext：配置文件路径

getBean：获取bean，返回的是一个Object对象可以抓换为想要的对象

```java
public class Main {
    public static void main(String[] args) {
        // 获取IOC容器
        ApplicationContext ctx = new ClassPathXmlApplicationContext("beans.xml");
        // 获取bean
        UserService userServiceimpl = (UserService)ctx.getBean("userServiceimpl");
        System.out.println(userServiceimpl.Getuser());
    }

}
```

## DI

配置bean于bean之间的关系

#### 实现类配置

userDao就是在xml中要交给name属性的值表示将对应的ref实现类赋值给这给属性

注意要创建对应的seter方法不然bean管理器不知道给谁

```java
package org.example.service;

import org.example.dao.UserDao;
import org.example.dao.impl.UserDaoImpl;

public class UserServiceimpl implements UserService{
    private UserDao userDao;
    @Override
    public String Getuser() {
        return userDao.getuser();
    }

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }
}
```

#### XML配置

目前是两个bean

service是数据处理，dao是数据层

所以目前的关系是service依靠于dao层的数据，在service中会有创建dao层的对象这个过程

所以现在要将dao层的userDao这个实现类(userDaoImpl)交给 在userServiceimpl中创建是userDaoImpl对象名称(userDao)

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="userServiceimpl" class="org.example.service.UserServiceimpl">
        <!-- 需要将dao的数据给service  -->
        <!-- 所以要配置 service于dao的关系  -->
        <!-- name是指在service中Userdao创建的对象名称-->
        <!-- ref指的是将哪个bean给这个对象 -->
        <property name="userDao" ref="userDaoImpl"></property>
    </bean>
    <bean id="userDaoImpl" class="org.example.dao.impl.UserDaoImpl"></bean>
     <!-- 如果是单例类使用factory-method获取静态方法即可 -->
    <bean id="demo02" class="org.example.ioc.demo02" factory-method="getDemo02"></bean>
</beans>
```