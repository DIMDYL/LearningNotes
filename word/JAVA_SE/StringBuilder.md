## 为什么要学StringBuilder

在字符串拼接中，大量拼接String会很慢，而StringBuilder执行很快

## 为什么StringBuilder快

因为StringBuilder内容是可以变的，而String的内容是不可变的好比如说

String a = "DYl";

String b = "GEM";

在合并a和b的时候又会创建一个对象，如果再次合并还会创建一个对象

而StringBuilder是将内容放入容器中，全程只会产生一个StringBuilder对象

## 介绍

StringBuilder可以看作为一个容器，创建后里面的内容是可以发生改变的

#### 作用：

提高字符串的效率

## 常用方法

append：追加值在末尾

reverse：反转

replace：替换值

indexOf：是否包含某个字符串并返回第一次出现位置

```
StringBuilder S1 = new StringBuilder("DIM");
S1.append("DIM"); // 追加值
System.out.println(S1);
System.out.println(S1.reverse()); // 反转
System.out.println(S1.replace(0,3,"GEM")); // 替换
System.out.println(S1.toString()); // 转换为String
```