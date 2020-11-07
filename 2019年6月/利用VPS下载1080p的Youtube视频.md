---
title: 利用VPS下载1080p的Youtube视频
date: 2019-06-17 11:08:11
tags:
    - 随笔
---

# 起因

前段时间刚好有想法想搬运油管的视频，在Github找了很多开源软件，效果不错，但是能在Windows系统中稳定运行的GUI软件实在是太少了。于是决定使用前段时间买的Digital Ocean的VPS下载视频。主机选择的是San Francisco，最便宜的套餐，每月5刀，**记得勾选ipv6**，系统选的是Ubuntu16.04。使用Github的学生优惠，可以赠送50刀，适合学生党使用。

## 小插曲

前段时间学校的教育网突然无法登录DO的VPS，就是用Putty无法登录，一直显示连接超时，但是我用手机4G给笔记本开热点就可以连接，当时心就凉了一半，心里想的是DO的ip被封了...难道薅的羊毛这么快就没了？

昨天闲来无事，不信邪，又去折腾了一下，结果惊呆了！我在教育网下用VPS的ipv6地址可以登录！

## 安装You-get

You-Get是一个命令行程序，我用它来下载油管的视频。当然它也支持很多视频网站门户。
此处放上you-get的中文介绍页面：https://github.com/soimort/you-get/wiki/%E4%B8%AD%E6%96%87%E8%AF%B4%E6%98%8E

下面是安装步骤：

1.安装python3-pip

`sudo apt install python3-pip`

2.通过pip安装

`pip3 install you-get`

3.大功告成，此时使用you-get已经可以下载视频

`$ you-get [url]`

url即为视频网站地址。你也可以使用`-i`选项来查看所有可用画质与格式。

```
$ you-get -i 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
site:                YouTube
title:               Me at the zoo
streams:             # Available quality and codecs
    [ DEFAULT ] _________________________________
    - itag:          43
      container:     webm
      quality:       medium
      size:          0.5 MiB (564215 bytes)
    # download-with: you-get --itag=43 [URL]

    - itag:          18
      container:     mp4
      quality:       medium
    # download-with: you-get --itag=18 [URL]

    - itag:          5
      container:     flv
      quality:       small
    # download-with: you-get --itag=5 [URL]

    - itag:          36
      container:     3gp
      quality:       small
    # download-with: you-get --itag=36 [URL]

    - itag:          17
      container:     3gp
      quality:       small
    # download-with: you-get --itag=17 [URL]
```

标有`default`为默认画质。

```
$ you-get 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
site:                YouTube
title:               Me at the zoo
stream:
    - itag:          43
      container:     webm
      quality:       medium
      size:          0.5 MiB (564215 bytes)
    # download-with: you-get --itag=43 [URL]

Downloading zoo.webm ...
100.0% (  0.5/0.5  MB) ├████████████████████████████████████████┤[1/1]    7 MB/s

Saving Me at the zoo.en.srt ...Done.
```

(如YouTube视频带有字幕，将被一同下载，以SubRip格式保存.)

如果不加任何参数，you-get下载的中等质量的视频，即不是分辨率最高的视频。对于我这个强迫症患者来说，这能忍？？

果断选择1080p视频，But下载后的视频的音轨和画面会分开，生成两个文件。这就相当难受了啊...

于是开始下一步，合并两个文件！

## 安装FFmpeg

FFmpeg可以将两个文件合并，生成一个完整的1080p视频！在网上搜索了很多ffmpeg的安装方法，相当麻烦，甚至有些需要长时间的编译，不过还好，找到一种方便快速的方法。

1.添加源

```
sudo add-apt-repository ppa:djcj/hybrid
```

2.更新源

```
sudo apt-get update
```

3.下载安装

```
sudo apt-get install ffmpeg
```

4.Done!安装成功！

这样下次下载1080p视频的时候，系统会自动将音频文件和视频文件合并。

以上。