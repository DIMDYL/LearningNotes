## 介绍

List接口是一个有序、可重复的集合，继承Collection接口，并添加了一些针对有序列表的操作。它允许元素的重复，并提供了根据索引访问、添加、删除和替换元素的方法。在Java中，List接口有几个常见的实现类，每个实现类都具有不同的性能和用途。

## ArrayList

ArrayList是List接口的一个常见实现类，它基于动态数组实现，可以根据需要自动扩展和收缩数组的大小。以下是一些常用的ArrayList方法：

add(E element): 在列表的末尾添加元素。
get(int index): 获取指定索引位置的元素。
set(int index, E element): 替换指定索引位置的元素。
remove(int index): 移除指定索引位置的元素。
size(): 返回列表的大小。

```java
import java.util.ArrayList;
import java.util.List;

public class LIST {
    public static void main(String[] args) {
        List<String> fruits = new ArrayList<>();
        fruits.add("A");
        fruits.add("B");
        fruits.add("C");

        System.out.println("Fruits: " + fruits);

        fruits.remove(1);
        System.out.println(fruits);

        String fruit = fruits.get(0);
        System.out.println(ruit);
    }
}
```

## LinkedList

LinkedList是List接口的另一个实现类，它基于双向链表实现。与ArrayList相比，LinkedList对于频繁的插入和删除操作更高效。以下是一些常用的LinkedList方法：

add(E element): 在列表的末尾添加元素。
get(int index): 获取指定索引位置的元素。
set(int index, E element): 替换指定索引位置的元素。
remove(int index): 移除指定索引位置的元素。
size(): 返回列表的大小。

```java
import java.util.LinkedList;
import java.util.List;

public class LIST {
    public static void main(String[] args) {
        List<String> names = new LinkedList<>();
        names.add("A");
        names.add("B");
        names.add("C");
        names.remove(1);
        String name = names.get(0);
    }
}

```

