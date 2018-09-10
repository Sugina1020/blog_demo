﻿# 优知[英文版](http://192.168.14.240:3000/caolinan/blog_daemon/src/master/README.md)

一个轻量级的博客，将文章上传至ulord平台并进行定价，其他用户付费查看。所有交易信息均可通过ulord区块浏览器查阅

## 特性

> * 资源定价
> * 所有资源都可在ulord平台上查阅
> * 所有交易均可在ulord平台查看
> * 文章上传至ulord平台上，服务端不必担心存储
> * windows 环境
> * linux 环境
> * 多类型数据库，支持sqlite、mysql、postgresql等
> * 配置简单
> * 当用户请求数据时，会先将数据库的数据给用户，后台定期用web3同步相关数据

## 安装
### 安装 python 和 pip
首先安装 python3.6 可以在[官网](https://www.python.org/)上下载

然后安装pip来管理你的python包

第三包使用pip来安装所需要的软件包
```bash
pip install -r requirements.txt
```
### 安装ipfs的go版客户端

go-ipfs是ipfs的go版客户端。通过它就可以连接到ipfs网络中。修改配置之后你就可以连接到ulord平台的ipfs平台中去。

你可以在[这里](https://github.com/ipfs/go-ipfs/releases/tag/v0.4.14)下载go-ipfs，根据你自己的系统环境去下载对应的版本。

需要在环境变量设置一下来使用ipfs。

##### windows

你可以使用 Tools/ipfs/install.bat 脚本安装ipfs。它是把ipfs.exe程序复制在你系统环境文件夹中
> 注意:默认你的系统换件文件夹是"C:\Windows\System32"。所有如果你的系统环境不在那里你应该手动修改脚本文件然后再执行。
```bash
ipfs init
ipfs bootstrap rm --all
ipfs bootstrap add /ip4/114.67.37.2/tcp/20418/ipfs/QmctwnuHwE8QzH4yxuAPtM469BiCPK5WuT9KaTK3ArwUHu
ipfs config Datastore.StorageMax "1MB"
ipfs daemon
```
#### linux

你可以使用 Tools/ipfs/install.bat 脚本安装ipfs。它是把ipfs.exe程序复制在你系统环境文件夹中
> 注意:默认你的系统换件文件夹是"/usr/local/bin/"。所有如果你的系统环境不包含那里你应该手动修改脚本文件然后再执行。


用下面的命令来初始化ipfs(Windows/Linux):
```bash
ipfs init
ipfs bootstrap rm --all
ipfs bootstrap add /ip4/114.67.37.2/tcp/20418/ipfs/QmctwnuHwE8QzH4yxuAPtM469BiCPK5WuT9KaTK3ArwUHu
ipfs config Datastore.StorageMax "1MB"
```

##### 让IPFS处于后台服务中
以下是基于 Ubuntu Service   
```bash
cd /lib/systemd/system/
nano ipfs.service
```
粘贴以下代码让IPFS遇到故障后能自动重启服务。
```bash
[Unit]
Description=IPFS
[Service]
ExecStart=/usr/local/bin/ipfs daemon
Restart=always
User=root
Group=root
[Install]
WantedBy=multi-user.target
```
启动服务：
```
systemctl start ipfs
```


## 运行
```bash
python server.py
```

