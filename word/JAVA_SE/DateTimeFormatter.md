## 介绍

在Java中,DateTimeFormatter类用于格式化和解析日期时间对象。

它是日期时间格式化的强大而灵活的工具。

```java
DateTimeFormatter t = DateTimeFormatter.ofPattern("yyyy-MM-dd", Locale.CHINA);
LocalDate l = LocalDate.now();
System.out.println(l.format(t)); // 2023-12-25
```

