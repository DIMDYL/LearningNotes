## 自定义SQL

在开发中，不允许在service去写操数据的代码

操作数据规范就是在Mapper中写

在MybatisPlus中可以使用自定义sql的形式来拼接sql实现在Mapper中写操作数据的操作

#### 步骤

1. 在service中将条件构造器传给mapper
2. mapper需要使用@param("ew")来指定名称，只能是ew
3. 在xml中或者注解中拼接sql ${ew.customSqlSegment}

```java
// server
LambdaQueryWrapper<UserEntiy> list = new LambdaQueryWrapper<>();
String[] arr = {"1","2"};
list.in(UserEntiy::getId,arr);
List<UserEntiy> selebyid = userMapper.selebyid(list);
// mapper
List<UserEntiy> selebyid(@Param("ew") LambdaQueryWrapper<UserEntiy> list);
// mapper XML文件
<select id="selebyid" resultType="cn.mytodolist.day01.pojo.entity.UserEntiy">
    select * from user ${ew.customSqlSegment}
</select>

```