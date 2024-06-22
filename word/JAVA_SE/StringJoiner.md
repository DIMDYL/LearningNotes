## 介绍

用于拼接字符串

StringJoiner(",")：间隔符

StringJoiner(",","[","]")：间隔符，开始符合，结尾符号

```java
// 间隔符，开始符合，结尾符号
StringJoiner s = new StringJoiner(",","[","]");
s.add("1");
s.add("1");
s.add("1");
s.add("1");
System.out.println(s); // [1,1,1,1]
```

