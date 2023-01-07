

人人都知道学习很重要，学习究竟是为了什么呢？根本目的只有一个，学以致用！

机器学习，大家都学了很多算法，搞了很多模型，但是极少拿来解决实际问题。

毕竟开发一个机器学习应用需要的技术栈不是每个人都能掌握，今天就向同学们介绍一个绝佳解决方法————`streamlit`

它可以让你用Python用极短的时间快速生成一个``实现机器学习的web应用``

正式介绍之前，大家可以先看几个效果Gif（刷新可能有点慢，请耐心等待）

![Hello world](https://my-wechat.oss-cn-beijing.aliyuncs.com/downloaded-GIF%20(1)_20211204232814.gif)

![Playground](https://my-wechat.oss-cn-beijing.aliyuncs.com/33_20211205225115.gif)


![YOLO 目标检测器](https://my-wechat.oss-cn-beijing.aliyuncs.com/complex_app_example%20(1)_20211204233012.gif)


## streamlit

Streamlit 是第一个专门针对机器学习的应用开发框架，是开发自定义机器学习工具最快的方法，它的目标是取代Flask在机器学习项目中的地位。

![streamlit引用的第三方库](https://my-wechat.oss-cn-beijing.aliyuncs.com/Screen%20Shot%202021-11-24%20at%2010.33.45%20AM_20211124103453.png)

Streamlit 带给我最大好感的有以下几点：

- 开源、完全免费
- 极其容易入门、一天就能学会
- API 非常丰富且简单明了

下面我们就开始吧！


## Get started

在命令行模式下，启动Python虚拟环境后，直接pip安装
```
$ pip install streamlit
```

![test.py](https://my-wechat.oss-cn-beijing.aliyuncs.com/image%20(3)_20211205000844.png)

命令行模式下执行`streamlit run test.py`

现在可以在浏览器中查看Streamlit应用程序。

![本地URL: http://localhost:8501](https://my-wechat.oss-cn-beijing.aliyuncs.com/122221_20211205000859.gif)

是不是超简单

## Deploy
有了应用就要部署到服务器，如果不想买云服务器怎么办呢？
`streamlit` 连部署都是免费的！没想到吧。

首先，把项目push到你的github

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/image_20211205105208.png)

在刚才打开的http://localhost:8501页面右上角点击 `Deploy this app`

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/image_20211205105305.png)

Streamlit Cloud会链接到你的github，认证一下即可

![认证一下即可](https://my-wechat.oss-cn-beijing.aliyuncs.com/image_20211205104207.png)


![然后选择`Deploy！`稍作等待](https://my-wechat.oss-cn-beijing.aliyuncs.com/image_20211205104637.png)


![https://share.streamlit.io/tjxj/test/main/bar.py](https://my-wechat.oss-cn-beijing.aliyuncs.com/image_20211205105831.png)

现在，你的应用已经部署到互联网了


![手机也能访问哦~](https://my-wechat.oss-cn-beijing.aliyuncs.com/0ccd23a90830a26ecfd8d9a4ee00726_20211206211752.jpg)

## 学习路线

一天时间学会``streamlit``我觉得并不夸张  
只看它的官网文档就足够了
https://docs.streamlit.io/library/

- Get started  √  
理解基本原理和用法
- API reference  √  
知道有哪些api可以调用
- cheatsheet  √  
api速查表，可以时时看看

如果要进阶，就可以去``https://streamlit.io/gallery``,学习他人优秀的作品（都是开源的）。比如，本文中的几个Gif就是用的这个

![https://share.streamlit.io/pavankunchala/gif_converter_app/main/convert_app.py](https://my-wechat.oss-cn-beijing.aliyuncs.com/image_20211205003241.png)


当然，最好的方法永远是自己写一个应用~ ，下一篇，我会用视频分享一下我写的机器学习应用，感兴趣来个三连支持哈。
