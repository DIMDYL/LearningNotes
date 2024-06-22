## 批量添加元素

批量添加元素
public static < T> boolean addAll(Collection< T> c,T...elements)

打乱List集合元素的顺序
public static void shuffle(List<?> list)

排序
public static < T> void sort(List< T> list)

根据指定的规则进行排序
public static < T> void sort(List< T> list,Comparator< T> )

以二分查找算法查找元素
public static < T> int binarySearch(List< T> list,T key)

拷贝集合中的元素
public static < T> void copy(List< T> dest,List< T> src)

使用指定的元素填充集合
public static < T> int fill(List< T> list,T obj)

根据默认的自然排序获取最大/小值
public static < T> void max/min(Collection< T> coll)

交换集合中指定位置的元素
public static < T> void swap(List<?> list, int i,int j)

public static void main(String[] args) {
创建集合对象

ArrayList< String> list = new ArrayList<>();


```java
    批量添加元素
    Collections.addAll(list, "aaa", "bbb", "ccc");
    [aaa, bbb, ccc]
 
    打乱集合中的元素
    Collections.shuffle(list);
    [ccc, aaa, bbb]
 
    排序
    Collections.sort(list);
    [aaa, bbb, ccc]
 
    按照指定规则打乱
    Collections.sort(list, (o1, o2) -> {
        int i = o1.compareTo(o2);
        return Integer.compare(0, i);
    });
    [ccc, bbb, aaa]
 
    以二分查找算法查找元素
    int index = Collections.binarySearch(list, "ccc");
    System.out.println(index);
    0
 
    拷贝集合中的元素
    ArrayList<String> list2 = new ArrayList<>();
    Collections.addAll(list2, "a", "b", "c");
    Collections.copy(list2,list);
    System.out.println(list2);
    [ccc, bbb, aaa]
 
    根据默认的自然排序获取最大/小值
    String max=Collections.max(list);
    System.out.println(max);
    ccc
 
    交换集合中指定位置的元素
    Collections.swap(list,0,1);
    System.out.println(list);
    [bbb, ccc, aaa]
 
    使用指定的元素填充集合
    Collections.fill(list,"sss");
    System.out.println(list);
    [sss, sss, sss]
 
}
```
