## ThreadLocal

一此请求就是一个线程

ThreadLocal并不是一个Thread，而是Thread的局部变量

ThreadLocal为每一个线程提供一份存储空间，具有隔离的效果，只有在线程内才能获取到对应的值，线程外则不能访问

## 使用

在项目中会创建一个类，来使用ThreadLocal，分贝调用threadLocal的，get、set、remove方法

在拦截器中调用setCurrentId设置本次线程的数据

在service中使用的时候只需要BaseContext.getCurrentId()即可

```java
package com.sky.context;

public class BaseContext {

    public static ThreadLocal<Long> threadLocal = new ThreadLocal<>();

    public static void setCurrentId(Long id) {
        threadLocal.set(id);
    }

    public static Long getCurrentId() {
        return threadLocal.get();
    }

    public static void removeCurrentId() {
        threadLocal.remove();
    }

}
```