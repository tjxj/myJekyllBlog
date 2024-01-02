---
title: Python处理word文档，相关的库
author: 老章mlpy
date: 2024-01-01 14:10:00 +0800
categories: [Python系列]
tags: [Python]
render_with_liquid: false
---

当然，Python社区提供了多个库来处理Word文档，主要用于创建、修改和读取Word文件。以下是一些常用的库：

1. `python-docx`：用于创建和修改.docx文件。
2. `docx2txt`：将.docx文件转换成纯文本。
3. `pywin32` (仅限Windows)：通过Microsoft Word应用程序接口与Word文档交互。

### python-docx

`python-docx` 是一个创建和更新Microsoft Word (.docx)文件的Python库。这里有一个简单的例子，展示如何使用 `python-docx` 创建一个包含一段文本的Word文档：

```python
from docx import Document

# 创建一个Word文档对象
doc = Document()

# 向文档添加一个段落
doc.add_paragraph('Hello, this is a paragraph in a Word document!')

# 保存文档
doc.save('hello_world.docx')
```

### docx2txt

`docx2txt` 是一个轻量级的库，用于将.docx文档转换为纯文本。下面是一个例子：

```python
import docx2txt

# 将.docx文件的内容转换为纯文本
text = docx2txt.process("example.docx")

# 输出文档的纯文本
print(text)
```

### pywin32

`pywin32` 提供了与Windows应用程序的接口，包括Microsoft Word。这个库允许你通过COM自动化来操作Word。请注意，这只在Windows系统上有效。以下是使用 `pywin32` 打开一个Word文档的例子：

```python
import win32com.client as win32

# 启动Word应用程序
word = win32.gencache.EnsureDispatch('Word.Application')
word.Visible = False

# 打开一个现有的文档
doc = word.Documents.Open('path_to_your_document.docx')

# 添加一个新段落
doc.Paragraphs.Add()
doc.Paragraphs.Last.Range.Text = 'This is a new paragraph added by python.'

# 保存并关闭
doc.SaveAs('new_document.docx')
doc.Close()

# 退出Word
word.Quit()
```

这些库都可以通过Python的包管理工具pip进行安装。例如，要安装`python-docx`，你可以使用以下命令：

```sh
pip install python-docx
```

请注意，运行这些示例代码之前，你需要确保安装了相应的库。

![](https://my-wechat.oss-cn-beijing.aliyuncs.com/WX20230912-203916-20231217213830903-20231222231724242.png)
