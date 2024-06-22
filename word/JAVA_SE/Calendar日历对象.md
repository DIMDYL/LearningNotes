```java
// 创建日历对象
Calendar now = Calendar.getInstance();
// 获取当前时间对象
System.out.println(now.getTime());
// 修改指定日历信息
now.set(Calendar.YEAR,1);
System.out.println(now.get(Calendar.YEAR));
// 为某个指定信息增加或者减少
now.add(Calendar.YEAR ,1);
System.out.println(now.get(Calendar.YEAR));
```