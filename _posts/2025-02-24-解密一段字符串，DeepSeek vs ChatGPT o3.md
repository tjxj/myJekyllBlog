---
title: 解密一段字符串，DeepSeek vs ChatGPT o3.md
author: 老章 mlpy
date: 2025-02-24 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---

**太长不看：**
最聪明的是 ChatGPT o3，也只有他完成了解密

![](https://r2blog.zhanglearning.com/2025/02/553e42776489adda74a09de3c823b77a.png)


大家好，我是 Ai 学习的老章

周末无聊测试了一下大模型的智商

方式：先用 Base64 把中文加密，然后看看哪些大模型可以完成解密

> Base64 是网络上最常见的用于传输 8Bit 字节码的编码方式之一，包括小写字母 a-z、大写字母 A-Z、数字 0-9、符号"+"、"/"一共 64 个字符的字符集，（任何符号都可以转换成这个字符集中的字符，这个转换过程就叫做 base64 编码。

![](https://r2blog.zhanglearning.com/2025/02/96257b6670645a7d7f4e89204a3b46c4.png)

先测试了通用模型

明显不靠谱，豆包、通义千问，Claude-3.5-Sonnet 都不行。

![](https://r2blog.zhanglearning.com/2025/02/5488512548c0d6ccf4cacf1f09dd839e.png)

 Claude 3.5 Sonnet 识别出了这是经 Base64 编码的，但是解码失败
![](https://r2blog.zhanglearning.com/2025/02/3ad3514b2e7e7c171baeaa29dcac1bd0.png)
![](https://r2blog.zhanglearning.com/2025/02/72e840b7a1e24e84ce2c07da524bb24f.png)


只能上推理模型了，先试试 DeepSeek

开启了漫长的思考

![](https://r2blog.zhanglearning.com/2025/02/eb97088799926a95abec70ed76eb0c86.png)


耗时 398 秒，整整六分钟，深度思考中它换了 N 多种方式，确定了是 Base64 编码，但是解密是错误的。

![](https://r2blog.zhanglearning.com/2025/02/861694b6b7e390b498faaf50b6756613.png)

一直霸榜的 ChatGPT O3，我网络和账号都不太好，只能用 windsurf 中的 o3-mini，结果是秒出，结果正确✅

![](https://r2blog.zhanglearning.com/2025/02/334dc7b9800b429b5c3610c3110c5957.png)

![](https://r2blog.zhanglearning.com/2025/02/553e42776489adda74a09de3c823b77a.png)


号称[[250220 马斯克还可以，“地球上最聪明的人工智能”Grok-3免费了]]

正常模式解密失败，Think 模式，经过 126 秒的思考，结果错误


![](https://r2blog.zhanglearning.com/2025/02/a4ce61438fcb9aacb712cf141a9eb44e.png)
![](https://r2blog.zhanglearning.com/2025/02/4f0c108bc496e008b6f482583df85944.png)





DeepSeek 很强，但是还是不够强

我又重看了一下榜单，目前 o3 还是第一

马斯克的 Grok-3 号称超越了 o3-mini

这个解密任务而言，Crok-3 完全被 o3-mini 碾压了

![](https://r2blog.zhanglearning.com/2025/02/15541c8363c65a3c0f164ff8aca5c8ad.png)



