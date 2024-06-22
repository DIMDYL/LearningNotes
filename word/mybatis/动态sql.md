在开发中会遇到搜索的情况，搜索可以输入很多值如：姓名、班级等，如果使用常规sql班级传入null，会查询不到值

```java
select * from user where name = "dim" and class = null
```

## < if>

使用if判断是否满足条件如果满足条件才会拼接条件，不然不会拼接

如果下列是不满足的执行的sql就是 select * from usee where  1 = 1

```xml
<select id="GetUser" resultType="rog.studymybatis.stydumybatis1.pojo.User">
    select * from usee
        where
            <if test="id != null">
                id = #{id}
            </if>
        and
            1 = 1
</select>
```

## < where>

< where>标签用于动态生成where关键字，如果里面的条件都不满足连where都不会生成

会自动处理and和or关系，如果全面的不满足会自动去除

```xml
<select id="GetUser" resultType="rog.studymybatis.stydumybatis1.pojo.User">
    select * from usee
    <where>
        <if test="id == 1">
             id = #{id}
        </if>
        <if test="id == 3">
           and id = #{id}
        </if>
    </where>
</select>
```

## 案例：动态更新用户信息

修改用户名称和用户密码，有时候用户只修改用户名或者只修改密码，所以要使用动态sql

< set>可以动态删除语句后面的 , 

```
<update id="UpdateUser">
    update usee
        <set>
            <if test="username != null">
                username = #{username},
            </if>
            <if test="password != null">
                password = #{password},
            </if>
        </set>
    where id = #{id}
</update>
```

## < foreach>

collection 便利的集合

item: 变量名

separator：分隔符

open：开始前添加的符号

close：结束后添加的符号

```
    <delete id="DeleteUser">
        delete from usee where id in
        <foreach collection="userlist" item="id"  separator="," open="("  close=")">
            #{id}
        </foreach>
    </delete>
```

## < sel>与< include>

在查询的时候 select * 执行慢建议将所有字段罗列出来，但是每次查询所有字段就要写一遍

mybatis中可以使用< sql>将重复的代码片段抽出来，然后再使用< include>引入

id：唯一标识

refid：引入

```
<sql id="select*">
    select id, username, password from usee
</sql>
<select id="GetUser" resultType="rog.studymybatis.stydumybatis1.pojo.User">
     <include refid="select*"></include>
     ...
</select>
```

## trim

trim：不会生成where语句需要使用prefix在语句前面添加where

prefix：在语句前面添加指定内容

prefixOverrides：在语句前面去除指定内容

suffix：在语句后面添加指定内容

suffixOverrides：在语句后面删除指定内容

```xml
<select id="getalltwo" resultType="cn.z2z.pojo.Users">
    select *
    from users where emp_id = #{empId};
    <trim prefix="where" suffix="and">
        <if test="name != null">
            name like concat('%',#{name},'%') and
        </if>
        <if test="home != null">
            home = #{home} and
        </if>
    </trim>
</select>
```

## choose when otherwise

when：相当于if .. else if ，最少一个

otherwise：相当于else，对多一个

```xml
<select id="getalltwo" resultType="cn.z2z.pojo.Users">
    select * where emp_id = #{empId};
    <where>
        <choose>
            <when test="name != null">
                name = #{name}
            </when>
            <when test="name2 != null">
                name2 = #{name2}
            </when>
            <otherwise>
                name3 = #{name3}
            </otherwise>
        </choose>
    </where>
</select>
```