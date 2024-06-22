## 介绍

在某些情况下，一个类的对象有且固定限制的，如季节类，它只有春夏秋冬4个对象这种实例有限且固定的类，在 Java 中被称为枚举类；

## 枚举：

枚举类的构造求是私有的，定义的变量也是私有的

```java
public enum demo01 {
    X,Y,Z;
}
```

给枚举添加成员变量和构造函数，枚举很聪明，会直接知道name和(中的内容)绑定

```java
package demo07;
public enum demo01 {
    RED("红色"),
    RED2("红色");
    private String name;

    demo01(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

## 使用

```java
// 获取所有的枚举常量
demo01 arr[] = demo01.values();
// 根据名称获取指定的枚举
demo01 a = demo01.valueOf("RED");
```

更好的限制类型，接受的至就只能是demo01这个枚举对象中定义的才可以

```java
package demo07;

public class main {
    public static void main(String[] args) {
        find(demo01.nv);
    }
    public static void find(demo01 a){
        switch (a){
            // 枚举会自动识别，不需要再使用demo01.nv了
            case nv:
                System.out.println("女");
                break;
            case nan:
                System.out.println("男");
                break;
        }
    }
}
```