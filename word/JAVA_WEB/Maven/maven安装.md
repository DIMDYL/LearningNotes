# 安装
1.下载：

apache-maven-X.X.X-bin.zip

访问官方网站：https://maven.apache.org/download.cgi

2.配置本地仓库：

在/conf/settings.xml中添加本地仓库

```xml
  <localRepository>D:\DIM_Maven</localRepository>
```

3.配置阿里云私服

在/conf/settings.xml的mirrors中添加一下代码

```xml
  <mirror>
    <id>alimaven</id>
    <mirrorOf>central</mirrorOf>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
  </mirror>
```

4.配置环境变量

添加Maven_home为maven的解压目录，并将bin目录添加到path环境中

5.测试是否配置成功

打开cmd输入

```cmd
nvm -v
```

如果输出的是版本号那么恭喜你配置成功了！



