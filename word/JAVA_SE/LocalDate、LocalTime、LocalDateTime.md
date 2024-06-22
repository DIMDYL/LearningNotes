## 三者的不同点是:

LocalDate只能使用年月日；

LocalTime只能使用时分秒；

LocalDateTime可以使用年月日时分秒。

我们在使用的时候可以根据自己的需求进行选择。

LocalDate：

修改时间后会返回一个新的时间LocalDate对象

```java
LocalDate l = LocalDate.now**()**;

System.out.println**(**l.getYear**())**; // 获取年份

System.out.println**(**l.getMonthValue**())**; // 获取月份

System.out.println**(**l.getDayOfMonth**())**; // 获取几号

// 修改时间

LocalDate l2 = l.withYear**(**2099**)**;

System.out.println**(**l2.getYear**())**; // 2099
```

![img](https://d.z2z.cn/wp-content/uploads/2023/12/QQ%E6%88%AA%E5%9B%BE20231225185353.png)