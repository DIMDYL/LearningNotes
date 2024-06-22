## 概述

字符串是不会被改变的，字符串的对象在创建后不能更改

以下案例创建了两个字符串变量，等于创建了两个对象，但是在输出的时候是name + name2 这样属于拼接还会创建一个新的对象

所以以下三里创建了三个对象

```java
String name = "邓安然";
String name2 = "邓紫棋";
System.out.println(name + name2);
```

## 创建方式

```java
String name = "邓安然";
String name2 = "邓紫棋";
System.out.println(name + name2);
// new String创建
String s = new String("DIM");
System.out.println(s);
// 通过字符数组创建字符串
char[] arr = {'D','Y','L'};
String s1 = new String(arr);
System.out.println(s1);
// 通过字节数组创建
byte[] arr2 = {97,98,99};
String s2 = new String(arr2);
System.out.println(s2);
```

## 直接赋值的方式底层讲解

java底层内存分为：

1. 栈：方法运行时进栈，运行完毕出栈
2. 堆：new出来的对象都在堆中
3. 方法区：存放字节码文件

还有StringTable是用来存储字符串常量的，JDK7以前在方法区中，JDK8开始在堆中

在使用直接赋值的情况创建字符串的时候会先看StringTable中有没有如果有这个常量直接拿来用，如果没有在常量池中存储

## 字符串比较

因为== 比较的是字符串的地址

equals：比较的是字符串的内容

equalsIgnoreCase：忽略大小写比较内容

```java
String a = "DIM";
String b = new String("DIM");
System.out.println(a == b); // false
System.out.println(a.equals(b)); // true
String a2 = "gem";
String b2 = "GEM";
System.out.println(a2.equalsIgnoreCase(b2)); // true
```

## 分割字符串

使用substring分割字符串，它是左开右闭的。意思就是包含左边的值，不包含右边的值

```
String phone = "18600000000";
String start = phone.substring(0,3);
String end = phone.substring(7,phone.length());
System.out.println(start + "****" + end);
```