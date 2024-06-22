## 项目结构

1. sky-take-out：maven父工程，统一管理依赖版本，聚合其他子模块

2. sky-common：子模块，存放公共类，例如：工具类、常量类、异常类

3. sys-pojo：子模块，存放实体类、VO、DTO、Entity
4. sky-server：子模块，后端服务，存放配置文件，Controller、Service、Mapper等

Entity：实体，通常和数据库中的表对应

DTO：数据传输对象，通常用于程序中各层之间传递数据

VO：视图对象，为前端展示数据提供的对象

POJO：普通Java对象，只有属性和对应的getter和setter