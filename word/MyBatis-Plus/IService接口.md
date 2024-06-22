## IService接口

IService接口提供了很多的方法操作Mapper，不需要自己写Mapper了

其中封装的方法由前缀命名方式区分，可以分为以下几类：
**`save`：**   新增
**`remove`：** 删除
**`update`：** 更新
**`get`：**   查询单个结果
**`list`：**  查询集合结果
**`count`：** 计数
**`page`：**  分页查询

## 使用IService

service的接口需要继承IService并且要指定泛型为表实体类

因为我们自己的service接口继承了一个接口那么我们自己的Service实现类就需要实现自定义的方法和IService中的方法

IService提供了一个 ServiceImpl的方法我们只需要继承他就可以实现IService接口的全部方法了

ServiceImpl类需要指定两个泛型：

第一个是表的Mapper接口。也就是需要操作的表的Mapper

第二个是表的实体类

这样就完成了对IService的配置，简单的SQL就不需要我们自己写了

```java
public interface UserService extends IService<UserEntiy> {
}
-------------------------------
@Service
public class UserSericeImpl extends ServiceImpl<UserMapper, UserEntiy> implements UserService {
}
```

## 使用IService接口简单开发

lambdaUpdate：更新数据，一定要在结尾调用.update()不然不会执行

lambdaQuery()：查询数据，也需要在结尾添加one或者list这样的查询

```java
lambdaUpdate().eq(UserEntiy::getId,1).set(UserEntiy::getPassword,"DZ").update();
List<UserEntiy> list = lambdaQuery().eq(UserEntiy::getId, 1).list();
```