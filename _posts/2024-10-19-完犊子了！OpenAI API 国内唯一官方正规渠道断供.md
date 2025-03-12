---
title: 完犊子了！OpenAI API 国内唯一官方正规渠道断供.md
author: 老章 mlpy
date: 2024-10-19 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---


大家好，我是章北海

前天，收到一封微软来信

大致意思，Azure 将在2024年10月21日不再向个人提供OpenAI API服务

![](https://r2.zhanglearning.com/blog/2024/10/604d9ba18e2cbd9d8db3f8799506aa13.png)

OpenAI API 国内个人用户唯一官方正规渠道断了

我自己部署到chatbot用的就是微软Azure OpenAI 的GPT-4o

![](https://r2.zhanglearning.com/blog/2024/10/19feade5491154512f1920478a52a4c1.png)


这下彻底玩完了

既然不让用，老子就不用了

还TM的死贵死贵的

我准备彻底转向siliconflow了

[我的另一个应用自动化数据分析就用了siliconflow的api](https://mp.weixin.qq.com/s?__biz=MzA4MjYwMTc5Nw==&mid=2648991069&idx=1&sn=2d7cfea4c9a2a38824ffacae7dc0e352&chksm=8793f777b0e47e615407c60c6b065f696656083a0ff86d43d5f89a389fae18bab10bcb7b6042&payreadticket=HLE664zqpZOziyXyb6N3r38he-tflds0SzDbwtvmm0lbBOHamDd-8amJChBzGB9LjOdxmm8#rd)

它免费赠送 14 元（即约 2000 万 Qwen1.5-14B 模型 tokens，或 500 张图片）
![](https://r2.zhanglearning.com/blog/2024/07/61071fab450b870e047b7acdc43775af.png)

注册地址：`https://cloud.siliconflow.cn?referrer=cly7ai3ir000jqab7qaqp0qwf`

它提供了大量国内外的大模型

更菩萨的是，它提供了很多免费模型！！！

还可以免费使用`Qwen、GLM、Yi `等模型。

注册后免费赠送 14 元（够用很久很久，用 deepseek 翻译了一本 40 页的 pdf，只花了几分钱）

注册地址：https://cloud.siliconflow.cn/i/YefhGWlT


![支持的模型列表：https://cloud.siliconflow.cn/models](https://r2.zhanglearning.com/blog/2024/10/4e53fc237fd379f49a82e72606f849c3.png)

api 获取地址：https://cloud.siliconflow.cn/account/ak

![](https://r2.zhanglearning.com/blog/2024/10/38ab7d06a2fb735a1c190a7d6b02d573.png)

用法：

当前大语言模型部分支持以 openai 库进行调用，安装 Python3.7.1 或更高版本并设置虚拟环境后，即可安装 OpenAI Python 库。

从终端/命令行运行：

```shell
pip install --upgrade openai
```

完成此操作后，running 将显示您在当前环境中安装的 Python 库，确认 OpenAI Python 库已成功安装。 

之后可以直接通过 OpenAI 的相关接口进行调用，目前平台支持 OpenAI 相关的大多数参数。

```python
from openai import OpenAI

client = OpenAI(api_key="这里填写你的 api key", base_url="https://api.siliconflow.cn/v1")
response = client.chat.completions.create(
    model='deepseek-ai/DeepSeek-V2.5',
    messages=[
        {'role': 'user', 
        'content': "SiliconCloud 推出分层速率方案与免费模型 RPM 提升 10 倍，对于整个大模型应用领域带来哪些改变？"}
    ],
    stream=True
)

for chunk in response:
    print(chunk.choices[0].delta.content, end='')
```


这里需要修改的只有 api_key（上面申请后复制到的）、model（名称要遵循 siliconflow 的规范）和 messages（定义了 role 和 prompt）