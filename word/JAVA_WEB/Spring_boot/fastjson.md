## 引入依赖

```java
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
</dependency>
```

## 将对象转换为JSON

``` java
String error = JSONObject.toJSONString(Reponse.success("tokenError"));
```

## 将json转换为对象

```java
String josn = HttpClientUtil.doGet("https://api.weixin.qq.com/sns/jscode2session", map);
// 解析json
JSONObject jsonObject = JSON.parseObject(josn);
// 获取指定属性值
String openid = jsonObject.getString("openid");
```