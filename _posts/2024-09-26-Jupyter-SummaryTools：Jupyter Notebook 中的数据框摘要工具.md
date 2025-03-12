---
title: Jupyter-SummaryTools：Jupyter Notebook 中的数据框摘要工具.md
author: 老章 mlpy
date: 2024-09-26 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---



在数据科学领域，能够快速、准确地了解数据集的特性至关重要。

对使用 Jupyter Notebook 进行数据分析的用户而言，jupyter-summarytools 是一个强大且便捷的工具。

本文将详细介绍 jupyter-summarytools 的功能、安装方法及使用示例，帮助你在数据分析过程中事半功倍。
![](https://r2.zhanglearning.com/blog/2024/09/f9fa55479e51360824deecce4b27f4b9.png)

## 什么是 Jupyter Summary Tools？

jupyter-summarytools 是一个 Python 包，旨在为 Jupyter Notebook 用户提供类似于 R 语言中 summarytools 包的功能。它通过生成标准化且全面的数据框（DataFrame）摘要，帮助用户快速了解数据集的结构和主要特征。当前，jupyter-summarytools 主要提供了 dfSummary 函数，用于生成 HTML 格式的数据摘要，并支持多种展示方式，如可折叠摘要和标签页摘要。

## 主要特性

- 标准化摘要：快速生成包含数据类型、缺失值、描述性统计等信息的综合摘要。

- 可折叠摘要：通过折叠功能，用户可以选择性查看详细信息，避免信息过载。

- 标签页摘要：将不同数据集的摘要以标签页形式展示，便于在同一页面查看多个数据集。
-
## 安装

在使用 `jupyter-summarytools` 之前，确保已安装该库。可以通过以下命令使用 `pip` 进行安装：

```bash
pip install summarytools
```

## 依赖

`jupyter-summarytools` 依赖于以下环境和库：

1. **Python**：版本 3.6 及以上。
2. **Pandas**：版本 1.4.0 及以上。

确保您的环境符合上述要求，以避免安装或运行时出现问题。

## 快速开始

以下是 `jupyter-summarytools` 的快速入门指南，帮助您快速在 Jupyter Notebook 中生成数据框的摘要。

### 基本用法

首先，导入必要的库并加载数据集：

```python
import pandas as pd
from summarytools import dfSummary

# 加载数据集
titanic = pd.read_csv('./data/titanic.csv')

# 生成数据框摘要
dfSummary(titanic)
```

![](https://r2.zhanglearning.com/blog/2024/09/f6b143946ecdcf3c62643d0ec9f4ff93.png)


### 可折叠摘要

为了更好地展示数据摘要，可以使用可折叠摘要功能：

```python
import pandas as pd
from summarytools import dfSummary

titanic = pd.read_csv('./data/titanic.csv')

# 生成可折叠的数据框摘要
dfSummary(titanic, is_collapsible=True)
```


![](https://r2.zhanglearning.com/blog/2024/09/4c04e410e94674e04c6055d9686dbe5e.png)

### 标签式摘要

`jupyter-summarytools` 还支持标签式摘要，允许在不同标签页中查看多个数据框的摘要：

```python
import pandas as pd
from summarytools import dfSummary, tabset

# 加载多个数据集
titanic = pd.read_csv('./data/titanic.csv')
vaccine = pd.read_csv('./data/country_vaccinations.csv')
vaccine['date'] = pd.to_datetime(vaccine['date'])

# 生成标签式摘要
tabset({
    'titanic': dfSummary(titanic).render(),
    'vaccine': dfSummary(vaccine).render()
})
```

![](https://github.com/6chaoran/jupyter-summarytools/blob/master/images/tabbed.gif)
## 导出 Notebook 为 HTML

在将 Jupyter Notebook 导出为 HTML 时，确保已安装并启用了 `Export Embedded HTML` 扩展。使用以下命令可以保留数据框摘要在导出的 HTML 中：

```bash
jupyter nbconvert --to html_embed path/of/your/notebook.ipynb
```
![](https://r2.zhanglearning.com/blog/2024/09/b997355ce8d440ff6b99a1bf09b8b596.png)
