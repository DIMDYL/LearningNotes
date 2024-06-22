## 集合进阶：

Collection：单列 >list 可重复 set 不可重复

map：双列

## **Collection集合常用方法：**

boolean  add(E e)：添加元素

boolean remove(Object o)：从集合中删除指定元素

void clear()：清空集合所有元素

boolean contains(Object o)：判断指定元素是否存在

boolean isEmpty()：判断集合是否为空

int size()：集合长度

## Collection集合遍历：

iterator：迭代器，集合的专用遍历方式

iterator中常用的方法

E next()：返回迭代中下一个元素

boolean hasNext()：如果迭代具有更多元素，则返回true

代码实现：

```java
Iterator<String> iterator = list.iterator();

while (iterator.hasNext()){

System.out.println(iterator.next());

}
```

List集合的特有方法：
List特有的方法，Collection是没有的，但是List的儿子ArrayList有

```java
void add(int index,E element)：在集合的指定位置添加指定元素

E remove(int index)：删除指定索引的指定元素

E set(int index,E element)：修改指定索引，返回被修改的元素

E get(int index)：返回指定索引的元素
```

