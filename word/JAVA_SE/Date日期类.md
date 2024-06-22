把时间转换成字符串

```java
Date d = new Date();
// EEE表示星期几， a表示上午还是下午
SimpleDateFormat s = new SimpleDateFormat("yyyy.MM.dd HH:mm:ss EEE a"); // 格式化
System.out.println(s.format(d)); // 2023.12.25 16:44:50 星期一 下午
```

把字符串时间转换为时间对象

```java
String sss ="2022.1.1 2:2:1";
SimpleDateFormat ss = new SimpleDateFormat("yyyy.M.d H:m:s");
Date d = ss.parse(sss);
System.out.println(d);
```