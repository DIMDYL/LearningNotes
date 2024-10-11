## 介绍

stream流在jdk8以后新增的，可以用于操作集合或者数组的数据

优势：stream大量的结合lambda的语法风格来编程，提供了一种更加强大，更加简单的操作数组和集合

## 获取集合中的指定元素

collect：收集

Collectors.toSet()：Set集合中

.map：中间操作，对数据做处理，产生的流，不会返回数据，只有通过收集器才能收集到数据

.map一般用于提取数据

```java
Set<Long> itemIds = vos.stream().map(CartVO::getItemId).collect(Collectors.toSet());
```

## Map获取stream流

方式1：

map想要获取stream流需要获取所有的key，然后再进行stream的操作

```java
Map<String,Integer> map = new HashMap<>();
map.put("dim",20);
map.put("dzq", 10);
map.put("zdf", 18);
Set<String> keys = map.keySet();
System.out.println(map.get("dim"));
List<String> l1 = keys.stream().filter(s->s.startsWith("d")).filter(s->map.get(s)>10).collect(Collectors.toList());
System.out.println(l1);
```

方式2：

map.entrySet()：获取map的所有数据

将map数据转换为set结构，使用set获取stream流进行操作

```java
Map<String,Integer> map = new HashMap<>();
map.put("dim",20);
map.put("dzq", 10);
map.put("tsy", 18);
Set<Map.Entry<String,Integer>> set = map.entrySet();
Set<Map.Entry<String,Integer>> set2 =  set.stream().filter(s->s.getKey().contains("d")).collect(Collectors.toSet());
System.out.println(set2);
```

## 遍历

```java
List<String> list = new ArrayList<>();
list.add("dim");
list.add("dyl");
list.add("zdf");
list.stream().forEach((string -> System.out.println(string)));
```

## 过滤

.collect(Collectors.toList())：将结果封装为集合返回

```java
List<String> list = new ArrayList<>();
list.add("dim");
list.add("dyl");
list.add("zdf");
List<String> l2 =  list.stream().filter(s->s.startsWith("d")).collect(Collectors.toList());
System.out.println(l2);
```

## 常用的中间方法

1、filter：过滤

2、limit：获取前几个元素

``` java
import java.util.ArrayList;
import java.util.Collections;
 
public class Stream01 {
    public static void main(String[] args) {
 
        ArrayList<String> list = new ArrayList<>();
        Collections.addAll(list,"张三","李四","王五","张六六");
        list.stream()
                .filter(s -> s.startsWith("张"))
                .filter(s->s.length()==3)
                .forEach(s->System.out.println(s));
    }
}
```

3、skip：跳过前几个元素

``` java
import java.util.ArrayList;
import java.util.Collections;
 
public class Stream01 {
    public static void main(String[] args) {
 
        ArrayList<String> list = new ArrayList<>();
        Collections.addAll(list,"张三","李四","王五","张六六");
//        思路1
            list.stream().skip(1).limit(2).forEach(s->System.out.println(s));
//        思路2
            list.stream().limit(3).skip(1).forEach(s->System.out.println(s));
    }
}
```

4、distinct：元素去重

``` java
import java.util.ArrayList;
import java.util.Collections;
 
public class Stream01 {
    public static void main(String[] args) {
 
        ArrayList<String> list = new ArrayList<>();
        Collections.addAll(list,"张三","李四","王五","张六六","李四");
        list.stream().distinct().forEach(s->System.out.println(s));
    }
}
```



5、concat：合并a和b两个流为一个大流

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.stream.Stream;
 
public class Stream01 {
    public static void main(String[] args) {
 
        ArrayList<String> list1 = new ArrayList<>();
        Collections.addAll(list1,"张三","李四","王五","张六六","李四");
        ArrayList<String> list2 = new ArrayList<>();
        Collections.addAll(list2,"张三三","李四四","王五五");
        Stream.concat(list1.stream(),list2.stream()).forEach(s->System.out.println(s));
    }
}
```

6、map转换流]中的数据类型

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.function.Function;
import java.util.stream.Stream;
 
public class Stream01 {
    public static void main(String[] args) {
 
        ArrayList<String> list1 = new ArrayList<>();
        Collections.addAll(list1,"张三-18","李四-19","王五-20","张六六-30","李四-40");
        //方法1
        list1.stream().map(new Function<String, Integer>() {
            @Override
            public Integer apply(String s){
                String[] arr=s.split("-");
                String ageString = arr[1];
                int age = Integer.parseInt(ageString);
                return age;
            }
        }).forEach(s->System.out.println(s));
        //方法2
        System.out.println("-----------------------------");
        list1.stream()
                .map(s -> Integer.parseInt(s.split("-")[1]))
                .forEach(s-> System.out.println(s));
    }
}
```
