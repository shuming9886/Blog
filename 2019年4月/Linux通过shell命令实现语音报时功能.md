---
title: Linux通过shell命令实现语音报时功能
date: 2019-04-08 16:52:11
tags:
    - Linux
---
# Linux通过shell命令实现语音报时功能

## 前言

上一周Linux操作系统实验课要求实现如题的功能，在网上查了一些资料发现网上很少有相关的内容，于是准备自己写一份。

## 别人的方法

使用Ubuntu系统自带的语音功能，然后将date命令的输出内容全部念出来，命令如下：

``$ espeak -vzh "现在时间是`date +%T|sed -e 's/:/时/1;s/:/分/1;s/$/秒/'`"``

保存成shell文件，我把他命名为`saytime.sh`。

在Linux终端运行它：

`$ bash saytime.sh`

尝试了一下系统自带的语音功能，效果确实比较差，所以强迫症的我开始选择另一种方法。

参考资料：<http://ju.outofmemory.cn/entry/228459>

## 我的方法

我所用的方法是调用百度的ttsAPI。首先，安装mplayer，mplayer是一个多功能多媒体播放器。

`$ sudo apt-get install mplayer`

创建一个shell脚本文件，

`$ gedit voice.sh`

```
#!/bin/bash

str="现在时间是`date +%T|sed -e 's/:/时/1;s/:/分/1;s/$/秒/'`"
wget "http://tts.baidu.com/text2audio?lan=zh&ie=UTF-8&spd=5&text=$str" -O - -o /dev/null |mplayer -cache 1024 ->/dev/null 2>&1
```

然后保存退出，运行此脚本：

`$ bash voice.sh`

## 实现定时功能

脚本已经有了，还有一个要求就是整点报时。可以想到是设置定时任务，让`voice.sh`在整点运行。命令`crontab`是`linux`任务计划功能，`-e`选项是指定计划任务。

`$ crontab -e`

进入vim界面，输入如下：

`0 * * * * sh 地址`

上述代码中的地址是`voice.sh`的绝对路径。例如：`/home/suda/voice/voice.sh`

Done!功能实现！

