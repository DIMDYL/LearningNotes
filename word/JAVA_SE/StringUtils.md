## 介绍

StringUtils 是 Apache Commons Lang 库中的一个类，是线程安全的，用于提供字符串操作的各种实用方法。

StringUtils.isEmpty()：此方法检查给定的字符串是否为 null 或空字符串。

```java
boolean isEmpty = StringUtils.isEmpty(str);
```

stringUtils.isNotEmpty()：此方法检查给定的字符串是否不为 null 且不为空字符串。

```java
boolean isNotEmpty = StringUtils.isNotEmpty(str);
```

StringUtils.capitalize()：此方法将字符串的第一个字符转换为大写。

```java
String capitalized = StringUtils.capitalize(str);
```

1. **StringUtils.uncapitalize()**：此方法将字符串的第一个字符转换为小写。

```java
String uncapitalized = StringUtils.uncapitalize(str);
```

StringUtils.substring()：此方法用于获取字符串的子字符串。

```java
String substring = StringUtils.substring(str, start, end);
```

StringUtils.replace()：此方法用于替换字符串中的所有指定子字符串。

```java
String replaced = StringUtils.replace(str, "old", "new");
```

StringUtils.join()：此方法用于将一个数组或集合的元素连接成一个字符串。

```java
String joined = StringUtils.join(array, delimiter);
```

StringUtils.contains()：此方法检查给定的字符串是否包含指定的子字符串。

```java
boolean contains = StringUtils.contains(str, substring);
```

StringUtils.indexOf()：此方法返回子字符串在字符串中首次出现的索引，如果未找到则返回 -1。

```java
int index = StringUtils.indexOf(str, substring);
```

StringUtils.lastIndexOf()：此方法返回子字符串在字符串中最后一次出现的索引，如果未找到则返回 -1。

```java
int lastIndex = StringUtils.lastIndexOf(str, substring);
```