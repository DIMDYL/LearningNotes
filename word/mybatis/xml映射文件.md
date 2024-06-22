## 规范

XML映射文件的名称与Mapper接口名称一致，并且将XML映射文件和Mapper接口放置在相同包下（同包同名）

XML映射文件的namespace属性为Mapper接口全类名一致

XML映射文件中sql语句的id与Mapper接口中的发方法名一致，并保持返回类型一致

## XML基础文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper  namespace="rog.studymybatis.stydumybatis1.mapper">
</mapper>
```

## 简单案例：

#### xml：

创建与接口同名的xml文件：

1. 需要同包同名：在resources创建 rog/studymybatis/stydumybatis1/mapper然后创建与接口名称相同的xml文件

这里的id是接口中的抽象方法名称

resultType: 单条记录所封装的类型

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper  namespace="rog.studymybatis.stydumybatis1.mapper.UserMapper">
<!-- resultType: 单条记录所封装的类型    -->
    <select id="GetUser" resultType="rog.studymybatis.stydumybatis1.pojo.User">
        select * from usee where id = #{id}
    </select>
</mapper>
```
