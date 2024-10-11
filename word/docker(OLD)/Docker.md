## 在线安装docker
1、官网安装参考手册：
https://docs.docker.com/engine/install/centos/
2、卸载系统中安装的旧版本

``` shell
 yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

3、安装软件包（提供实用程序）并设置存储库

``` shell
yum install -y yum-utils
```

4、设置docker镜像源

``` shell
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

5、更新yum软件包索引

``` shell
yum makecache fast
```

6、安装docker

``` shell
yum install docker-ce docker-ce-cli containerd.io -y
```

## 阿里云镜像加速       
​        介绍： https://www.aliyun.com/product/acr
​        注册一个属于自己的阿里云账户 ( 可复用淘宝账号 )
​        进入管理控制台设置密码，开通
​        查看镜像加速器自己的

配置镜像加速器

``` shell
mkdir -p /etc/docker
cat > /etc/docker/daemon.json <<'EOF'
{
    "exec-opts": ["native.cgroupdriver=systemd"],
    "log-driver": "json-file",
    "log-opts": {
      "max-size": "100m"
    },
    "storage-driver": "overlay2"
}
EOF
 systemctl restart docker
```

## dockerfile

dockerFile是用于构建Docker镜像的

Docker镜像是分层的

## 基于dockerFile构建java项目镜像

#### 安装基础环境

openjdk:11.0-jre-buster：已经包含了JDK11的Cenntos环境

``` shell
docker pull  openjdk:11.0-jre-buster
```

当前目录需要和jar包在同一个文件夹中

``` text
# 基础镜像
FROM openjdk:11.0-jre-buster
# 环境变量
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# 拷贝docker-demo.jar包到镜像中重命名并移动到根目录
COPY docker-demo.jar /app.jar
# 入口 执行java项目
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

#### 打包镜像

在打包Docker镜像时，`docker build` 命令默认会查找当前目录下的 `Dockerfile` 文件（注意文件名是区分大小写的）。

你不需要在命令中指定 `Dockerfile` 的文件名，除非它的名称不是默认的 `Dockerfile`。

-t就是镜像的名称和版本，默认是最新版

``` shell
docker build -t docker-demo .
```

## 网络

#### dockers network 命令

create：创建新的 Docker 网络。
rm：删除 Docker 网络。
inspect：检查 Docker 网络的详细信息。
list：列出所有 Docker 网络。
prune：删除未使用的 Docker 网络。
connect：将容器连接到网络。
disconnect：将容器与网络断开连接。

#### 选型：

-d, --driver：指定网络驱动程序。
-o, --opt：设置网络驱动程序的选项。
–attachable：指定网络是否可附加。
–internal：指定网络是否为内部网络。
–gateway：指定网络的网关地址。
–subnet：指定网络的子网地址。
–ip-range：指定网络的 IP 地址范围。
–aux-address：指定网络的辅助地址。
–help：显示帮助信息。

#### 使用

创建网络

``` shell
docker network create 网络名
```

将容器加入网络

``` shell
docker network connect 网络名 容器名
```

查看容器详细信息

``` shell
docker inspect 容器名
```

#### 启动容器时加入网络

``` shell
docker run -d   -p 3307:3306 --network 网络名   -e MYSQL_ROOT_PASSWORD=123321 镜像名
```
