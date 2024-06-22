方法一：使用字符串格式化实现四舍五入(支持float和double类型)

```java
double data = 3.02;
//利用字符串格式化的方式实现四舍五入,保留1位小数
String result = String.format("%.1f",data);
//1代表小数点后面的位数, 不足补0。f代表数据是浮点类型。保留2位小数就是“%.2f”，依此累推。
System.out.println(result);//输出3.0
```

方法二：使用BigDecimal实现四舍五入(支持float和double类型)

```java
double data = 3.02;
//利用BigDecimal来实现四舍五入.保留一位小数
double result = new BigDecimal(data).setScale(1, BigDecimal.ROUND_HALF_UP).doubleValue();
//1代表保留1位小数,保留两位小数就是2,依此累推
//BigDecimal.ROUND_HALF_UP 代表使用四舍五入的方式
System.out.println(result);//输出3.0
```

方法三：使用DecimalFormat实现四舍五入(仅支持float类型)

```java
DecimalFormat decimalFormat=new DecimalFormat("#.##");
//保留2位小数，.后面的#代表小数点后面的位数,保留3位小数就是#.###
System.out.println(decimalFormat.format(3.065f));//输出3.07
System.out.println(decimalFormat.format(3.065));//double类型，输出3.06
```