---
title: “CloseAI”在美国，“OpenAI”在中国.md
author: 老章 mlpy
date: 2025-01-21 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---

大家好，我是章北海

今天中国版 OpenAI——`DeepSeek` 开源了最新、最强悍 R1 系列大模型
- DeepSeek-R1 推理大模型
- DeepSeek-R1-Zero
- R1 数据蒸馏的 Qwen、Llama 系列小模型

**DeepSeek-R1** 推理大模型，性能与 `OpenAI-o1-1217` 不相上下。

![](https://r2blog.zhanglearning.com/2025/01/8b53039fa68667303758ecdc0db71bab.png)

最惊艳的是 R1-Zero 模型（预训练模型直接 RL，不走 SFT）在思考过程中涌现了**“顿悟时刻”（aha moment）**，并自己学会为问题分配更多思考时间。
![](https://r2blog.zhanglearning.com/2025/01/1b3ae5497f423720fcd61743a502b5cd.png)

DeepSeek 团队开源了蒸馏的 Qwen 和 Llama 系列模型，蒸馏 14B 模型在推理基准测试中大幅超过了当前最先进的开源 QwQ-32B-Preview，而蒸馏的 32B 和 70B 模型在密集模型中树立了新的推理任务基准。

![](https://r2blog.zhanglearning.com/2025/01/90eab2fc8d125b80d0420f594d45a848.png)

团队还把在实验过程中很多失败的尝试分享出来，防止后人踩坑。在过程奖励模型、蒙特卡洛树搜索算法上，DeepSeek 都没能获得进展。不过他们也强调，只是他们失败了，并不意味着这些方法无法开发出有效的推理模型。

也就是，过程奖励模型、蒙特卡洛树搜索算法可能此路不通，但也可能是我们不行。

**运行 deepseek-r1**
![](https://r2blog.zhanglearning.com/2025/01/b32a80436be9b89f79a1795ea1865da0.png)

现在 ollama 一行代码

`ollama run deepseek-r1:7b` 即可跑起`deepseek-r1`

70 亿参数版本的本地运行，我测了一下

模型大小 4.7GB

![](https://r2blog.zhanglearning.com/2025/01/98579cb1ec9271903e04815493e4c70b.png)

运行起来之后，显存占用只有5.4GB

![](https://r2blog.zhanglearning.com/2025/01/9c04602c1faa2341e4060fd40b4f4b46.png)

实际对话，最明显的变化是可以看到它的思考过程

![](https://r2blog.zhanglearning.com/2025/01/ebce67c14cf77e167cdeecc91b289ed1.png)

更大尺寸的版本，我还在下载中，如果感受不错，我可能要抛弃Qwen2.5了。


这一波开源，我看很多评论把 DeepSeek 成为真正的 OpenAI，仅看开源协议就属实真诚了

🏆 DeepSeek-R1 采用 MIT 许可证，免费商用
🔓 向社区开放，以便利用模型权重和输出
🛠️ API 输出可用于微调与蒸馏


>MIT 许可证是源自美国麻省理工学院（Massachusetts Institute of Technology，MIT）的一种开源许可证。MIT 许可证是一种非常宽松的开源许可证，对软件的使用、修改和分发限制较少，给予了开发者极大的自由。


最后放一些列deepseek相关资源，共同学习：


- 网页体验：`https://chat.deepseek.com/`
- ollama：`https://ollama.com/library/deepseek-r1`
- API 手册：`https://api-docs.deepseek.com/guides/reasoning_model`
- 官方简介：`https://x.com/deepseek_ai/status/1881318130334814301`
- 基于 Gradio 的 deepseek-chatbot：`https://github.com/AK391/ai-gradio`
- 论文：`https://github.com/deepseek-ai/DeepSeek-R1/blob/main/DeepSeek_R1.pdf`
