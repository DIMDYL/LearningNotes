## resultMap

使用resultMap进行映射数据库字段于java实体字段不同的情况

```xml
<resultMap id="collectiond" type="cn.z2z.pojo.Entiy">
    <association property="DIMDIM" javaType="emp">
        <result column="dim_id" property="dimId"></result>
    </association>
</resultMap>
<resultMap id="empResultMap" type="cn.z2z.pojo.Entiy">
    <result column="create_time" property="DIMDIM"></result>
</resultMap>
<select id="getall" resultType="cn.z2z.pojo.Entiy" resultMap="empResultMap">
    select * from user;
</select>
```

1. **id**: 这是 `resultMap` 的唯一标识符，用于在其他地方引用这个映射。
2. **type**: 指定映射的 Java 类型。
3. **extends**: 如果这个 `resultMap` 与另一个 `resultMap` 有很多相似之处，你可以使用 `extends` 属性来继承另一个 `resultMap` 的配置，然后只定义差异部分。
4. **autoMapping**: 如果设置为 `true`，MyBatis 会自动映射所有列到 JavaBean 的属性。默认值为 `false`。
5. **result**: 用于定义单个列到 JavaBean 属性的映射。
   - **column**: 数据库结果集中的列名。
   - **property**: JavaBean 的属性名。
   - **javaType**: Java 属性的类型，当 MyBatis 不能自动推断属性类型时使用。
   - **jdbcType**: JDBC 类型，用于指定列的类型，如 `VARCHAR`、`INTEGER` 等。
   - **nested**: 如果设置为 `true`，则此属性是另一个 `resultMap` 的引用，该 `resultMap` 将被用于映射该列的值。
6. **association**: 用于一对一 (1:N) 的关联映射。
   - **property**: JavaBean 的属性名。
   - **javaType**: Java 属性的类型。
   - **column**: 数据库中的外键列名。
   - **select**: 指定一个已映射的 `select` 语句的 ID，用于加载关联数据。
   - **resultMap**: 指定一个已定义的 `resultMap` 的 ID，用于加载关联数据。
7. **collection**: 用于一对多 (1:n) 的关联映射。
   - **property**: JavaBean 的属性名。
   - **ofType**: 集合中对象的类型。
   - **column**: 数据库中的外键列名。
   - **select**: 指定一个已映射的 `select` 语句的 ID，用于加载关联数据。
   - **resultMap**: 指定一个已定义的 `resultMap` 的 ID，用于加载关联数据。
8. **discriminator**: 鉴别器，用于基于某个列的值来决定使用哪个 `resultMap`。
   - **column**: 用于确定使用哪个 `case` 的列。
   - **javaType**: 列的 Java 类型。
   - **typeHandler**: 用于处理列值的类型处理器。
   - **cases**: 包含一个或多个 `case` 元素，每个 `case` 元素都包含一个 `resultMap` 引用。