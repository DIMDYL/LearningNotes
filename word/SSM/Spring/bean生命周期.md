## 生命周期配置

初始化容器：

1. 创建对象(内存分配)
2. 执行构造方法
3. 执行属性注入（seter）
4. 执行bean初始化方法

使用bean

1. 执行业务操作

关闭/销毁容器

1. 执行bean销毁方法

## XMl配置

init-method：初始化操作

destroy-method：销毁前操作

```xml
<bean id="userServiceimpl" class="org.example.service.UserServiceimpl" init-method="init" destroy-method="destory">
    <!-- 需要将dao的数据给service  -->
    <!-- 所以要配置 service于dao的关系  -->
    <!-- name是指在service中Userdao创建的对象名称-->
    <!-- ref指的是将哪个bean给这个对象 -->
    <property name="userDao" ref="dyl"></property>
</bean>
```

## Java中配置：

```java
// bean初始化操作
public void init(){
    System.out.println("init...");
}
// bean销毁前操作
public void destory(){
    System.out.println("destory...");
}
```

## 接口控制bena生命周期

在接口中实现 InitializingBean, DisposableBean，并重写对应方法

afterPropertiesSet：表示在将bean对象交给对应属性后（private UserDao userDao;设置的seter执行完后）

destroy：在bean销毁前

```java
// 在bean销毁前
@Override
public void destroy() throws Exception {
    System.out.println("销毁前");
}

@Override
public void afterPropertiesSet() throws Exception {
    System.out.println("属性设置后");
}
```