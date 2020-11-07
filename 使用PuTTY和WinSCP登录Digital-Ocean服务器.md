---
title: 使用PuTTY和WinSCP登录Digital Ocean服务器
date: 2018-10-09 20:56:24
tags:
    - 随笔
---
## 前言

前段时间为了学习，在Digital Ocean上开通了VPS服务器，使用的是linux系统，每月5＄。虽说有点小贵，但是毕竟是自己搭建的，相较于其他提供服务的网站，可能唯一的优点就是稳定:) 之前都是在Git Bash中配置linux服务器，由于之前没认真研究过linux的操作方法，也是照着百度瞎敲。但是这学期的编译原理课程实践要求使用Ubuntu系统，在linux终端中编写运行python文件，而我的电脑也没安装Ubuntu系统，所以想着在linux服务器中跑python文件。


---
### 1.PuTTY和WinSCP是啥

PuTTY是一个Telnet、SSH、rlogin、纯TCP以及串行连接软件。特点就是完全免费，**绿色软件、无需安装、下载后再桌面建个快捷方式即可使用**，体积小，操作简单。用它来远程管理Linux十分好用。

下载地址：[PuTTY下载地址][1]

WinSCP是一个Windows环境下使用SSH的开源图形化SFTP客户端。同时支持SCP协议。它的主要功能就是在本地与远程计算机间安全的复制文件。简单来说，**将服务器中的文件图形化界面展示出来，可以在随意拖拽文件到服务器和本地**。

下载地址：[WinSCP下载地址][2]

### 2.SSH密钥

虽然可以使用基于密码的登录管理服务器，使用SSH密钥对会更好。SSH密钥比密码更安全，并且可以帮助您登录，而无须记住长密码。

用**PuTTYgen**来生成SSH密钥，**PuTTY**创建SSH会话，连接服务器。SSH密钥对分为公钥和密钥，公钥可以对外公布，密钥自己保管，同来连接服务器。

PuTTY、PuTTYgen下载地址相同。

![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-putty.png)

### 3.创建SSH密钥对

打开**PuTTYgen,点击Generate按钮**
**注意！！！！点击完按钮后，必须在读进度条时鼠标一直在界面上滑动，不然进度条是走不动。我就是等了十几分钟后，进度一点都没动，一度以为电脑坏了...**
![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-putty-01.jpg)

生成完后，**点击Save private key生成一个.ppk文件，将它保存在你的电脑中的某个易于找到的位置，因为待会要用。界面不要关闭！**
**复制上方的公钥密码**
![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-putty-02.jpg)

### 4.上传公钥到Digital Ocean

在Digital Ocean网站上，点击ACCOUNT->Security->SSH keys,**点击ADD SSH Key**。


![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-putty-03.jpg)

将刚才复制的公钥复制上去，随意取个名字。点击**CREATE SSH KEY**。

### 5.PuTTY使用SSH Key登录VPS流程

首先，打开PuTTY软件，在HostName(or IP address)空格处输入 **root@你的服务器IP**。端口(一般为22)，然后点击**SSH ->Auth**



![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-putty-04.jpg)

然后在**Private key file for authentication**选项选择你的**SSH私钥的路径(后缀为.ppk)**，然后到登录页**点击Default Setting ->Save 保存设置**

![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-putty-05.jpg)

最后，点击Open进入界面。

### 6.WinSCP使用SSH Key 登录VPS流程

首先打开WinSCP。

![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-putty-06.jpg)

选择SFTP。第一步输入你的主机域名或者IP。端口为22.第二步用户名为root。第三步点击高级。

选择SSH -> 验证：添加私钥

![](https://gitee.com/shuming9886/pic-go/raw/master/img/2020-10-24-putty-07.jpg)

最后完成，登录。



[1]: https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
[2]: https://winscp.net/eng/download.php

