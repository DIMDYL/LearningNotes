## 配置

```xml
<profiles>
    <!-- 生产环境 -->
    <profile>
        <id>pro_env</id>
        <properties>
            <profile.active>pro</profile.active>
        </properties>
    </profile>
    <!-- 开发环境 -->
    <profile>
        <id>dev_env</id>
        <properties>
            <profile.active>dev</profile.active>
        </properties>
        <!-- 开启使用 -->
         <activation>
            <activeByDefault>true</activeByDefault>
        </activation>
    </profile>
    <!-- 测试环境 -->
    <profile>
        <id>test_env</id>
        <properties>
            <profile.active>test</profile.active>
        </properties>
    </profile>
</profiles>
```

## 使用

