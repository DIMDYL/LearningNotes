## 学习日记
<img src="./img/005I4VvOly1hhwpya1w4ej30sg0sf14m.jpg" alt="Alt" style="zoom:50%;" />

## 2024年5月22日

今天学习了DockerCompose 来部署多个镜像一次，通过yaml的格式来书写docker参数，多个镜像可以根据配置文件来快速部署

还学习了微服务的相关知识

例如：

什么是微服务：微服务就是将一个庞大复杂的单体项目拆分为多个小型单体项目

为什么要使用微服务：微服务更好维护，单个模块出问题直接修改单个模块不会影响整体项目

什么时候使用微服务：项目复杂、用户量庞大

拆分微服务要求：高内聚、低耦合，在拆分微服务的时候要做到模块功能完整，尽量减少对其他模块的引用

如何拆分：根据业务模块拆分、根据公共字模块拆分

## 2024年5月20日至2024年5月21日

学习了Docker的基础使用以及Docker制作镜像，如何通过DockerFile来打包镜像

#### DockerFile：

可以通过dockerfile来指定基础的镜像，然后制作自己想要的镜像

在执行 docker build -t 镜像名称  **.** ：只要加了最后的面这个 . 就会自动去在当前目录寻找   dockerfile这个文件来执行

例如：

打包java项目镜像，通过一个拥有jdk11环境的centos镜像来将自己的项目拷贝到镜像的根目录中执行java -jar xx.jar的命令

这样就可以实现封装一个项目的镜像，在其他服务器中可以快速的部署，都不要配置java环境了

## docker网络

在docker启动的容器是默认分配了一个网段的ip，但是在项目重启的时候可以会出现ip变化的情况

为了避免这一现象可以使用 docker network  create xxx 来创建一个网络

在镜像运行的的时候使用 --network 网络名 来加入该网络或者 使用 docker network connect 网络名称 容器命来加入

加入自定义网络的容器可以直接使用容器名称来充当容器的ip使用，这样就避免了ip变化的情况

## 2024年5月16至2024年5月19日

#### Iservice接口

MybatisPlus的Iservice接口，Iservice接口提供了大量单表操作函数，在需要使用service接口中继承Iservice接口在使用的service实现类中要继承ServiceImpl<Mapper接口， 实体类>

Iservice接口用于快速书写简单语句，可以不需要去Mapper中写sql或者是生成的sql语句执行了

例如：需要查询一个id为1的数据只需要在需要操作的service实现类上使用getById(1)就可以实现、

#### 静态SQL

Db静态SQL方法用于处理循环注入的问题

Db方法可以使用Iservice中的操作mapper的方法，只不过需要传入对应的实体类的字节码文件才能使用

#### 枚举处理器

默认处理器为：Jackson

在开发中在操作用户状态的时候，一般是使用数字来操作，有时候可能会不记得或者传错的情况

这时MyBatisPlus提供了枚举类型，可以将数据库和实体类的用户状态字段进行自动转换，值需要添加注解即可

也可以将枚举类型转换为前端json数据，也是使用一个注解即可十分的简单

这样就可以优化代码的可读性也可以明确的标注用户状态了

## 2024年5月15日

今天学习了：

1. MyBatis-Plus的条件构造器：
   通过条件构造器可以快速的生成复杂的SQL语句
   条件构造器分为，Query的和Update构造器用于实现查询和修改数据
   以及LambdaQuery和LambdaUpdate通过Lambda表达式的写法使用（推荐使用Lambda的写法）

2. 使用BaseMapper来自定义sql：

   自定义Mapper方法，在方法中传入生成的SQL语句，在xml进行sql语句拼接即可
   这样就可以在Mapper来操作数据了，而不是在Service中操作

3. Iservice接口：
   Iservice接口是MyBatis-Plus提供的CRUD接口
   提供了大量的CRUD操作
   只需要在需要操作的Service接口中继承IService接口
   并且在service层的实现类中继承ServiceImpl<需要操作的Mapper, 操作的表实体>即可

4. 批量操作：
   使用Mysql自带的属性

   ``` yml
   jdbc:mysql://127.0.0.1:3306/mybatisplus?rewriteBatchedStatements=true
   ```

   结合IService的批量添加可以实现几秒添加10万条数据

## 2024年5月14日

今天完成了，MyToDoList项目的登录、注册组件的开发、以及MyToDoList的后端的项目初始化

#### 新学了MyBatis-Plus

MyBatis-Plus是MyBatis的增强版，对单表操作及其简单

使用只需要在需要的Mapper类中继承BaseMapper<实体类>

#### 原理

MyBatis-Plus通过反射来获取实体类中的内容转换为字段的内容

#### @TableName("xxx")

如果实体类和数据库的表明不一致可以在实体类上添加@TableName("xxx")来实现映射

#### @TableId("xx", type=xxx)

来映射字段名和实体类中主键名称不同的情况

#### @TableField(value = "name", exist = false)：

来映射普通字段字段和属性名不同的情况

也可以用于设置表中没有的字段但是实体类中存在的字段过滤

#### 特殊情况

例如：属性为is开头并且为Boolean类型，必须使用@TableField()来指定才能使用（MyBatis-Plus在通过反射的时候会去除is）

例如：字段名为数据库关键词，也需要使用@TableField( \` xxx` )来转义后指定才能使用，不然会报错，因为在sql中不能出现关键词

#### 配置

MaBatis-Plus继承了Myabtis的配置，在yml项目配置中基本是一致的

局部配置的是高于全局配置

例如：

在全局配置的: id-type: auto # id为自增

但是在某个实体类中配置的是@TableId(type = IdType.ASSIGN_ID)

那么通过该实体类的sql的ID会是ASSIGN_ID（雪花算法生成）

## 2024年2月1日至2024年2月10日

复习了多线程与反射、动态代理，完成了苍穹外卖的开发，学习了SpringCache的使用，SpringCache支持多种的缓存中间件，只需要引入如redis的依赖即可，无需配置SpringCache，在使用的位置使用注解就可以完成缓存和清除缓存以及将方法返回值存入缓存中等等，其他的操作基本就是增删改查，准备SSM复习完做项目，然后再复习一下开始微服务

使用AOP的功能去处理代码中的重复度高的代码，使用自定义注解切入点，处理代码中的createtinme等重复高的操作

## 2024年1月30日

今天学习了Spring的AOP，AOP是用于将重复代码抽出来降低代码耦合以及冗余的，通过AOP的切入点来控制哪个包下的方法或接口会执行切面方法，通过AOP的连接点可以获取到执行的目标方法全类名以及方法名和返回参数等。

使用场景：日志处理、计算接口运行时常等

## 2024年1月29日

今天跟着视频开发了苍穹外卖的添加员工、删除员工、修改员工、禁用与启用员工，并根据文档开发了分类的分页接口、添加分类、修改分类、启用于禁用分类接口，分页使用的是pagehelper

## 2024年1月25日

今天学习了Spring的bean读取配置文件、第三方bean、使用配置文件替换掉xml配置、使用注解定义bean

读取配置文件：在配置类中读取配置文件（@PropertySource("classpath:dim.properties")）在需要注入的地方使用@Value("${xxx.xxx}")来指定数据

第三方bean：第三方bean一般在配置文件中使用@Import(xxxx.class)来引入bean

使用配置文件替换掉xml配置：使用@Configuration注解表示当前是一个配置类，@ComponentScan("xxx.xxx")来扫描指定包的bean，在创建容器的时候需要使用AnnotationConfigApplicationContext(配置文件.class)来创建容器

注解定义bean：使用Component或Component的衍生注解来定义bean，在需要注入引用类型的地方使用@Autowired表示此处需要注入，如果有多个实现类可以使用@Qualifier("xxx")来指定具体需要注入的bean

## 2024年1月24日

今天学习了Spring的IOC于DI，以及bean的生命周期

IOC：控制器取代传统的new来创建对象，而是使用将对象交给IOC容器来管理，IOC通过注入的方式来创建对象（bean），从而实现解耦

DI：管理bean于bean之间的关系，可以注入引用类型，于普通类型，普通类型使用value的形式来注入，一级数组、map等都能注入

## 2024年1月21日

今天学习了拦截器和spring中的事务和异常处理

拦截器：拦截器拦截进入spring的处理，拦截器可以指定排除那个路径不进行拦截，如果拦截器和过滤器一起使用，请求会先进入过滤器进行过滤，然后进入拦截器处理，最后进入过滤器过滤放行后的操作

事务：通过注解自动开启事务和回滚提交，当一个事务调用另外一个事务的时候会牵扯到事务传播，事务传播就是调用的事务究竟是和本事务一起混滚提交还是不参与本事务的提交，并且事务默认是捕获运行时异常，需要使用rollbackFor设置捕获那些异常

异常处理：定义一个异常类（RestControllerAdvice：全局异常类），指定捕捉的异常（ExceptionHandler(xxxx)指定捕捉的异常），定义了异常捕捉就不用一个一个类的自己添加了，并且在出错的时候会有返回错误数据，而不是报服务器异常错误

## 2024年1月18日

今天学习了Cookie和Session和JWT，以及Spring的过滤器

Cookie：在服务端设置数据客户端会自动存储，缺点是客户端可以直接挂不必Cookie，数据存储在客户端数据不安全，不能在移动端APP存储

Session：存储在服务端数据，第一次链接服务端会与之创建Session对象，每次通过SessionID寻找这个唯一的对象，直到有一方关闭才会断开连接，Session底层也是通过Cookie实现的，如果Cookie关闭了会通过URL的形式实现，缺点是数据存储在服务端会占据大量服务器资源

JWT：是一串Base64字符串，数据通过加密，存储在客户端，每次请求客户端将JWT写入请求头返回给服务器解析接口，可以在移动端APP使用

过滤器（Filter）：

在请求前进行拦截做出对请求做出处理，例如验证用户是否登录

Filter在使用的时候需要在启动类加上@ServletComponentScan注解因为Fileter是Javaweb的三大类不是SpringBoot的

## 2024年1月17日

今天做了SpringBoot的增删改查案例，以及文件上传，还有分页查询，分页查询先是我自己用select * from xxx limit xx offset xx 写了个接口，然后又学习了个PageHelper分页插件，这个插件也太好用了吧，只需要几行就实现了Service层的操作，只需要把获取第几页，和一页显示多少条给他，然后再给他一个获取的全部数据抓换为Page<java映射类名> 给他就能获取到查询页的数据和数据总和

还学习了文件上传的本地上传，本地上传需要用MultipartFile来做为接收参数名，还学习了UUID唯一标识的生成UUID.randomUUID()

好好学习，天天向上！

## 2024年1月15日

今天学习了XML映射sql，通过xml书写sql语句，Mybatis中提供了< where>、< if>、< set>、< foeach>方法来更好的控制修改删除添加以及< sql>语句片段以及< inclide>引入等操作

< where>：动态条件，如果条件都不满足where都不出创建，而且会自动处理and和or（如果第一条没有执行成功会把当前的and或者or删除）

< if>：if中有一个 test = "xx != null" 这种写法可以控制预编译sql是否拼接此条件的语句

< set>：在修改的时候使用，set可以去除语句的后面的 ,  如果当前是第一条语句但是后面的都不满足条件，那么当前的语句后面的 ， 就会被删除

< foreach>：用于删除，可以遍历集合，拼接成（x,x,x,x,）的形式

< sql>：用于将重复代码抽取写入

< include>：将重复代码片段引入

## 2024年1月14日

今天学习了mysql的事务、索引、和mybatis入门

事务：要么都执行成功才能成 功要就不成功，失败可以回滚确保了数据的准确性

索引：索引是对一个字段创建索引，底层原理是树结构，索引对查询优化快，是因为提前跑了一边存储起来，会占据硬盘空间，索引查询快 ，写入和修改慢

mybatis：持久性框架，用于简化JDBC的操作，简单的做了一个删除功能还学习了Lombok，用于简化Geter、Serter等操作，只需要添加注解就能实现

mybatis在创建的时候使用mapper来代替dao层，通过@Mapper可以自动实现接口，并将实现类放入IOC中

## 2024年1月13日

今天学习了数据库设计：一对一、一对多、多对多，内连查询外连查询以及子查询

数据库设计：

1. 一对一使用外键进行连接但是这个外键需要添加一个唯一约束
2. 一对多使用外键进行连接
3. 多对多使用第三张表来存储另外两张表的外键

多表查询：

1. 内连查询：在查询时会输出两张表的全部组合情况所以需要添加查询条件，筛选外键与另外一张表的主键
2. 外连查询：分为左和右外连，一般使用左外连，外连接查询指的是第一张表的全部属于和第二张表交际的数据，注意外连也需要处理集合全部组合问题
3. 子查询：子查询就是将一个查询语句的返回值作为查询条件的参数，在进行子查询的时候需要考虑都涉及到那几张表，处理完表之间的问题了（全部组合问题）再写查询逻辑



## 2024年1月12日

今天学习了mysql的DML（数据的增加删除修改），以及学习了查询语句（DQL），聚合函数和分组查询、排序查询、分页查询以及流程控制语句

if(a = 1, "1","2") 如果a=1那么显示1。如果不是显示2

分组查询之后还需要进行条件筛选需要使用having，having跟着条件，一般having后面跟的都是聚合函数

## 2024年1月11日

今天学习了springboot的日期请求参数和路径请求参数已经json请求参数，以及封装一个固定响应包，以及学习了什么分层解耦，还有复习mysql基础知识

路径请求参数：/user/{name} get(@PathVariable String name)，需要依靠注解绑定参数，并路径后的名称要和形参参数名一致

json参数：需要创建于前端传递的json对应的对象，使用@RequestBody绑定参数 get(@RequestBody Data data)

日期参数：前端需要于指定格式匹配才能请求成功 get( @DateTimeFormat( pattern="yyyy-MM-dd")  LocalDate time)

#### 分层：

在控制器中请求和响应的属于controller

处理逻辑的属于service

访问数据的属于Dao

对于对应代码创建对应包模块化开发

#### 解耦

在service中需要Dao的数据，就需要对Dao的接口实现方法进行创建对象，如果更改实现方法的逻辑那么代码Service也需要修改，增加耦合性

使用LOC&DI解决此方法，将service和Dao的实现类使用@Component 注解放入容器中，在使用了@Autowired 注解会在容器中寻找对应对象

## 2024年1月9日

今天学习了Springboot，Springboot是用于创建Spring项目的框架，SpringBoot内置集成了Tomcat，tomcat是无法识别普通类的，但是tomcat设计中包含了javaEE规范的servlet，在Springboot中客户端发送请求会经过Dispatcherservlet，Dispatcherservlet间接继承与servlet所以是可以在Springboot中是可以被识别到的，Dispatcherservlet将请求内容分发给处理方法，处理方法处理完成会返回给Dispatcherservlet响应给客户端

DispatcherServlet 是一个典型的 Servlet。它继承自 HttpServlet，而 HttpServlet 则实现了 Servlet 接口。因此，DispatcherServlet 间接地继承了 Servlet 接口

请求参数 get(String a, String b)，在前端发送请求的时候需要保持与后端形参名一致，如果想要不一致可以使用@RequestParam 注解@RequestParam(name = "a",required = false) ，required为是否为必填项，默认使用了该注解就为true

还有数据请求，学习了使用GET、POST请求，封装复杂请求类，复杂请求参数就是请求参数过于多，可以定义一个方法私有参数，实现geter、seter，还有接收数组参数，需要前端在请求时，参数名保持一致例如：?dim=1&dim=2后端接收到[1, 2]，也可以使@RequestParam注解参数绑定接收一个List集合

## 2024年1月8日
今天学习了Maven的安装已经Maven项目的创建，以及Maven的生命周期，了解到Maven的生命周期都是有Maven的插件来完成

每一个生命周期的阶段是需要依赖前面的阶段

<br>
<a href="https://beian.miit.gov.cn/">鄂ICP备2021011541号-7</a>