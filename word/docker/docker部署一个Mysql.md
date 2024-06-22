## 获取镜像

``` shell
docker pull mysql:8.0
```

## 启动容器

在 mysql/init 的sql都会被执行

``` shell
 docker run -d  
 -v /mysql/init:/docker-entrypoint-initdb.d/ -- 初始化脚本
 -v /mysql/conf:/ect/mysql/conf.d -- 配置
 -v /mysql/data:/var/lib/mysql
 -p 3307:3306  -e MYSQL_ROOT_PASSWORD=123321 镜像id
```
