---
title: 别随便本地部署DeepSeek了，Ollama重大安全隐患.md
author: 老章 mlpy
date: 2025-02-13 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---

大家好，我是章北海

最近 DeepSeek 大火，市面上教人本地部署大模型的文章、视频众多

多数都是用 Ollama 一行命令就启动模型了

但是最近爆出 Ollama 启动大模型可能存在安全隐患

**在 FOFA 上可以轻而易举地发现众多暴露在互联网上的 Ollama 11434 端口**

![](https://r2blog.zhanglearning.com/2025/02/3a46cdda1c0be8fa297bf0e923646440.png)


>FOFA 是一个网络空间测绘平台，周期性不间断对全球互联网暴露资产进行深度扫描与探测，通过多种方式进行资产检索，全面发现互联网暴露资产，对资产进行画像管理

随便找一个广东网友的 ip

他这电脑很豪，部署了 DeepSeek R1 70B

![](https://r2blog.zhanglearning.com/2025/02/5a6e0569802b5e3ebe42470db8ee21cd.png)

试了一下，但是没有跑起来

又找了一个广东网友的，他部署了 R1 1.5B
![](https://r2blog.zhanglearning.com/2025/02/847dc20d99fde1f7e038f577fc0b26a6.png)

然后我就成功地用他的电脑发起了一次对话

![](https://r2blog.zhanglearning.com/2025/02/b44c6b83d39d10f8ef99bcefd48626b4.png)

我甚至可以将他的 ip 配置到任意一个 chatbot
![](https://r2blog.zhanglearning.com/2025/02/ef64c404a6007d89f221802d3a11f7ac.png)

然后就可以无损、免费对话了

![](https://r2blog.zhanglearning.com/2025/02/9b478c63eef5e8a3b50b855a2b3c8fbc.png)

我搜了一下，发现Ollama安全隐患一事早在去年就以爆出
![](https://r2blog.zhanglearning.com/2025/02/9404374a18d01ee793635f0912699ec1.png)

>“未经授权将Ollama暴露给互联网，等同于将Docker套接字暴露给公共互联网，因为它可以上传文件，并且具有模型拉取和推送能力（可能被攻击者滥用）。”Lumelsky指出。

Ollama 完全不能用了吗？

也不尽然，做好安全防护即可，不要在没有防火墙策略情况下将其配置为监听所有IP（0.0.0.0）

![](https://r2blog.zhanglearning.com/2025/02/7f8f6fa173b98b504226551291b8e50d.png)
相对安全做法：将 Ollama 只监听本地地址 export OLLAMA_HOST=127.0.0.1

检查是否只监听本地命令： netstat -an | grep 11434`

应该只看到 127.0.0.1:11434 的监听，而不是 0.0.0.0:11434

同时做好防火墙策略：


```bash
# MacOS 配置方法

# 检查端口

sudo lsof -i :11434

# 使用内置防火墙

sudo /usr/libexec/ApplicationFirewall/socketfilterfw --add /path/to/ollama

sudo /usr/libexec/ApplicationFirewall/socketfilterfw --block /path/to/ollama
```


```powershell
# Windows 配置方法
或通过图形界面：

打开 Windows Defender 防火墙高级设置
右键"入站规则" → "新建规则"
选择"端口" → TCP → 特定本地端口：11434
选择"阻止连接" → 应用到所有配置文件

# 或者PowerShell命令

New-NetFirewallRule -DisplayName "Block Ollama" `

-Direction Inbound `

-LocalPort 11434 `

-Protocol TCP `

-Action Block

  

New-NetFirewallRule -DisplayName "Block Ollama Outbound" `

-Direction Outbound `

-LocalPort 11434 `

-Protocol TCP `

-Action Block
```



```bash
# Ubuntu/Debian
# 使用 UFW

sudo ufw deny 11434/tcp

  

# 或使用 iptables

sudo iptables -A INPUT -p tcp --dport 11434 -j DROP

sudo iptables -A OUTPUT -p tcp --dport 11434 -j DROP
```


```bash
# CentOS/RHEL
# 使用 firewall-cmd

sudo firewall-cmd --permanent --add-port=11434/tcp --zone=public

sudo firewall-cmd --permanent --remove-port=11434/tcp --zone=public

sudo firewall-cmd --reload

```
验证配置

在所有系统上都可以使用以下命令验证：

```bash

# 检查端口监听状态

netstat -an | grep 11434

  

# 尝试从其他机器连接（应该失败）

curl http://[服务器IP]:11434/api/generate

```

  最后声明一下，勿作恶