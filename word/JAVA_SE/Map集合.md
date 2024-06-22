## 介绍

Map<k,v>  k: 键 v: 值

Map的键是不能重复的，后面重复的值会替换前的值

```java
Map<String, String> map = new HashMap<String,String>();
        //添加元素
        map.put("dim", "001");
        map.put("di2", "002");
        map.put("di3", "001");
        System.out.println(map.toString());
        
        System.out.println("--------");
        
        //根据键删除指定元素
        map.remove("dim");
        System.out.println(map.toString());
        
        System.out.println("--------");
        
        //移除所有元素
        //map.clear();
        //System.out.println(map.toString());

        //查看是否包含键是dim的
        System.out.println(map.containsKey("dim"));
        
        
        //查看值是否有包含002的
        System.out.println(map.containsValue("001"));
        
                
        //判断集合是否为空
        System.out.println(map.isEmpty());
        
        //集合中的个数
        System.out.println(map.size());
```

## 获取功能：

```java
Map<String, String> map = new HashMap<String,String>();    
        map.put("dim", "001");
        map.put("di2", "002");
        map.put("di3", "001");
        
        //获取所有键
        Set<String> d = map.keySet();
        for(String s :d) {
            System.out.println(s + " " + map.get(s));
        }
        
        //获取所有的值
        Collection<String> d2 =  map.values();
        for(
            s :d2) {
            System.out.println(s);
        }
```