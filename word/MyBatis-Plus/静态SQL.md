## 静态sql

静态sql是IService接口中提供的

用于处理循环依赖的问题

例如：

表：user、book

查询：

在user表中需要获取user表指定id的book表中的数据

在book表中需要获取book指定id的user表中的数据

问题：

那么现在就出现了循环依赖了，互相都要注入对方的Service层

解决：

使用静态SQL只需要传入对应的实体类的字节码就可以进行表的操作

``` java
@Override
public getbook get() {
    Book Book = Db.getById(1, Book.class);
    return Book;
}
```

## 版本

只有在最新版本中才会出现Db模块

```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.5.3</version>
</dependency>
```

## getOne()

指定一个实体设置属性值根据属性值做查询条件

```java
UserEntity userEntity = new UserEntity();
userEntity.setPhoneNumber(authorizedlearnersDTO.getPhoneNumber());
QueryWrapper<UserEntity> wrapper = new QueryWrapper<>(userEntity);
UserEntity user = Db.getOne(wrapper);
```
