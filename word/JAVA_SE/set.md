## 介绍

Set数据不允许重复

最常见的实现类是HashSet和TreeSet

作为接口它抽取了所有实现类的共有方法，所有实现Set接口的实现类均可使用这些方法。例如HashSet和TreeSet均可使用如下共有方法。

HashSet允许null值，并且只允许一个null值存在，它也是非线程安全的，不过它提供构造线程安全的HashSet的方法

## 常用方法

boolean add(E e)	添加元素
boolean remove(Object o)	从集合中移除指定的元素
void clear()	清空集合中的元素
boolean contains(Object o)	判断集合中是否存在指定的元素
boolean isEmpty()	判断集合是否为空
int size()	集合的长度，也就是集合中元素的个数

```java
public static void main(String[] args) {
    // 创建一个数据类型为String的Set对象，并指明其实现类为HashSet
    Set<String> set=new HashSet<>();
    // 添加
    set.add("DIM");
    set.add("DZQ");
    set.add("XZQ");
    // 删除
    set.remove("XZQ");
    // 是否存在某个值
    boolean yorn = set.contains("DZQ");
    System.out.println(set);
    System.out.println(yorn);
}
```

