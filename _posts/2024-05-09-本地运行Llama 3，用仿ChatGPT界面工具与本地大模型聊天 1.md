---
title: 本地运行Llama 3，用仿ChatGPT界面工具与本地大模型聊天 1.md
author: 老章 mlpy
date: 2024-05-09 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---


大家好，我是章北海

前几天我发布了一个视频：[《本地运行大模型，配合笔记应用王者 Obsidian 做知识管理》]()


这几天大模型开源世界又热闹起来了，因为 Meta 发布了 Llama 3。

我在这篇文章中详细介绍了Llama 3的两个版本和本地运行方法：

[《本地运行 Llama 3，可以中文，但不强》](https://mp.weixin.qq.com/s/MxZlAQ0ofZWIdte4KUY6oQ)

Ollama 目前支持了市面上几乎所有的开源大模型，安装后均可一个命令本地启动并运行。

模型下载完成后就可以直接在 Terminal 中聊天。

不过这种方式有点太麻烦了，很不优雅。
![](https://r2.zhanglearning.com/blog/2024/05/3d92d0425e6c8fc270df588ac61d99d0.png)


这里老章再推荐一个好用的工具，open-webui：https://github.com/open-webui/open-webui

![](https://raw.githubusercontent.com/open-webui/open-webui/main/demo.gif)

它是一个仿照 ChatGPT 界面，为本地大模型提供图形化界面的开源项目，可以非常方便的调试、调用本地模型。它支持各种运行器，还兼容 OpenAI 的 API。




open-webui用起来也很方便，最极简的安装、运行方法是使用 Docker

```shell
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

Terminal 中执行这行代码，稍等片刻，然后访问localhost:3000即可。

如果你的电脑还没有安装Docker，可以先安装一下，方法也很简单。

我直接安装了docker-desktop，下载后一路下一步即可：https://www.docker.com/products/docker-desktop/

open-webui还提供了用户注册与登陆功能，首次使用需要先注册一个账号：
![](https://r2.zhanglearning.com/blog/2024/05/d2523e230223811a70d09ba123c6a63d.png)

登陆后主页面如下，在这里可以选择我们刚刚运行起来的大模型，我的电脑性能太差，这里还拿 qwen 0.5b 做演示
![](https://r2.zhanglearning.com/blog/2024/05/87217b8fc0c3ee8031995fd86c6d0e7c.png)



然后就可以直接与本地大模型聊天了

![](https://r2.zhanglearning.com/blog/2024/05/1cf58d1d957897af9be58224e9e7ace7.png)


open-webui 前端界面功能还蛮多的，感兴趣的小伙伴可以本地跑起来试试。

open-webui 前端界面功能：
- 🖥️ 直观的界面
- 📱 响应式设计  
- 💻 代码语法高亮
- 🔢 全面的Markdown和LaTeX支持
- 📚 本地RAG集成
- 🌐 网络浏览能力
- 📜 提示预设支持  
- 👍 RLHF注释
- 🏷️ 对话标记
- 🗑️ 下载/删除模型
- ⬆️ GGUF文件模型创建
- 🤖 多模型支持
- 🧩 模型文件构建器
- ⚙️ 多模型对话
- 💬 协作聊天
- 📥 导入/导出聊天历史  
- 🗣️ 语音输入支持
- ⚙️ 通过高级参数进行微调控制
- 🤖 图像生成集成
- 🤝 OpenAI API集成
- 🔗 外部Ollama服务器连接
- 🔀 多个Ollama实例负载均衡
- 👥 多用户管理
- 🔐 基于角色的访问控制（RBAC）
- 🔒 后端反向代理支持
- 🌍 多语言支持

好了，本文此结束啦，如有帮助，可以给我一个三连吗？爱你呦！