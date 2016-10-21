---
title: CentOS7安装shadowsocks
date: 2016-10-21 17:29:28
categories: [linux学习]
tags:
- linux学习
- CentOS
---
<blockquote class="blockquote-center"><h1> CentOS7安装shadowsocks以及添加ssh-key</h1></blockquote>
![Google](http://123.206.20.249/wp-content/uploads/2016/10/20161021172211.png)
<!--more-->
##<b>centos添加本机的sshkey</b>
>登录远程Linux  VPS/服务器,并在.ssh目录下添加文档authorized_keys并加入自己的sshkey，执行：<br>
```c++
ssh-keygen -t rsa
```
##<b>安装shadowsocks：</b>
>在vps上执行如下命令：<br>
```c++
wget http://mirrors.linuxeye.com/oneinstack.tar.gz
tar xzf oneinstack.tar.gz
cd oneinstack
./shadowsocks.sh install
```
>添加用户执行如下命令:
```c++
./shadowsocks.sh adduser
```

##<b>会遇到的问题</b>
>1.连接不上:<br>
<ul>
	可能CentOS 7 默认防火墙为 Firewall 被开启<br>
		>添加自己的端口到防火墙：<br>
		```c++
		firewall-cmd --permanent --add-port=9001/tcp
		firewall-cmd --reload
		```
		>若最后发现还是连接不上，之间关闭防火墙:<br>
		```c++
		 systemctl stop firewalld.service
		```
</ul>

##<b>Shadowsocks 服务管理命令：</b>
```c++
systemctl start shadowsocks
systemctl stop shadowsocks
systemctl restart shadowsocks
systemctl status shadowsocks
```
























