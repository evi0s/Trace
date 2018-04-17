# Ngrok内网穿透

## Ngrok是什么？

Ngrok是一个反向代理工具，通过在公共的端点和本地运行的 Web 服务器之间建立一个安全的通道。
也就是说，Ngrok需要一个有公网IP的服务器端和一个提供服务的客户端

## 为什么要使用Ngrok？

作为一个Web开发者，我们有时候会需要临时地将一个本地的Web网站部署到外网，以供他人体验评价或协助调试等等，通常我们会这么做：

* 找到一台运行于外网的Web服务器
* 服务器上有网站所需要的环境，否则自行搭建
* 将网站部署到服务器上
* 调试结束后，再将网站从服务器上删除

而使用Ngrok我们只需一行命令即可将内网的服务映射到外网
*工作室自建Ngrok服务器已使用了可信任机构签发的https证书，各浏览器可正常打开*

## 有DDNS为什么还选择Ngrok？

很多时候，DDNS并不能解决内网穿透的问题。DDNS名为动态域名解析，其本质即动态将域名解析到当前IP地址。但在很多场景，如校园，都使用NAT，DDNS就不能实现内网穿透了

## Ngrok的使用

### HTTP服务和HTTPS服务内网映射

自行下载对应系统的Ngrok客户端
在同一目录创建配置文件 ngrok.cfg

```shell
server_addr: "ngrok.lrworkshop.xin:4443"
trust_host_root_certs: true
```
**工作室内部服务器，请勿泄露IP地址或域名以防滥用**
然后只需一行命令

```shell
./ngrok -config=ngrok.cfg -subdomain=admin 80
#-config 是配置文件的地址
#-subdomain 是你想要映射到外网的二级域名
#请不要使用www等常用二级域名防止冲突
#80 是本地服务端口
```

然后就可以直接访问https://admin.lrworkshop.xin 查看网页了

### TCP协议内网穿透

有时候我们希望内网的SSH服务或者shadowsocks服务在外网可以访问，这就需要TCP协议内网穿透

其他配置同上，命令有所不同
```shell
./ngrok -config=ngrok.cfg -proto=tcp 22
#不可指定二级域名，是Ngrok的设定
#映射端口不可指定，随机分配
```

### 批量端口映射

自行下载对应系统的Ngrok客户端
在同一目录创建配置文件 ngrok.cfg
```
server_addr: "ngrok.lrworkshop.xin:4443"
trust_host_root_certs: true
tunnels:
    ssh:
        remote_port: 158
        proto:
            tcp: 22
    vnc:
        remote_port: 5902
        proto:
            tcp: 5902
    dd:
        remote_port: 9208
        proto:
            tcp: 8888
    www:
        subdomain: 231
        proto:
            http: 80
```
**工作室内部服务器，请勿泄露IP地址或域名以防滥用**

然后启动
```shell
ngrok -config=ngrok.cfg start ssh vnc dd www
```
这样即可指定映射公网端口并批量映射服务
