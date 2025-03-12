---
title: Word转markdown.md
author: 老章 mlpy
date: 2024-12-07 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---

大家好，我是章北海

我现在连写文档也要用 `Cursor` 了，`Word` 转 `Markdown` 是刚需

分享一个上周写的 `Python` 脚本，用于将 `Microsoft Word` 文档（`.docx`）转换为 `Markdown` 格式，同时保留文档中的格式和图片。


```python
from docx import Document
from PIL import Image
import os
from base64 import b64encode
from docx.shape import InlineShape

def docx_to_markdown(docx_path, output_dir):
    # 创建输出目录
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)
    
    # 创建 images 子目录
    images_dir = os.path.join(output_dir, 'images')
    if not os.path.exists(images_dir):
        os.makedirs(images_dir)
    
    # 打开 docx 文件
    doc = Document(docx_path)
    markdown_content = []
    
    # 处理每个段落
    for para in doc.paragraphs:
        # 提取文本
        text = para.text
        
        # 处理段落中的图片
        for run in para.runs:
            if run._element.drawing_lst:
                for drawing in run._element.drawing_lst:
                    # 获取图片关系 ID
                    rid = drawing.xpath('.//a:blip/@r:embed')[0]
                    image = doc.part.related_parts[rid]
                    
                    # 保存图片
                    image_filename = f'image_{len(os.listdir(images_dir))}.png'
                    image_path = os.path.join(images_dir, image_filename)
                    with open(image_path, 'wb') as f:
                        f.write(image.blob)
                    
                    # 添加 markdown 图片语法
                    text += f'\n![image](images/{image_filename})\n'
        
        # 添加到 markdown 内容
        markdown_content.append(text)
    
    # 写入 markdown 文件
    output_path = os.path.join(output_dir, 'output.md')
    with open(output_path, 'w', encoding='utf-8') as f:
        f.write('\n\n'.join(markdown_content))
    
    return output_path

# 使用示例
docx_path = '你的文档路径.docx'
output_dir = '输出目录路径'
markdown_file = docx_to_markdown(docx_path, output_dir)
```


### 脚本功能

- **文本转换**：将 `docx` 文档中的段落文本转换为 `Markdown` 格式。
- **图片处理**：提取文档中的图片并保存到 `images` 文件夹中，同时在 `Markdown` 文件中插入相应的图片引用。


在运行此脚本之前，请确保已安装以下软件：

- `Python 3.6` 或更高版本
- `pip`（`Python` 包管理器）

### 安装

1. 拷贝代码在的本地计算机。

2. 使用以下命令安装所需的 `Python` 库：

   ```bash
   pip install python-docx Pillow
   ```

### 使用方法

1. 将您要转换的 `.docx` 文件放在项目目录中。

2. 打开 `docx_to_markdown.py` 文件，并根据需要修改以下变量：

   ```python
   docx_path = '你的文档路径.docx'
   output_dir = '输出目录路径'
   ```

   - `docx_path`：要转换的 docx 文件的路径。
   - `output_dir`：生成的 Markdown 文件和图片的输出目录。

3. 在终端中运行脚本：

   ```bash
   python docx_to_markdown.py
   ```

4. 转换完成后，您将在指定的输出目录中找到 `output.md` 文件和 `images` 文件夹。`output.md` 是转换后的 `Markdown` 文件，`images` 文件夹中包含文档中的所有图片。

其实还能改成批量处理，感兴趣可以试试。
