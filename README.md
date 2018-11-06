# docker
参考： http://www.runoob.com/docker/docker-tutorial.html
## docker命令
``` shell
service docker start  //启动docker daemon
docker pull[OPTIONS] NAME[:TAG] //拉取镜像,:TAG(默认 :Latest)
docker images[OPTIONS][REPOSITORY[:TAG]] //查看本地镜像
docker image ls   //查看本地所有镜像
docker images node[REPOSITORY]  //查看指定image

docker run [OPTIONS]IMAGE[:TAG][COMMAND][ARG……] //启动镜像
docker run -d -P training/webapp python app.py  //启动容器,-d运行这个容器在后台
docker run -d -P --name [$NAMES] training/webapp python app.py //自定义名称的启动容器
docker run ubuntu:15.10 /bin/echo "Hello world" //启动容器

docker exec [OPTIONS] CONTANIER COMMAND [ARG……] //进入容器
docker exec -it f4 bash
exit //退出容器

docker ps   //查找正在运行的容器
docker port bf08b7f2cd89[CONTAINER ID]  //查看容器映射端口号
docker port zealous_agnesi[NAMES]  //查看容器映射端口号  0.0.0.0:32771->5000/tcp
docker stop $NAMES   //停止指定容器
docker stop $CONTAINER_ID   //停止指定容器
docker start $NAMES //启动指定容器
docker start $CONTAINER_ID   //启动指定容器

netstat -na|grep 8080 //查看8080端口占用情况
```
## 简介
`docker`：2013年横空出现。  
以Docker为代表的内核容器技术不是新技术，而是将已有技术（LXC,cgroups,Union FS）进行了更好的包装和整合，并形成了一种标准镜像格式。   
开源项目，它可以将任何应用以轻量级的形式打包、发布、运行  
可以粗糙的理解为轻量级的虚拟机。开挂的chroot。 
Docker与传统虚拟化方式不同在于，只在操作系统层实现虚拟化，只虚拟操作系统而不虚拟内核。  
Docker是什么呢，白话点说，就是一个Container的管理工具。  
计算机基本单元由虚拟机变为了容器，越来越多应用的构建、部署与运行选择在容器中进行。

|特性|容器|虚拟机|
|---|---|---|
|启动|秒级|分钟级|
|硬盘使用|MB-GB|GB|
|性能|接近原生|小于原生|
|系统支持量|单机支持上千个容器|一般几十个|  
## 思想
* 集装箱
* 标准化（1.运输方式  2.存储方式  3.api接口）
* 隔离（LXC思想）
#### docker思想解决的问题
* 本地运行没问题，测试环境或者生产环境有问题。docker的集装箱思想解决了运行环境不一致的问题。
* 系统卡，磁盘占满。linux系统本身就是多租户的。docker的隔离思想可以解决该问题，保证自己的app不被其他应用影响。
* 服务器撑不住。扩容可以解决这种问题。
## 术语
|en|中文|作用|
|---|---|---|
|host|宿主机|正在使用的电脑|
|image|镜像|本地建的或者远端拉去的重复使用的软件打包|
|container|容器|镜像运行实际|
|registry|仓库|存储很多镜像的仓库|
|daemoon|守护程序|用来接收用户命令，和registry共享|
|client|客户端|给daemon输送命令|
## docker命令
|命令|用途|
|---|---|
|docker pull|获取image|
|docker build|创建image|
|docker images|列出image|
|docker run|运行container|
|docker ps|列出container|
|docker rm|删除container|
|docker rmi|删除image|
|docker cp|在host和container之间拷贝文件|
|docker commit|保存改动为新的image|
## dockerfile
类似配置文件，通过dockerfile可以构建一个image
#### dockerfile语法
|命令|用途|
|---|---|
|FROM|base image|
|RUN|执行命令|
|ADD|添加文件|
|COPY|拷贝文件|
|CMD|执行命令|
|EXPOSE|暴露端口|
|WORKDIR|指定路径|
|MAINTAINER|维护者|
|ENV|设定环境变量|
|ENTRYPOINT|容器入口|
|USER|指定用户|
|VOLUME|mount point|
# 镜像
镜像的本质就是文件  
通过docker images指令来查看本地有哪些镜像  
* 镜像ID： 每个镜像有一个唯一的ID；长度为64个字符。通常只使用前12个字符
* 镜像Tag：每个镜像上可以打上一个或多个TAG
* 镜像Repository:每个镜像存储在一个仓库中  
* Respository:TAG 唯一标识了一个镜像
#### 镜像分层
Dockerfile中每一行都产生一个新层。
``` javascript
FROM alpine:latest  4e38e38c8ce0
MAINTAINER xbf  fb1aabf4427b
CMD echo 'hello docker' 3df065bgdff6
```
镜像分层的好处是当多个dockerfile中有5个镜像分层相同时变可以减少压力
# 容器
容器的本质是进程
# 仓库
如何把本地镜像传输到目的地，这时候就需要docker仓库。  
步骤一：本地----->docker仓库。  
步骤二：docker仓库---->拉取到目的地  
docker仓库：
* hub.docker.com
* c.163.com  
docker支持自己在内网内建立一个私有仓库
# docker网络
#### 网络类型
* Bridge：独立的ip 端口和namespace
* Host 与主机共用，不会独立分配。启用该模式该容器不会拥有独立的networknamespace，而是和主机使用一个，容器将不会再虚拟出自己的网卡，配置自己的ip和端口
* None
#### 端口映射
容器内的端口要在主机内访问到

``` shell
docker run -d -p 8080:80 nginx //启动nginx 分配8080端口号
docker run -d -P nginx   //启动nginx 随意分配一个端口号
```
## Volume
提供独立于容器之外的持久化存储
## Registry
镜像仓库
## docker-compose
多容器app
## 理解资料
https://segmentfault.com/a/1190000008557309
