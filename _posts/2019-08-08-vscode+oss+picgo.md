---
title: vscode+oss+picgo
author: cotes
date: 2019-08-08 14:10:00 +0800
categories: [Blogging, Tutorial]
tags: [writing]
render_with_liquid: false
---

大家一定不要随便立flag

10月份发了个朋友圈，有好兄弟留言说写个教程，我说好

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106100426.png)


然后一忙起来就忘了，昨天好兄弟追到知识星球，在一个新flag帖子下催更了
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106100653.png)

写个无废话极简

## VSCode
从这下载：https://code.visualstudio.com

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106101405.png)

安装就是一路下一步就行


## OSS
去阿里云注册个号

https://www.aliyun.com/

我们需要的是`对象存储OSS`，进去点立即开通就行了，所有选项都选最低配，足够用了。挺便宜的，每个月三四块钱。

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106102412.png)


建议直接购买资源包，一年9元钱。

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106102843.png)

完事儿进入OSS控制台

https://oss.console.aliyun.com/overview

点击左侧Bucket列表，创建Bucket，填写好名称，选择好地域就行


![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106105941.png)

记住你的`Bucket名称和Endpoint地址`，一会儿要用

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106110009.png)

搞定之后鼠标移动到页面右上角你头像，然后点击`AccessKey管理`
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106103111.png)

进来之后点击创建AccessKey
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106103414.png)

把ID和Secret复制出来，一会儿要用
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106103345.png)

## PicGo

打开VSCode之后就这样，点击侧边插件，搜索Picgo，然后安装，下图是我安装好的样子

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106102106.png)

装好之后点击⚙️，点击设置

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106103705.png)

设置页面拖到这里

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106104107.png)

把刚才提到一会儿要用的ID、Secret、Area、Bucket、Url（Endpoint地址前面加上bucket名，注意格式）填进去

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106110610.png)


PicGo使用也很简单

在VSCode新建一个Markdown文件，比如此文就是

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106111405.png)

可以使用QQ或微信截图，也可以复制本地图片，然后在VSCode中通过Ctrl+Alt+u的快捷键将剪切板中的图快速插入。


## Github 备份

https://github.com/

这没啥好说的，在Github新建一个私有仓库，专门用来同步自己的文章，防丢失，还能做版本控制。

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106112218.png)

## 文章主题美化

此类工具很多，我喜欢用https://editor.mdnice.com/

本文就是用它美化的

把Markdown内容粘贴到编辑框,里面主题有很多
![](https://my-wechat.oss-cn-beijing.aliyuncs.com/20230106111905.png)

右侧可以复制，粘贴到公众号、知乎或者别的博客平台都可以。

