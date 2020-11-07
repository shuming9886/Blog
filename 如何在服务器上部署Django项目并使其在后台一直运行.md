---
title: 如何在服务器上部署Django项目并使其在后台一直运行
date: 2018-12-27 20:54:05
tags:
    - 随笔
---

## 前言
前几天老师让我把一个Django项目（爬虫网页）放到校园内网上，但是我想先用自己的服务器来尝试一下。之前刚好有在Digital Ocean上买过服务器用来运行ss脚本，平时服务器一直放着没啥用，所以就拿它来试验一下。

## 第一步
废话不多说，第一步通过WinSCP软件把Django文件传到服务器上。

## 第二步
在服务器中安装Django需要的环境和我所需要的Python第三方库。

## 第三步
以上所有步骤完成后，还需要进行一步操作，这是我经历的一个**坑**。 打开Django文件目录中的*settings.py* ，把`ALLOWED_HOSTS=[]`改为`ALLOWED_HOSTS=["*"]`。

## 最后一步
在服务器中打开到*manage.py*所在的目录，输入命令：
`python3 manage.py runserver 0.0.0.0:8000`
然后按下回车，在浏览器中输入：`该服务器IP地址:8000`，大功告成！

*Attention:*
1.`python3`不是特定的，是根据你的Django项目所需要的环境指定的。
2.`8000`是端口号，可以修改。

## 后台运行
如果想要Django项目一直运行，关闭终端后还在运行，即需要运行如下命令，`nohup command &`，`command`即位上文所说的`python3 manage.py runserver 0.0.0.0:8000`。