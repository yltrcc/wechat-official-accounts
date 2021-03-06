# 每日一句
No victory comes without a price.
凡是成功就要付出代价。

# 概述

这个快速开始手册是帮忙您快速在您的电脑上，下载、安装并使用 nacos。

# 版本选择

您可以在Nacos的[release notes](https://github.com/alibaba/nacos/releases)及[博客](https://nacos.io/zh-cn/blog/index.html)中找到每个版本支持的功能的介绍，当前推荐的稳定版本为1.4.1。

# 预备环境准备

Nacos 依赖 Java 环境来运行。如果您是从代码开始构建并运行Nacos，还需要为此配置 Maven环境，请确保是在以下版本环境中安装使用:
1. 64 bit OS，支持 Linux/Unix/Mac/Windows，推荐选用 Linux/Unix/Mac。
2. 64 bit JDK 1.8+；[下载](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) & [配置](https://docs.oracle.com/cd/E19182-01/820-7851/inst_cli_jdk_javahome_t/)。
3. Maven 3.2.x+；[下载](https://maven.apache.org/download.cgi) & [配置](https://maven.apache.org/settings.html)。

# 下载源码或者安装包

你可以通过源码和发行包两种方式来获取 Nacos。

**从 Github 上下载源码方式**

```Bash
git clone https://github.com/alibaba/nacos.git 
cd nacos/ 
mvn -Prelease-nacos -Dmaven.test.skip=true clean install -U ls -al distribution/target/ 

// change the $version to your actual path 
cd distribution/target/nacos-server-$version/nacos/bin
```


**下载编译后压缩包方式**

您可以从 [最新稳定版本](https://github.com/alibaba/nacos/releases) 下载 nacos-server-$version.zip 包。

`unzip nacos-server-$version.zip 或者 tar -xvf nacos-server-$version.tar.gz cd nacos/bin`

# 启动服务器

**Linux/Unix/Mac**

```Bash
启动命令(standalone代表着单机模式运行，非集群模式):
sh startup.sh -m standalone
如果您使用的是ubuntu系统，或者运行脚本报错提示[[符号找不到，可尝试如下运行：
bash startup.sh -m standalone
```


**Windows**

```Bash
启动命令(standalone代表着单机模式运行，非集群模式):
cmd startup.cmd -m standalone
```

# 服务注册&发现和配置管理

**服务注册**
`curl -X POST 'http://127.0.0.1:8848/nacos/v1/ns/instance?serviceName=nacos.naming.serviceName&ip=20.18.7.10&port=8080`
**服务发现**
`curl -X GET 'http://127.0.0.1:8848/nacos/v1/ns/instance/list?serviceName=nacos.naming.serviceName`
**发布配置**
`curl -X POST "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test&content=HelloWorld`
**获取配置**
`curl -X GET "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test`

# 关闭服务器

**Linux/Unix/Mac**

`sh shutdown.sh`

**Windows**

`cmd shutdown.cmd`
或者双击shutdown.cmd运行文件。


# 美文佳句

一生匆匆来去，没有什么是看不开，过不去的。

没有人规定人人都必须长成玫瑰才算成功，只要你喜欢，你可以长成郁金香、雏菊、茉莉，甚至是路边迎风绽放的小花朵。

想挣钱，就努力工作；累了倦了，就停下来休息；想追逐远方，就去旅行；想充实自己，就看书学习技能。

孤独，会让人在无人打扰的时分，给自己的精神世界创造完美的留白；孤独，也可酿成岁月的香醇。

虽然生活有时会有危机，但有时也可以变得温存和美好。只要一路向前，总会赶得上日出和日落。

这世界盛大灿烂，只要自己开心快乐，我们可以尝试不同的生活方式。