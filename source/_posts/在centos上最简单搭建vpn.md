---
title: 搭建vpn最简单的方法
date: 2016-08-21 00:51:52
categories: [搭建vpn]
tags:
- 技术
- centos
---
<blockquote class="blockquote-center"><h1>搭建vpn最简单的方法在centos上</h1></blockquote>
![](http://i4.buimg.com/572447/c8068d7df031f6be.jpg)
<!--more-->
## 最近看了好多搭建vpn的方法都失败了，只有这个成功了。所以来分享:

## 第一步： 下载vpn(CentOS6专用)一键安装包

```
#wget http://www.hi-vps.com/shell/vpn_centos6.sh
#chmod a+x vpn_centos6.sh
```

## 第二步： 运行一键安装包

```
#bash vpn_centos6.sh
```

## 第三步：会有三个选择:
>1. 安装VPN服务<br>
>2. 修复VPN<br>
>3. 添加VPN用户<br>

>首先输入1，回车,VPS开始安装VPN服务（VPN服务安装完毕后会默认生成一个用户名为vpn，密码为随机数的用户来。

>此外需要添加新的VPN用户时，作如下操作,然后选择3，然后输入用户名和密码,OK
```
#bash vpn_centos6.sh
```
>4. 修复VPN服务
如果VPN拨号发生错误,可以试着修复VPN,然后重启VPS
#bash vpn_centos6.sh
选择2，然后reboot