## 读取单一数据

#### yml

```yml
dyl:
  name: DIMDZQ
  year: # 数组数据
    - 1
    - 2
    - 3
```

#### 读取二级属性数据

```java
@Value("${dyl.name")
String name;
```

#### 读取数组数据

根据坐标获取数，在yml中一定要使用 - xx 来定义数据

```java
@Value("${dyl.year[0]}")
String name;
```

## 变量引用

通过${xx.xx}来一层一层获取数据进行引用

```
dyl:
  path: /dzq
  year:
    - ${dyl.path}1
    - ${dyl.path}2
    - ${dyl.path}3
```

#### 转义字符的使用

如果想要使用转义字符可以加上双引号即可，\t等转义字符就不会被作为普通字符串了

```yml
dyl:
  name: DIMDZQ
  path: /dzq
  year:
    - "${dyl.path} \t1"
    - ${dyl.path}/t2
    - ${dyl.path}/t3
```

## 读取所有属性

Spring提供了一个Environment用于获取所有配置信息

通过getProperty("xx.xx")来获取对应的数值

```java
// 注入Environment
@Autowired
private Environment env;
@GetMapping("/get1")
public String api1(){
    return env.getProperty("dyl.name");
}
```