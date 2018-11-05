# docker
参考： http://www.runoob.com/docker/docker-tutorial.html
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
#### docker镜像
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
## Volume
提供独立于容器之外的持久化存储
## Registry
镜像仓库
## docker-compose
多容器app
## docker命令
``` shell
service docker start //启动docker daemon
```
## 理解资料
https://segmentfault.com/a/1190000008557309
