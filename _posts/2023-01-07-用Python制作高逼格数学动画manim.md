---
title: 用Python制作高逼格数学动画manim
author: 老章mlpy
date: 2023-01-07 14:10:00 +0800
categories: [Python]
tags: [python,manim]
render_with_liquid: false
---

## 简介
manim是斯坦福大学数学系小哥Grant Sanderson开源的数学仿真模拟python库，并用于YouTube 频道3Blue1Brown，来解说高等数学。  

manim是一个非常优秀的数学动画制作引擎，先来两个GIF感受一下 manim 的魅力：
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/ece58e52bb1fb59a109dfcd550cd062d_20211023211014.jpg)

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/ad1583d96ce7e290fe4b68f01a9ec24f_20211023211032.jpg)

很多同学应该在 B 站看过3b1b的视频，最经典的就是线性代数的本质系列。
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/image_20211023210452.png)


## 版本说明

manim 初学者可能会有些许困惑，网上的代码、文档、教程等差异太大，不知道该跟着那个学习。 

目前manim有三个版本：

![by：鹤翔万里 & widcardw](https://my-wechat.oss-cn-beijing.aliyuncs.com/image_20211026114738.png)

**3b1b 旧版**：3blue1brown 自己维护的版本，使用 Cairo 作为后端。  
**3b1b 新版**：3blue1brown 自己维护的版本，使用 OpenGL 和 moderngl 来进行 GPU 渲染，优点是速度快。  
**manim 社区版**：manim 旧版的衍生，更新更活跃，有很好的文档和社区支持。

我比较信任Grant Sanderson 大神，所以直接学习了新版。

## manimgl 环境搭建
manimgl 这个版本的安装特别简单


**1、安装配置FFmpeg和LaTex**  
https://ffmpeg.org/download.html 
FFmpeg，下载安装即可，把安装路径添加到环境变量即可

https://mirror.ctan.org/systems/texlive/tlnet/install-tl-windows.exe  
LaTex更简单，一路下一步即可。

**2、创建虚拟环境**  
```
conda create -n manim python=3.8
conda activate manim
```

**3、安装manimgl包**  
```
pip install manimgl
```
也可以clone最新的源码进行安装
```
git clone https://github.com/3b1b/manim.git
cd manim
pip install -e .
```
这样还能测试一下是否安装成功了。
```
manimgl example_scenes.py OpeningManimExample
```
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/1222_20211026225532.gif)

## 学习资源

官方文档：  
https://3b1b.github.io/manim

中文文档:  
https://docs.manim.org.cn/

3b1b 视频源码：  

https://github.com/3b1b/videos  

manim 源码：  
https://github.com/3b1b/manim  

学习顺序，可以先看中/英文文档，然后就动手制作自己的动画吧。  
如有余力，可以抽空看看3b1b的视频源码，如果能为manim贡献代码就更好了。

最近在youtube上看到了一个用 manim 制作了数据结构与算法的视频，挺强的。

视频源码：https://github.com/nipunramk/Reducible
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/image_20211026170407.png)

祝大家学的愉快，也欢迎交流学习，这一块我也是小白呢。
