---
title: 用 Python 把 PDF 玩的明明白白.md
author: 老章 mlpy
date: 2024-11-19 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---


大家好，我是章北海

PDF 文档解析不是什么新东西了，但是最近大模型、RAG 兴起，把这一块又带火了。

本文，梳理 7 个很常用的 pdf 处理、解析、翻译库、项目和资料。

如有帮助，欢迎点个 **【在看】**

## 1、PDFMathTranslate：文档翻译神器，公式、图表都不在话下

**项目地址：`https://github.com/Byaidu/PDFMathTranslate/**
### 简介


![](https://r2.zhanglearning.com/blog/2024/11/b494a2e95abf29e870d12ca20c4d0ce9.png)

![](https://r2.zhanglearning.com/blog/2024/11/1fc982a9e346e29cb156f1d97fbe8a66.png)

![](https://r2.zhanglearning.com/blog/2024/11/fcd1b33b72525740da4e811244b503fc.png)

### **功能**
PDF 文档翻译及双语对照
- 📊 保留公式和图表
- 📄 保留可索引目录
- 🌐 支持多种翻译服务
### **安装**

要求 Python 版本 >=3.8, <=3.12

```bash
pip install pdf2zh
```

### **使用**

命令行中执行翻译指令，在工作目录下生成翻译文档 `example-zh.pdf` 和双语对照文档 `example-dual.pdf`，默认使用 Google 作为翻译服务

```bash
# 翻译完整文档
pdf2zh example.pdf
# 翻译部分文档
pdf2zh example.pdf -p 1-3,5
# 使用指定语言翻译
pdf2zh example.pdf -li en -lo ja


# 使用 DeepL/DeepLX 翻译
# 参考 [DeepLX](https://github.com/OwO-Network/DeepLX)
# 设置环境变量构建接入点：`{DEEPL_SERVER_URL}/translate`
# - `DEEPL_SERVER_URL`（可选）, e.g., `export DEEPL_SERVER_URL=https://api.deepl.com`
# - `DEEPL_AUTH_KEY`, e.g., `export DEEPL_AUTH_KEY=xxx`
pdf2zh example.pdf -s deepl



# 使用 Ollama 翻译
# 参考 [Ollama](https://github.com/ollama/ollama)
# 设置环境变量构建接入点：`{OLLAMA_HOST}/api/chat`
# - `OLLAMA_HOST`（可选）, e.g., `export OLLAMA_HOST=https://localhost:11434`
pdf2zh example.pdf -s ollama:gemma2


# 使用 OpenAI/SiliconCloud/Zhipu 翻译
# 参考 [SiliconCloud](https://docs.siliconflow.cn/quickstart), [Zhipu](https://open.bigmodel.cn/dev/api/thirdparty-frame/openai-sdk)
# 设置环境变量构建接入点：`{OPENAI_BASE_URL}/chat/completions`
# - `OPENAI_BASE_URL`（可选）, e.g., `export OPENAI_BASE_URL=https://api.openai.com/v1`
# - `OPENAI_API_KEY`, e.g., `export OPENAI_API_KEY=xxx`
pdf2zh example.pdf -s openai:gpt-4o



# 使用正则表达式指定需要保留样式的字体和字符
pdf2zh example.pdf -f "(CM[^RT].*|MS.*|.*Ital)" -c "(\(|\||\)|\+|=|\d|[\u0080-\ufaff])"
```

## 2、pdf2htmlEX：PDF 转换为 HTML
### 简介
**项目地址：**`https://github.com/pdf2htmlEX/pdf2htmlEX`
基于 pdf2htmlEX 的分支，将 PDF 转换为 HTML，其转换效果非常好，生成的网页和原始 PDF 几乎完全一致。

原理是利用 Chrome Headless 来渲染 PDF，然后导出为 HTML 格式，甚至连图片也被转换为了 base64 编码，因此生成的网页可以完整包含文本、字体和图片等所有内容。


![](https://r2blog.zhanglearning.com/2024/11/270e6e3507ca042d28639c9dde6400dd.png)

### 功能
- 原生 HTML 文本，具有精确的字体和位置。

- 灵活的输出：一体化 HTML 或按需页面加载（需要 JavaScript）。

- 文件大小适中，有时甚至比 PDF 还小。

- 支持链接、大纲（书签）、打印、SVG 背景、Type 3 字体

### 安装
安装还是蛮麻烦的，照着文档一步一步操作吧

`https://github.com/pdf2htmlEX/pdf2htmlEX/releases`

### 使用
```
pdf2htmlEX /path/to/foobar.pdf

pdf2htmlEX --help

pdf2htmlEX --zoom 1.3 pdf/test.pdf
```


## 3、文档合并：PyMuPDF

### 简介

PyMuPDF 是一个高性能的 Python 库，用于对 PDF（及其他）文档进行数据提取、分析、转换和操作。

项目地址：`https://github.com/pymupdf/PyMuPDF`
### 功能

PyMuPDF 支持多种文档格式，如 PDF、XPS、EPUB 等，而其他软件如 pikepdf、PyPDF2、pdfrw、pdfplumber/pdfminer 支持的格式相对较少。PyMuPDF 在渲染文档页面、提取文本、提取表格、提取矢量图形、绘制矢量图形、OCR 集成等方面具有优势。

### 安装

```pip install PyMuPDF```



### 使用
```python
import pymupdf # imports the pymupdf library
doc = pymupdf.open("example.pdf") # open a document
for page in doc: # iterate the document pages
  text = page.get_text() # get plain text encoded as UTF-8
```

## 4、文档解析：Pdfminer.six
### 简介

项目地址：`https://github.com/pdfminer/pdfminer.six`

### 功能

完全用 Python 编写。
解析、分析和转换 PDF 文档。
提取内容为文本、图像、html 或 hOCR。
支持 PDF-1.7 规范。（差不多吧）。
支持中日韩语言和竖排书写脚本。
支持各种字体类型（Type1、TrueType、Type3 和 CID）。
支持提取图像（JPG、JBIG2、位图）。
支持各种压缩方式（ASCIIHexDecode、ASCII85Decode、LZWDecode、FlateDecode、RunLengthDecode、CCITTFaxDecode）。
支持 RC4 和 AES 加密。
支持 AcroForm 交互式表单提取。
目录提取。
标记内容提取。
自动布局分析。

### 安装

```pip install pdfminer.six```


### 使用

```pdf2txt.py example.pdf```

或者


```python
from pdfminer.high_level import extract_text

text = extract_text("example.pdf")
print(text)
```

## 5、文档提取：MinerU
### 简介

一站式开源高质量数据提取工具，将 PDF 转换成 Markdown 和 JSON 格式。
项目地址：`https://github.com/opendatalab/MinerU`

### 功能
![](https://r2.zhanglearning.com/blog/2024/11/1332240f5d33d612199ef3f8cf6b9c08.png)


-   删除页眉、页脚、脚注、页码等元素，确保语义连贯
-   输出符合人类阅读顺序的文本，适用于单栏、多栏及复杂排版
-   保留原文档的结构，包括标题、段落、列表等
-   提取图像、图片描述、表格、表格标题及脚注
-   自动识别并转换文档中的公式为 LaTeX 格式
-   自动识别并转换文档中的表格为 HTML 格式
-   自动检测扫描版 PDF 和乱码 PDF，并启用 OCR 功能
-   支持多种输出格式，如多模态与 NLP 的 Markdown、按阅读顺序排序的 JSON、含有丰富信息的中间格式等
-   支持多种可视化结果，包括 layout 可视化、span 可视化等，便于高效确认输出效果与质检
-   支持 CPU 和 GPU 环境
-   兼容 Windows、Linux 和 Mac 平台

### 安装
1、安装 magic-pdf
```bash
conda create -n MinerU python=3.10
conda activate MinerU
pip install -U magic-pdf[full] --extra-index-url https://wheels.myhloli.com -i https://mirrors.aliyun.com/pypi/simple
```
2. 下载模型权重文件
详细参考 https://github.com/opendatalab/MinerU/blob/master/docs/how_to_download_models_zh_cn.md

3. 修改配置文件以进行额外配置
完成 2. 下载模型权重文件步骤后，脚本会自动生成用户目录下的 magic-pdf.json 文件，并自动配置默认模型路径。您可在【用户目录】下找到 magic-pdf.json 文件。

Tip

windows 的用户目录为 "C:\Users\用户名", linux 用户目录为 "/home/用户名", macOS 用户目录为 "/Users/用户名"

您可修改该文件中的部分配置实现功能的开关，如表格识别功能：

Note

如 json 内没有如下项目，请手动添加需要的项目，并删除注释内容（标准 json 不支持注释）

{
    // other config
    "layout-config": {
        "model": "layoutlmv3" // 使用 doclayout_yolo 请修改为“doclayout_yolo"
    },
    "formula-config": {
        "mfd_model": "yolo_v8_mfd",
        "mfr_model": "unimernet_small",
        "enable": true  // 公式识别功能默认是开启的，如果需要关闭请修改此处的值为"false"
    },
    "table-config": {
        "model": "rapid_table",  // 默认使用"rapid_table",可以切换为"tablemaster"和"struct_eqtable"
        "enable": false, // 表格识别功能默认是关闭的，如果需要开启请修改此处的值为"true"
        "max_time": 400
    }
}

### 使用

```bash
magic-pdf --help
Usage: magic-pdf [OPTIONS]

Options:
  -v, --version                display the version and exit
  -p, --path PATH              local pdf filepath or directory  [required]
  -o, --output-dir PATH        output local directory  [required]
  -m, --method [ocr|txt|auto]  the method for parsing pdf. ocr: using ocr
                               technique to extract information from pdf. txt:
                               suitable for the text-based pdf only and
                               outperform ocr. auto: automatically choose the
                               best method for parsing pdf from ocr and txt.
                               without method specified, auto will be used by
                               default.
  -l, --lang TEXT              Input the languages in the pdf (if known) to
                               improve OCR accuracy.  Optional. You should
                               input "Abbreviation" with language form url: ht
                               tps://paddlepaddle.github.io/PaddleOCR/latest/en
                               /ppocr/blog/multi_languages.html#5-support-languages-
                               and-abbreviations
  -d, --debug BOOLEAN          Enables detailed debugging information during
                               the execution of the CLI commands.
  -s, --start INTEGER          The starting page for PDF parsing, beginning
                               from 0.
  -e, --end INTEGER            The ending page for PDF parsing, beginning from
                               0.
  --help                       Show this message and exit.


## show version
magic-pdf -v

## command line example
magic-pdf -p {some_pdf} -o {some_output_dir} -m auto
```
## 6、布局解析：DocLayout-YOLO
### 简介

基于 YOLO-v10，通过提供多样性文档预训练及适配文档检测的模型结构优化，可针对多样性文档进行实时鲁棒的检测。

项目地址：`https://github.com/opendatalab/DocLayout-YOLO`

![](https://github.com/opendatalab/DocLayout-YOLO/raw/main/assets/showcase.png)


### 功能


### 安装

```bash
conda create -n doclayout_yolo python=3.10
conda activate doclayout_yolo
pip install -e .
```
注意：如果只想使用 DocLayout-YOLO 的推理功能，直接通过 pip 进行安装：

```bash
pip install doclayout-yolo
```

### 使用

可以通过脚本的方式或者 SDK 的方式进行推理：

脚本推理

通过以下命令运行推理脚本 demo.py 来进行推理：

```python
python demo.py --model path/to/model --image-path path/to/image
```
SDK 推理

直接通过 SDK 进行模型推理：

```python
import cv2
from doclayout_yolo import YOLOv10

# Load the pre-trained model
model = YOLOv10("path/to/provided/model")

# Perform prediction
det_res = model.predict(
    "path/to/image",   # Image to predict
    imgsz=1024,        # Prediction image size
    conf=0.2,          # Confidence threshold
    device="cuda:0"    # Device to use (e.g., 'cuda:0' or 'cpu')
)

# Annotate and save the result
annotated_frame = det_res[0].plot(pil=True, line_width=5, font_size=20)
cv2.imwrite("result.jpg", annotated_frame)
```



## 7、pdf 文档标准：PDF Explained、PDF Cheat Sheets
### 简介

最后再推荐俩资料，非常适合入门 PDF 及加深对其的理解

![](https://zxyle.github.io/PDF-Explained/images/logo.png)

这是对广泛使用的可移植文档格式的平易近人的介绍。PDF 无处不在，无论是在线形式还是印刷形式，但很少有人利用这些有用的功能或掌握这种格式的细微差别。这本简明的书籍为程序员，高级用户提供了世界领先的页面描述语言 (pdf) 的动手实践。以及搜索，电子出版和印刷行业的专业人士，有大量示例，本书是你完全理解 PDF 所需的文档。

项目地址：`https://zxyle.github.io/PDF-Explained`


pdf 知识卡片速查表

![](https://pdfa.org/wp-content/uploads/2024/10/CS2-Basics.png)

项目地址：`https://pdfa.org/resource/pdf-cheat-sheets/`
