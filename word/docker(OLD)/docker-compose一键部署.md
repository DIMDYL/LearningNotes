## 基础语法

``` yaml
version: "3.8"
service:
	容器名:
	
        build:  # 指定包含构建上下文的路径, 或作为一个对象，该对象具有 context 和指定的 dockerfile 文件以及 args 参数值
            context: # context: 指定 Dockerfile 文件所在的路径
            dockerfile: # dockerfile: 指定 context 指定的目录下面的 Dockerfile 的名称(默认为 Dockerfile)
		image: # 镜像
		container_name: # 容器启动名称
		prots:  # 端口
			- "xx: xx"
		environment: # 系统环境
			ENV TZ=Asia/Shanghai
            RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
        volumes: # 挂载卷
        	- "./xxx:/xxx/xxx"
        network: # 自定义网络
        	- xxx 
```

## 使用

``` yaml
services:
  mysql:
    image: 3218b38490ce
    container_name: reverent_curran
    ports:
      - "3306:3306"
    environment:
      TZ: Asia/Shanghai
      MYSQL_ROOT_PASSWORD: 123321
    volumes:
      - "./init:/docker-entrypoint-initdb.d/ " # 初始化sql
      - "./conf:/mysql:/ect/mysql/conf.d " # mysql配置
      - "./mysql/data:/var/lib/mysql" 
    networks:
      - hmallnet
  hmall:
    image:  9d2375db0950
    container_name: hmall
    ports:
      - "9090:8080"
    networks:
      - hmallnet
  nginx:
    image: 605c77e624dd
    container_name: nginx
    ports:
      - "18080:18080"
      - "18081:18081"
    volumes:
      - "/www/nginx.conf:/etc/nginx/nginx.conf "
      - "/www/:/usr/share/nginx/html"
    networks:
      - hmallnet
networks:
  hmallnet:
    name: hmallnet
```

