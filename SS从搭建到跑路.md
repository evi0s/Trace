# SS从搭建到跑路

## 什么是番羽土啬

众所周知，因为某些历史原因，筑起了长城防火墙，使得我们国内的互联网成为了*LAN*。

所以像某些网站例如
* Geegle
* Facabook
* Twiter

等等都无法打开了~~(卧槽)~~！

然鹅这不是最关键的，关键在于

* D0cker hub巨慢
* GayHub 濒临打不开
* Stankoverflow 日常抽风

~~可能你感觉现在好像用不到~~，但是作为一个程序猿，怎么能不懂番羽土啬呢~~(理直气壮)~~！

行吧，废话不多说了，开始跑路

## 如何番羽土啬

其实番羽土啬有多种**手段**，目前常用的有：

* ~~修改hosts~~
* 挂*V*P*N*
* *S*S/*S*S*R*

其实还有更多，但是基本上原理都是类似的~~(其实是我太菜了想不出来了)~~

有这么多番羽土啬的方法，为啥我要选择**SS**呢？

* hosts目前被和谐的越来越多，使得很不稳定
* VPN也是可以的，但是有时候会有蜜汁问题~~(Windows!说的就是你)~~
* SSR是SS的加强版，但是同样的，对于番羽土啬而言SSR更新的特性很多我们都使用不到，配置错的话还会出现蜜汁问题

所以我们偏向于使用SS来番羽土啬~~(当然如果你有其他更好的办法或者觉得我太菜了就可以无视这篇文章了)~~

## 前期准备

~~(番羽土啬不打4个字了，太累了)~~

**接下来可能会出现很多你陌生的名词，此时，该好好发挥搜索引擎的作用了！**

当然，和学长直接py也是可以的

你需要

* 一台有网络连接的客户端~~(其实就是电脑/手机)~~
* 一定的**Linux**命令行的基础(不懂不会就可以直接问搜索引擎了哇)
* 一台服务器(或VPS)(当然一定是要在墙外面的)

## 开始搭建！

### STEP 1

#### 关于服务器/VPS

服务器和VPS还是有些区别的，服务器只是一个通俗的说法~~(是我太菜了)~~。后面都统称服务器了。

#### 服务器选购

妈耶，一上来就要花钱？

是的，没办法，服务器托管商总不能白送给你吧(其实有免费的，下面会说)。

下面总结一下常见的服务器和其中的坑(这里不会列出国内服务器托管商)

* **AWS** (Amazon Web Services) 目前最好的服务器，没有之一。性能好，带宽大，云服务提供商的老大。同时，如果你有一张国际信用卡(这种东西，想到了啥)，可以去AWS申请一年的试用(没错，免费的就是这个)，但是你要注意：只有10GB的外网(WAN)包括上传和下载的流量；硬盘读写很容易超出免费套餐限制。超出免费套餐限制是需要按照正常计费标准收费的。而AWS的价格就非常的不亲民了。所以，想体验一下可以去某宝搜索***然后激活注册体验一下~~(美滋滋)~~。
* **Azure** (MicroSoft Azure) 全球使用第二多的云服务器，在部署服务的时候很蛋疼，性能不错，带宽个人感觉一般。曾经有免费活动，现在没有了。价格较贵，不适合翻墙使用。
* **Bandwagon** (搬瓦工) 目前价格非常好的服务器。搬瓦工提供的服务器有OpenVZ架构和KVM架构，其中OpenVZ架构的服务器非常便宜，但是除非你想找麻烦，否则还是别去买这种了；KVM架构的服务器其实也不是很好，性能一般，带宽一般，但是你只想搭一个**能用**的SS，而且也不想花太多的钱的话，搬瓦工是你的不二之选。
* **Vultr** Vultr是老牌云服务器商了，也是我推荐的云服务器商。Vultr有很多$2.5/月的服务器可供选择，便宜实惠，性能不错，带宽还行，流量也比较多。个人推荐$5/月的服务器，~~你可以在上面玩更多的骚操作~~。近期Vultr也有活动，新用户充值$5送$25，能用一年，也就意味着最便宜的方案可以$5用一年，推荐的方案可以用半年，非常划算。
* **DigitalOcean** DigitalOcean也是老牌云服务器商了，最低价格$5/月，用的时间有点久了，记得性能还算不错，其他的应该也和现在有些不同了。
* **Linode** 同上，Linode属于高富帅型的云服务器商，对服务器可以有很多高级的配置，但是用户界面非常拙鸡。性能不错，带宽还行。但是最重要的是，我忘了交费竟然追着我要了半年？？？~~(好吧并不重要，雾)~~

好吧，常见的就这些了，如果有看到不错的，也可以去体验一下(比如Google的云服务)

### STEP 2

#### SSH

好不容易把服务器给买好了，但是怎么去操作服务器？

这时候我们就需要SSH工具了

SSH是什么？

你可以简单的理解为，SSH是一个远程的终端，连接到服务器，并可以在服务器上执行命令。

一般情况下，Linux服务器都会自动安装好了SSH服务器端，在服务器提供商的管理平台可以看到你的Linux服务器的root用户的密码和服务器的IP地址。此时，我们只需要使用客户端的SSH链接到服务器就可以了。

*root用户即根用户或超级用户，拥有对系统的最高权限，因此在root用户下操作务必小心*

SSH有哪些客户端？
* **XShell** Windows客户端，有免费版。
* **putty** Windows客户端，轻量且免费
* **juiceSSH** Android客户端，非常好用
* **WebSSH** iOS客户端，免费但是广告巨多，操作起来有些蛋疼，总体还算不错
* **Termius** macOS客户端，界面清爽，非常好用
* **ssh** 所有的UNIX/Linux发行版和macOS都自带的一个命令行工具，原汁原味，非常好用

安装好了SSH客户端，你就可以去链接你的服务器了

在客户端内填入服务器的IP地址，用户名和密码，接受并保存密钥，你就可以看到~~熟悉~~的Linux命令行界面了。

如果你成功连接上了你的服务器，你就可以继续往下看了；如果你遇到了任何问题，可以去寻求搜索引擎的帮助；如果实在搜不到，就可以直接找学长交流~~(py)~~。

##### 一些问题
* 我们为何要去使用Linux服务器？在服务器上很少使用Windows Server，Linux可以精简的非常轻量，对配置要求低，性能优秀。~~最重要的是~~，一个程序猿能不懂Linux？~~(瞎扯，Windows开发者就行)~~
* 为啥是命令行界面，我想要可视化操作啊。确实，命令行对初学者很不友好，但是当你使用多了以后，你会发现命令行操作的效率会比可视化操作效率高得多得多。更重要的是，很多Linux的软件根本没有可视化界面。。。
* 系统这么多，我用什么比较好？常见的有Ubuntu、Debian、CentOS、Arch Linux等等，使用哪一种系统都没有太大的本质上的区别，根据个人使用喜好而定。个人推荐：CentOS或Ubuntu

#### 环境部署

根据服务器商提供的系统镜像不同，Linux系统自带的软件也就不同。避免在安装时出现各种蜜汁错误，我们需要对包管理器进行初始化和部分常用软件安装。

对于UNIX系系统如Debian和Ubuntu，使用了apt作为包管理器：
```bash
apt-get update
apt-get install wget curl net-tools git vim screen iptables python
# wget、curl为下载器
# net-tools为网络工具的小集合包
# git为git管理工具
# vim就是最好用的编辑器(删掉删掉)
# screen是一个窗口管理工具，可以避免SSH的一些蜜汁问题
# iptables是防火墙，可以不装，有的系统自带了，有时候iptables会出现一些蜜汁问题，可选安装
# python不用说了，虽然自带但是安装一下让它更新到最新版本
```

对于Linux系系统如CentOS和RHEL，使用了yum作为包管理器：
```bash
yum update
yum install wget curl net-tools git vim screen iptables python
```

### STEP 3

#### 什么是SS

SS，全称ShadowSocks，是一种Socks5代理工具，开源，具有轻量，安全，跨平台等优秀的特性。

SS有许多不同的版本，如python版，libev版等，一般情况下，我们使用python版来做简单的搭建，当然libev版也因轻量快捷而被广泛使用。

python版SS搭建可以让你自己动手，多多了解命令行。但是如果你觉得麻烦，也可以直接跳转至一键脚本安装。

#### python版SS搭建

*Python版本为2.6或2.7*

##### 首先安装python-setuptools和pip包管理器

对于UNIX系系统如Debian和Ubuntu

```bash
apt-get install python-gevent python-pip
```

对于Linux系系统如CentOS和RHEL

```bash
yum install python-setuptools
easy_install pip
# 按 y 回车以确认
```

##### 通过pip安装shadowsocks-python版

对于UNIX系系统如Debian和Ubuntu

```bash
pip install shadowsocks
apt-get install python-m2crypto # 加密模块
```

对于Linux系系统如CentOS和RHEL

```bash
pip install shadowsocks
```

到此为止，python版的shadowsocks已经安装完毕

是的没错，如果没有任何错误的话，就已经安装完毕了，但是我们还没有对其进行配置

##### 配置shadowsocks

在这里，无论什么系统，配置都是相同的

* 创建配置目录

```bash
mkdir /etc/shadowsocks # 创建 /etc/shadowsocks/ 目录
touch /etc/shadowsocks/config.json # 创建 /etc/shadowsocks/config.json 文件
```

* 编辑配置文件

```bash
vim /etc/shadowsocks/config.json
```

此时，就进入到了vim的编辑器界面，这里有些指令不理解，可以去搜索引擎查找相应的教程

* 按 i 键进入编辑模式(insert)
* 粘贴以下文本

```json
{
    "server":"0.0.0.0",
    "server_port":8989,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"YOURPASSWORD",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open":false,
    "workers": 1
}
```

* server_port为你想要开启的SS服务的端口号
* password为你想要设置的密码
* method为你的加密方式，请将你设置的记下，后面在客户端连接时需要

* 按esc键(escape)退出编辑模式
* 按**半角**冒号键(:)
* 输入wq保存并退出(w: write; q: quit)

至此，shadowsocks配置完成。

##### 启动！

shadowsocks启动直接可以使用ssserver命令

```bash
ssserver -c /etc/shadowsocks/config.json -d start
```

此时没有错误的话，即是启动成功了，查看一下端口是否已经打开

```bash
netstat -tunlp | grep python
```

检查有没有你设置的端口

##### 关闭

同启动一样，关闭还是使用ssserver命令

```bash
ssserver -c /etc/shadowsocks/config.json -d stop
```

没有错误的话，即是关闭成功了，同样去查一下端口情况

```bash
netstat -tunlp
```

检查你设置的端口是否已经关闭

##### 后续

为了方便开启和关闭shadowsocks服务，一下子输这么长的命令肯定会令人不悦的。这里我们可以写一个非常简单的脚本来执行这个操作

* 在/bin下创建ssstart文件和ssstop文件

在ssstart中写入下列内容

```shell
#!/bin/bash
ssserver -c /etc/shadowsocks/config.json -d start
```

在ssstop中写入下列内容

```shell
#!/bin/bash
ssserver -c /etc/shadowsocks/config.json -d stop
```

* 给这两个脚本赋可执行权限

```bash
chmod +x /bin/sss*
```

至此，开启和关闭shadowsocks服务可以这样

```bash
ssstart # 开启ss服务
ssstop # 关闭ss服务
```

是不是简单多了

至此，如果你在上述步骤中没有发生任何错误，此时就可以跳转至客户端安装去测试shadowsocks是否工作正常了

如果你遇到了一些错误，可以将错误的提示在搜索引擎上查找，或者更简单的，直接找学长~~py~~啊

#### 一键脚本安装 shadowsocks-libev

其实，在搜索引擎上搜索一下，你会发现有许多的SS搭建一键脚本。不要随便使用这些！因为未知的脚本可能会携带挂马软件或~~挖矿~~。

这里我们推荐一个网站

[秋水逸冰](https://teddysun.com)

目前该网站可能已经遭封杀，在你的shadowsocks搭建完毕以后可以去看一看，该网站有非常多的优质一键脚本，并且开源。

这里直接给出安装的步骤

##### 新建窗口

*此步骤非必须*

由于网络的不稳定性，SSH可能会断线(没错)。而短线之后，在SSH一个session中正在运行的程序都会被kill掉(强行停止)。

为了保证脚本正常运行结束，这里我们使用screen打开一个窗口，来维护脚本运行。

如果SSH非正常断开~~(或自己手贱点错了)~~，就可以使用打开的screen来继续之前的进度。

```bash
screen -S ss # 新建一个窗口，名字叫ss
```

此时你应该进入了新的界面，这就是一个窗口，我们可以继续下面的步骤了

##### 一键安装

对于Linux系系统如CentOS和RHEL

*原地址[CentOS下shadowsocks-libev一键安装脚本--秋水逸冰](https://teddysun.com/357.html)*

执行

```bash
wget --no-check-certificate -O shadowsocks-libev.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev.sh
chmod +x shadowsocks-libev.sh
./shadowsocks-libev.sh 2>&1 | tee shadowsocks-libev.log
```

脚本会提示输入端口，密码和加密方式

端口，密码可以自定义，加密方式建议使用默认值

相关管理命令：

```bash
/etc/init.d/shadowsocks start # 启动
/etc/init.d/shadowsocks stop # 停止
/etc/init.d/shadowsocks restart # 重启
/etc/init.d/shadowsocks status # 查看状态
```

对于UNIX系系统如Debian和Ubuntu

*原地址[Debian下shadowsocks-libev一键安装脚本--秋水逸冰](https://teddysun.com/358.html)*

执行

```bash
wget --no-check-certificate -O shadowsocks-libev-debian.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev-debian.sh
chmod +x shadowsocks-libev-debian.sh
./shadowsocks-libev-debian.sh 2>&1 | tee shadowsocks-libev-debian.log
```

执行过程中要求和管理命令同CentOS相同

##### 退出窗口

在窗口中执行完后，可以直接输入

```bash
exit
```

退出窗口

当然，如果你还想继续使用这个窗口但不想终止，你可以按

```
ctrl + A + D # Windows键盘
control + A + D # macOS键盘
```

当挂起了以后想再进入窗口，可以执行

```bash
screen -r ss # 恢复窗口
```

在窗口中按

```
ctrl + A + K # Windows键盘
control + A + K # macOS键盘
```

可以直接结束窗口，效果类似于执行exit

#### 进阶-容器化SS服务

容器是什么？首先，要来介绍一款非常棒的虚拟化软件

**Docker**

如同他的名字一样，Docker虚拟化和码头一样，由一个个集装箱堆叠而成

在这里，不再赘述Docker的安装和使用，想要深入学习的可以咨询搜索引擎，只想了解并使用的可以去参考这篇文档~~(觉得有帮助能不能求给个star嘤嘤嘤)~~

[Docker初步](https://github.com/evi0s/Trace/blob/master/Docker.md)

看完，你应该对Docker有了一个初步的认识，并初步会使用Docker了

##### 从官方repo的镜像构建

官方shadowsocks提供了libev版本的镜像，源地址[shadowsocks-Servers](https://shadowsocks.org/en/download/servers.html)

执行

```bash
docker pull shadowsocks/shadowsocks-libev
docker run -e PASSWORD=<password> -p<server-port>:8388 -p<server-port>:8388/udp -d shadowsocks/shadowsocks-libev
```

密码和端口在命令的环境变量设置中指定，可以自定义，默认的加密方式为aes-256-cfb

*官方的镜像其实我还没有测试，如果出问题可以参考下面的另一个镜像*

##### 第三方镜像--秋水逸冰

没错，又是他(太巨了)，源地址[介绍几款 Docker 镜像](https://teddysun.com/536.html)

* 创建config文件

参考python版，文件路径 /etc/shadowsocks-libev/config.json 

内容有所区别

```json
{
    "server":"0.0.0.0",
    "server_port":8989,
    "password":"password0",
    "timeout":300,
    "method":"aes-256-gcm",
    "fast_open":true,
    "nameserver":"8.8.8.8",
    "mode":"tcp_and_udp"
}
```

* 启动容器

执行

```bash
docker run -d -p 8989:8989 -p 8989:8989/udp --name ss-libev -v /etc/shadowsocks-libev:/etc/shadowsocks-libev teddysun/shadowsocks-libev:alpine
```

至此，常见的SS搭建方法就结束了，如果在搭建中有任何问题，请不要吝啬你的提问。当然如果发现我写的有错误，也请及时告~~(批)~~诉~~(评)~~我

### STEP 4

我SS搭好了，但是怎么用哇

这里即需要客户端去连接了

官方有一份客户端大全[shadowsocks-clients](https://shadowsocks.org/en/download/clients.html)

#### Windows

**shadowsocks-win** 

Windows客户端，由于手头没有Windows，我还不知道具体长啥样(接受批评)

但是你可以去询问搜索引擎，大体的步骤应该是添加服务器-开启代理，代理可以全局可以PAC，服务器只要照着安装的时候的配置填就可以了。

下载链接：

* [官方GitHub](https://github.com/shadowsocks/shadowsocks-windows/releases)

#### macOS

**ShadowsocksX-NG** 

macOS客户端，启动后在菜单栏右有个小飞机图标，点开以后有一个服务器，点击服务器设置，在左边框下点击'+'号，添加服务器配置，添加完成后关闭，点开小飞机，选择PAC自动模式或者全局模式，然后即可打开shadowsocks。

下载链接：

* [官方GitHub](https://github.com/shadowsocks/ShadowsocksX-NG/releases)

#### iOS

**ShadowRocket**

iOS客户端，国区已经凉了，可用第三方助手下载老版本安装，使用上没有任何问题~~(经常闪退)~~

#### Android

**shadowsocks-android**

play商店上有beta版，网上各种版本也流传甚广，**应该**是都能使用的~~(可以py一下apk安装包)~~。

很长时间没有用安卓了所以配置大致也忘了~~(懒得写了)~~，总体而言都是差不多的，奇奇怪怪的选项留空留默认绝对(一般)不会出问题。

### STEP 5

问题集锦

#### 连接上了，没有网？

首先检查配置有没有问题，加密方式填错了没有，ip地址填错了没，密码填错了没。。。。

如果确认没问题，查看一下网络是否通畅：

用本地机ping一下服务器ip，Windows和macOS和Linux都可以，命令相同

```bash
ping <ip>
```

如果通畅，下一步检查服务器防火墙问题

安装了iptables之后(CentOS 7请检查firewalld状态)，可能会自启动iptables服务，这时没有规则端口会被防火墙ban掉

*firewalld请自行搜索，可用systemctl stop firewalld.service命令直接关闭*

此时你可以添加规则/关闭防火墙

```bash
systemctl stop iptables.service # 关闭防火墙
```

```bash
echo "-A INPUT -m state --state NEW -m tcp -p tcp --dport 8989 -j ACCEPT" >> /etc/sysconfig/iptables # --dport为ss服务端口，可以改成自己的

systemctl restart iptables.service # 重启防火墙
```

如果还是有问题，请检查搭建步骤，或者换个方法搭建，或者找学长py寻求解决方法

#### 网速太慢？

网速慢几乎不可避免，但是我们有各种方法优化网络速度，降低延迟等

##### BBR

BBR算法是谷歌开发的一种TCP BBR 拥塞控制算法，实装后效果非常明显，甚至能提高几个数量级

在此不再赘述安装方法，一键脚本，走起！

没错还是他，[一键安装最新内核并开启 BBR 脚本](https://teddysun.com/489.html)

*这里提醒OpenVZ架构的服务器就可以不用尝试了*

执行

```bash
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh
```

重启之后，可以参照源网页确认BBR已经开启。

##### 锐速

老款加速工具，现在已经使用的很少，可以去寻求搜索引擎寻求相关内容，此处不再赘述

*同样的OpenVZ可以直接跳过了*

##### fast_open

在配置shadowsocks时，有个选项就是fast_open，默认我们填写的是false

如果服务器内核在3.7+，可以开启fast_open降低延迟

执行

```bash
echo 3 > /proc/sys/net/ipv4/tcp_fastopen
```

开启后，将fast_open的配置设置为true即可。

## 参考资料

* [秋水逸冰](https://teddysun.com)
* [shadowsocks](https://shadowsocks.org)
