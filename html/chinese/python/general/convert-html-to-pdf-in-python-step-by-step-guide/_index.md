---
category: general
date: 2026-08-06
description: 在 Python 中将 HTML 转换为 PDF，并提供完整示例。学习如何从 HTML 生成 PDF、将 HTML 保存为 PDF，并处理常见的边缘情况。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: zh
lastmod: 2026-08-06
og_description: 在 Python 中将 HTML 转换为 PDF 并实现文档自动化。按照本指南从 HTML 生成 PDF、将 HTML 保存为 PDF，并自定义输出。
og_image_alt: Example of convert html to pdf script in Python
og_title: 在 Python 中将 HTML 转换为 PDF – 综合教程
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: 在 Python 中将 HTML 转换为 PDF – 步骤指南
url: /zh/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为 PDF（Python） – 步骤指南

如果您需要**快速将 HTML 转换为 PDF**，本教程展示了在 Python 中的完整解决方案。您将看到如何从 HTML 生成 PDF、将 HTML 保存为 PDF，以及在不离开代码的情况下控制转换过程。

本指南将带您完成安装可靠库、加载 HTML 文档、执行转换以及验证结果的全过程。完成后，您即可在任何 Python 项目中从 HTML 文件创建 PDF，无论来源是静态页面还是动态生成的标记。

## 您将学到

* 安装 `pdfkit` 和 `wkhtmltopdf` 这两个进行 HTML‑to‑PDF 转换所需的依赖。  
* 从磁盘或字符串加载 HTML 文档。  
* 使用自定义页面大小、边距和编码选项从 HTML 生成 PDF。  
* 通过单个函数调用将 HTML 保存为 PDF。  
* 处理常见的边缘情况，如缺失资源、Unicode 字符以及大文件。  

**先决条件** – Python 3.8+，并具备基本的文件 I/O 知识。无需外部服务。

## 将 HTML 转换为 PDF – 整体工作流

转换过程由三个逻辑阶段组成：

1. **准备阶段** – 安装转换器并确保 `wkhtmltopdf` 可执行文件可被访问。  
2. **输入处理** – 读取 HTML 文件或以编程方式构建标记。  
3. **输出生成** – 调用转换器，写入 PDF 文件，并确认结果。

下面的每一步都针对相应阶段进行详细说明。

## 第 1 步：安装所需库

`pdfkit` 为广泛使用的 `wkhtmltopdf` 引擎提供了轻量的 Python 包装器。使用 `pip` 安装两者并验证二进制路径。

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

如果您更倾向于使用便携式二进制文件，请从 [wkhtmltopdf GitHub 页面](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) 下载相应的发行版，并将其放置在已加入 `PATH` 的目录中。脚本稍后会自动检查该路径。

## 第 2 步：加载 HTML 文档

您可以读取静态文件、获取远程内容，或在运行时构造 HTML。下面的示例加载位于您指定目录下的本地文件 `sample.html`。

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

将文件读取为 Unicode 字符串可确保诸如 “é”、 “ß” 或亚洲字符等在转换过程中得以保留。当您**从包含国际文本的 HTML 生成 PDF**时，此步骤尤为关键。

## 第 3 步：从 HTML 生成 PDF

`pdfkit.from_string` 将包含 HTML 标记的字符串转换为 PDF 文件。您可以传入一个选项字典，以控制页面大小、边距以及页眉/页脚行为。

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

上述调用**从 HTML 文件创建 PDF**并保存为 `sample.pdf`。如果源 HTML 引用了本地 CSS 或图片，`enable‑local‑file‑access` 标志会让 `wkhtmltopdf` 解析这些资源。

### 为什么这种方式有效

* `pdfkit` 将繁重的渲染工作交给 `wkhtmltopdf`，后者使用 WebKit 引擎渲染 HTML，能够高度还原原始布局。  
* 通过选项字典可以在不修改 HTML 本身的前提下微调输出。  
* 使用 `from_string` 能够在内存中完成工作流，这在 HTML 动态生成时非常有用。

## 第 4 步：将 HTML 保存为 PDF 并验证输出

转换完成后，您可能需要确认 PDF 已生成且可读取。下面的代码片段检查文件大小并使用系统默认的 PDF 查看器打开文件（平台特定）。

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

运行脚本后会打印成功信息并启动 PDF 查看器，您可以立即确认布局是否与原始 HTML 相匹配。此步骤完成了**将 HTML 保存为 PDF**的整个循环。

## 第 5 步：高级选项 – 使用自定义设置从 HTML 文件创建 PDF

有时您手头已有磁盘上的 HTML 文件，想直接使用 `pdfkit.from_file` 而不是自行读取内容。该方法在 HTML 已包含复杂相对路径时尤为方便。

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

您还可以通过扩展 `options` 字典来嵌入封面页、目录或 JavaScript 执行标志。例如，添加封面页的方式如下：

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

这些微调展示了**如何将 HTML 转换为 PDF**以满足更复杂的出版流水线需求。

## 常见陷阱及规避方法

| 问题 | 原因 | 解决方案 |
|-------|-------|--------|
| 图片或 CSS 未显示 | `wkhtmltopdf` 默认阻止本地文件访问 | 在选项字典中添加 `"enable-local-file-access": None` |
| Unicode 字符乱码 | 缺少 `encoding` 选项或以错误的字符集读取文件 | 始终设置 `"encoding": "UTF-8"` 并使用 UTF‑8 读取 HTML 文件 |
| PDF 空白 | `wkhtmltopdf` 二进制路径不正确 | 显式提供路径：`pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| 大型 HTML 文件超时 | 默认超时时间过短 | 设置 `"javascript-delay": "2000"` 或使用 `"timeout": "60"` 增加超时 |

解决这些问题可确保在不同环境下可靠地**从 HTML 生成 PDF**。

## 完整脚本 – 端到端示例

将以下内容保存为 `html_to_pdf.py` 并使用 `python html_to_pdf.py` 运行。将 `YOUR_DIRECTORY` 替换为指向您项目文件夹的路径。

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在已有技巧的基础上进一步掌握 API 功能并探索替代实现方案。

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}