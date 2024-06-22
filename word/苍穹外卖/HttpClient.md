## 介绍

HttpClient是用于提供高效的、最新的、功能丰富的支持HTTP协议的客户端编程工具包，并且它支持HTTP协议最新的版本和建议

## 导入依赖

阿里云OSS-SDK底层就是使用的HttpClient

```xml
<dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpclient</artifactId>
    <version>4.5.13</version>
</dependency>
```

## GET请求

```java
// 创建HttpClient对象
CloseableHttpClient httpClient = HttpClients.createDefault();
// 创建请求对象
HttpGet httpGet = new HttpGet("http://127.0.0.1:8080/user/shop/status");
// 发送请求
CloseableHttpResponse execute = httpClient.execute(httpGet);
// 获取服务器返回的状态码
int statusCode = execute.getStatusLine().getStatusCode();
System.out.println(statusCode);
// 获取响应体
HttpEntity entity = execute.getEntity();
// 解析响应体，返回字符串
String string = EntityUtils.toString(entity);
System.out.println(string);
// 关闭资源
httpClient.close();
execute.close();
```

## POST请求参数

```
// 创建HttpClient对象
CloseableHttpClient httpClient = HttpClients.createDefault();
Map<String,String> map = new HashMap<>();
map.put("username", "admin");
map.put("password", "123456");
// 创建请求对象
HttpPost httppost = new HttpPost("http://127.0.0.1:8080/admin/employee/login");
// 将参数转换为json字符串
StringEntity entity = new StringEntity( JSONObject.toJSONString(map));
// 设置编码方式
entity.setContentEncoding("utf-8");
// 设置参数格式
entity.setContentType("application/json");
// 传递参数
httppost.setEntity(entity);
// 发送请求
CloseableHttpResponse execute = httpClient.execute(httppost);
// 获取响应体
HttpEntity entity1 = execute.getEntity();
// 解析响应体转换为字符串
String string = EntityUtils.toString(entity1);
System.out.println(string);
httpClient.close();
execute.close();
```