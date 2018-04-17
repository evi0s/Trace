#Docker 初步
##Docker简介
Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的Linux或Windows机器上，从而实现虚拟化。

---
###Docker的组成
* Docker Client客户端
* Docker Daemon守护进程
* Docker Image镜像
* Docker Container容器

###Docker相对于一般的虚拟机的优点
* 节省硬盘空间 
* 部署 / 启动速度快
* 节省内存
* 分布式部署服务

简而言之，拿node.js举例，一行命令，只需5秒，即可部署一个完整的node.js服务容器

###Docker的安装
---
####Windows系统
请先确认Windows版本已为最新且为企业版或专业版
安装程序请移步[Docker For Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows)
具体安装步骤不再赘述

####macOS系统
安装程序请移步[Docker For macOS](https://store.docker.com/editions/community/docker-ce-desktop-mac)
具体的安装步骤也不再赘述

####CentOS及RHEL
*以下安装操作均在root用户下执行*

要求：
* CentOS 7 (64-bit)
* CentOS 6.5 (64-bit) 或更高的版本
* 内核版本 3.10+

使用yum包管理器安装
```
yum -y install docker
```
启动Docker容器服务
```
#CentOS 7
systemctl start docker.service
#CentOS 6.5
service docker start
```
####Ubuntu及Debian
*以下安装操作均在root用户下执行*

要求：
* Ubuntu 12.04 或更高的版本
* Debian 7.7 或更高的版本
* 内核版本 3.10+

在此使用官方安装脚本安装
```
wget -qO- https://get.docker.com/ | sh
```
启动Docker容器服务
```
service docker start
```

###Docker的配置
---
####配置镜像加速
一般而言，Docker无需配置，但是鉴于国内网络问题，后续拉取 Docker 镜像将会十分缓慢，我们可以配置加速器来解决，在此使用的是网易的镜像地址：
```
http://hub-mirror.c.163.com
```
新版的 Docker 使用 /etc/docker/daemon.json（Linux） 或者 %programdata%\docker\config\daemon.json（Windows） 来配置 Daemon。
请在该配置文件中加入（没有该文件的话，请先建一个）：

```
{
  "registry-mirrors": ["http://hub-mirror.c.163.com"]
}
```
然后重新启动Docker Daemon
```
#CentOS 7
systemctl restart docker.service
#CentOS 6.5+ & Ubuntu & Debian
service docker restart
```

###Docker两个名词解释
---
* 镜像：简单用面向对象来解释的话，相当于类
* 容器：可以理解为虚拟机，简单用面向对象来解释的话，相当于对象


###Docker命令
---
####docker run
---
#####启动一个容器
常用参数
* -i 以交互模式运行容器，通常与 -t 同时使用
* -t 为容器重新分配一个伪输入终端，通常与 -i 同时使用
* -d 后台运行容器，并返回容器ID
* --name 指定容器名称
* -P 暴露容器内已指定的端口并将其映射到宿主机的随机端口
* -p 指定容器内的端口并将其映射到宿主机的指定端口
* --link 链接到其他容器
* -e 设置环境变量
* -v 指定容器内的文件夹并将其映射到宿主机的指定文件夹

以启动一个node.js容器为例
```
docker run -it -d \
           -p 8080:80 \
           -v /data:/usr/local/data \
           --name=node-test \
           node
#最后一行的node为镜像名
#此命令将创建一个node.js容器，node.js镜像版本默认为最新版
#容器内的80端口被映射到宿主机的8080端口，容器内的/usr/local/data文件夹被映射到宿主机的/data文件夹
#容器名称为node-test，执行的命令默认为node
#容器将后台运行
```
执行docker run的时候，如果没有下载相应的镜像，则会自动下载
注意：
容器运行后将不能更改其启动参数
也就意味着，容器运行后不能动态更改映射的文件夹或端口
####docker pull
---
#####下载镜像

从hub上下载镜像
```
docker pull node
#下载node.js的官方镜像
docker pull node:9.9.0
#下载node.js的官方镜像，版本为9.9.0
docker pull mritd/shadowsocks
#下载mritd用户的公开的shadowsocks镜像
```

####docker push
---
#####上传镜像

需要登录docker账户，并在本地commit并tag镜像
具体操作在此不再赘述

####docker ps
---
#####查看当前容器

常用参数
* -a 查看所有容器

```
docker ps
#查看当前正在运行的容器
docker ps -a
#查看所有容器
```

####docker images
---
#####查看本地镜像

```
docker images
#查看本地所有镜像（包括自己保存的镜像）
```

####docker {start|restart|stop}
---
#####启动 / 重新启动 / 停止 一个容器

```
docker start node-test
#启动node-test容器
docker restart node-test
#重启node-test容器
docker stop node-test
#停止node-test容器
```

####docker log
---
#####查看容器日志

```
docker logs node-test
#显示node-test的运行日志（如果有的话）
```

####docker attach
---
#####进入容器

```
docker attach node-test
#进入node-test容器内，并提供命令行界面
```
注意
进入容器内并进行命令行操作有两种常用方法：
* docker attach
* docker exec -it {container name} /bin/bash

区别在于：
* docker attach 更像是console，当退出容器时，将不会停止正在运行的进程
* docker exec -it {container name} /bin/bash 更像是terminal，当退出时，将会kill掉正在运行的进程（参考ssh断开连接）

个人建议使用后者

####docker exec
---
#####在容器中执行命令
常用参数
* -i 以交互模式运行容器，通常与 -t 同时使用
* -t 为容器重新分配一个伪输入终端，通常与 -i 同时使用
* -d 分离模式: 在后台运行

```
docker exec -it node-test node /root/test.js
#在node-test容器中执行node /root/test.js
docker exec -it node-test /bin/bash
#在容器node-test中开启一个交互模式的终端
```

####docker cp
---
#####宿主机与容器之间互相拷贝文件

```
docker cp /data node-test:/usr/local/data
#将宿主机的/data文件夹拷贝到node-test容器的/usr/local/data文件夹
docker cp node-test:/usr/local/data
#将node-test容器的/usr/local/data文件夹拷贝到宿主机的/data文件夹
docker cp /data/test.js node-test:/usr/local/data
#将宿主机的/data/test.js文件拷贝到node-test容器的/usr/local/data文件夹内
```

####docker rm
---
#####删除容器
常用参数
* -f 强制删除，不管容器是否是运行状态

```
docker rm node-test
#删除容器，如果node-test容器为运行状态，将不会删除
docker rm -f node-test
#强制删除node-test容器，不管容器是否是运行状态
```

####docker build
---
#####构建镜像

从本地的Dockerfile构建镜像
具体操作在此不再赘述

####docker commit
---
#####保存容器为镜像

将容器保存为镜像
具体操作在此不再赘述

####docker tag
---
#####给镜像加上标签

标记本地镜像，将其归入某一仓库。
具体操作在此不再赘述

###Docker应用的小demo
---
####启动一个Linux虚拟机
---
```
docker run -it -d --name centos centos /bin/bash
docker exec -it centos /bin/bash
#启动一个CentOS容器，打开一个终端
docker run -it -d --name debian debian /bin/bash
docker exec -it debian /bin/bash
#启动一个Debian容器，打开一个终端
docker run -it -d --name ubuntu ubuntu /bin/bash
docker exec -it ubuntu /bin/bash
#启动一个Ubuntu容器，打开一个终端
```

####分布式部署一个ownCloud私有云服务
---
1.新建数据目录
```
sudo mkdir /var/data
sudo mkdir /var/data/mysql
sudo mkdir /var/data/mysql/owncloud
sudo mkdir /var/data/owncloud 
```
2.拉取镜像
```
docker pull owncloud
docker pull mysql
```
3.配置并启动 MySQL 容器
```
docker run --name mysql-owncloud \
-v /var/data/mysql/owncloud:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=YOUR_MYSQL_ROOT_PASSWORD \
-e MYSQL_DATABASE=owncloud \
-d mysql
```
4.配置并启动 ownCloud 容器
```
docker run --name=owncloud \
--link=mysql-owncloud:mysql-owncloud \
-v /var/data/owncloud:/var/www/html/data \
-p 8080:80 \
-d owncloud
```
5.完成部署
打开http://ip:8080 即可看到owncloud的初次配置界面，在填写数据库地址时，填写MySQL容器的名称即可
这里放出一个演示地址，搭建使用的就是docker技术
[ownCloud demo](https://pan.qrs0301.xin)

###Docker相关教程参考链接
[菜鸟教程](http://www.runoob.com/docker/docker-tutorial.html)
[WikiPedia](https://en.wikipedia.org/wiki/Docker_(software))