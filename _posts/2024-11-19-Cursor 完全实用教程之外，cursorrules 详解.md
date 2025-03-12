---
title: Cursor 完全实用教程之外，cursorrules 详解.md
author: 老章 mlpy
date: 2024-11-19 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---



![](https://r2.zhanglearning.com/blog/2024/11/9e99ac2ef53a33e97277771f36faef94.png)


大家好，我是章北海

之前推过两篇文章详细介绍 Cursor 这个神级代码编辑器：[Cursor 完全使用教程](https://mp.weixin.qq.com/s?__biz=MzA4MjYwMTc5Nw==&mid=2648990189&idx=1&sn=3c34f37012529c85f6af859c98e726aa&chksm=8793f3c7b0e47ad109fc12e5cdaef0876126895b7646c2aa55a47630ae25286ce67f2782b9b8&token=1648794801&lang=zh_CN#rd)、[迄今最好的AI代码编辑器，编程只需狂按Tab](https://mp.weixin.qq.com/s?__biz=MzA4MjYwMTc5Nw==&mid=2648989931&idx=1&sn=4891dd8c1583e4d6e07a8b6039359fd5&scene=21#wechat_redirect)
还在[【大模型实战，完整代码】AI 数据分析、可视化项目](https://mp.weixin.qq.com/s?__biz=MzA4MjYwMTc5Nw==&mid=2648991069&idx=1&sn=2d7cfea4c9a2a38824ffacae7dc0e352&chksm=8793f777b0e47e615407c60c6b065f696656083a0ff86d43d5f89a389fae18bab10bcb7b6042&payreadticket=HE-JE-rKiwH1Fwxr03rk8H6Fd1xuHj1pLBswFZ7_C_hZmW7eUpmjP3wTJWpfAZdQnyuPSWY#rd)这篇文章介绍了借助 Cursor + Claude 开发一个完整的项目。

今天探讨下 Cursor 中`Rules for AI`和`.cursorrules` 的关系、优先顺序及用法。

![`Cursor Settings` > `General` > `Rules for AI`](https://r2.zhanglearning.com/blog/2024/11/0f24c98f72b6ab5600dc862abfc137d8.png)

Rules for AI 用过的应该都熟悉，设置中填写Rules，即可在Cursor Chat 和 Ctrl/⌘ K 时生效，有点类似 system prompt。

设置中还有个`.cursorrules` 它是干什么用的呢？官方简介说：

- 定制 AI 行为： `.cursorrules` 文件有助于根据项目特定需求调整 AI 的响应，确保更相关和准确的代码建议。
    
- 一致性：通过在 .cursorrules 文件中定义编码标准和最佳实践，可以确保 AI 生成的代码与项目样式保持一致。
    
- 上下文意识：可以向 AI 提供关于项目的重要上下文信息，例如常用方法、架构决策或特定库，从而实现更具有洞察力的代码生成。
    
- 提高生产力：通过明确的规则，AI 可以生成需要更少手动编辑的代码，加速您的开发过程。
    
- 团队对齐：对于团队项目，共享 .cursorrules 文件确保所有团队成员获得一致的 AI 辅助，促进编码实践的一致性。
    
- 项目特定知识：可以包含有关项目结构、依赖关系或独特需求的信息，帮助 AI 提供更准确和相关建议。
    

与`Rules for AI`相同，“. cursorrules”文件中的说明将包含 Cursor Chat 和 Ctrl/😍K 等功能。

看起来有点厉害，.cursorrules 文件长什么样呢？

参考这个网站 https://cursor.directory

>网站涵盖 **Python****、FastAPI、****Django****、Next.js、****TypeScript****、Node.js** 等多种主流语言或框架，旨在通过这些配置使 Cursor 提供更好的代码补全、错误修复等功能。
**支持语言与框架** ：目前已支持到 30 多个。


![不同项目要支持不同的 cursor rules，就把 `.cursorrules` 加到项目根目录底下](https://r2.zhanglearning.com/blog/2024/11/9f20e3ce0908c980bd21753f92a1cdef.png)


比如你的项目可能是Python数据可视化的，可能是机器学习建模的，可能是前端、后端的，从网站中复制cursorrules，然后在项目根目录中创建一个 `.cursorrules` 文件粘贴rules即可。

或者

从`https://github.com/PatrickJS/awesome-cursorrules/tree/main/rules`直接下载 `.cursorrules` 文件到项目根目录。

![](https://r2.zhanglearning.com/blog/2024/11/bcae12f966f302129edcb4f0bc697897.png)

据我自己的测试，有几个结论：
1、Rules for AI 作用于.cursorrules 之前
2、workspace 中多个文件夹，第一个文件夹下的.cursorrules 起作用

我看有人说

>当你在进行项目时，你可能会在工作空间中打开多个仓库。一个用于后端，一个用于前端，... 每个仓库可能有自己的语言（例如，后端使用 python/fastapi，前端使用 JS/React）。然后你可能需要为每个仓库创建一个单独的.cursorrules 文件，每个文件中的规则适应于每个仓库中的你的技术栈。

目前看，貌似无法实现。

最后再推荐一个工具吧，可以帮你打造适合自己项目的cursorrules：

https://cursorrules.agnt.one/chat


至此

本文如有帮助，敬请【在看】，感谢🙏

