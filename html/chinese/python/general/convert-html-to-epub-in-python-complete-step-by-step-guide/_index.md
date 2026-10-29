---
category: general
date: 2026-07-18
description: 在 Python 中快速将 HTML 转换为 EPUB。学习如何在 Python 中加载 HTML 文件，并使用简易库将 HTML 转换为
  MHTML。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: zh
lastmod: 2026-07-18
og_description: 使用 Python 将 HTML 转换为 EPUB，提供清晰可运行的示例。同时学习如何在 Python 中加载 HTML 文件，并在几分钟内将
  HTML 转换为 MHTML。
og_image_alt: Diagram showing convert html to epub workflow
og_title: 在 Python 中将 HTML 转换为 EPUB – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: 在 Python 中将 HTML 转换为 EPUB – 完整的逐步指南
url: /zh/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为 EPUB（Python 完整分步指南）

有没有想过在不抓狂的情况下 **将 HTML 转换为 EPUB**？你并不是唯一的——开发者经常需要把网页转换成离线阅读的电子书，而在 Python 中实现这一点出奇地简单。本教程将带你一步步完成：在 Python 中加载 HTML 文件、将 HTML 转换为 EPUB，甚至将同一源文件转换为 MHTML，以便通过电子邮件归档。

阅读完本指南后，你将拥有一个可直接运行的脚本，只需提供一个 `sample.html` 文件，即可生成 `sample.epub` 和 `sample.mhtml`。没有神秘，只是清晰的代码和解释。

---

![转换流程图](https://example.com/images/convert-html-epub.png "展示 HTML 转 EPUB 工作流的图示")

## 你将构建的内容

- **使用内置的 `pathlib` 和 `io` 模块在 Python 中加载 HTML 文件**。  
- **使用 `ebooklib` 库将 HTML 转换为 EPUB**，该库会为你处理 EPUB 容器格式。  
- **使用 `email` 包将 HTML 转换为 MHTML**（亦称 MHT），生成浏览器可直接打开的单文件网页归档。  

我们还会涉及：

- 必要的依赖以及如何安装它们。  
- 错误处理，使脚本能够优雅地失败。  
- 如何自定义 EPUB 文件的元数据，如标题和作者。  

准备好了吗？让我们开始吧。

---

## 前置条件

在开始编码之前，请确保你已经具备：

1. **Python 3.9+** —— 本教程使用的语法在任何近期版本均可运行。  
2. **pip** —— 用于安装第三方包。  
3. 一个简单的 HTML 文件，例如 `sample.html`，放在你可控制的文件夹中。  

如果这些都已经就绪，太好了——直接跳到下一节。

> **小技巧：** 保持你的 HTML 结构良好（正确的 `<head>` 和 `<body>` 部分）。虽然 `ebooklib` 会尝试修复轻微问题，但干净的源文件能为你省去后续的麻烦。

---

## 第一步 – 安装所需库

我们需要两个外部包：

- **ebooklib** – 用于生成 EPUB。  
- **beautifulsoup4** – 可选，但在转换前清理 HTML 时非常有用。

在终端中运行：

```bash
pip install ebooklib beautifulsoup4
```

> **为什么选择这些库？** `ebooklib` 为你构建基于 ZIP 的 EPUB 结构，自动处理 `META‑INF` 文件夹、`content.opf` 和 `toc.ncx`。`beautifulsoup4` 让我们能够整理 HTML，确保最终的电子书在所有阅读器上都能正确渲染。

---

## 第二步 – 在 Python 中加载 HTML 文件

加载 HTML 文件非常直接，但我们会把它封装在一个小助手函数中，返回一个 **BeautifulSoup** 对象，以便后续处理。

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**解释：**  
- `Path` 提供跨平台的文件操作。  
- 使用 `read_text` 可以省去手动 `open`/`close` 的样板代码。  
- 返回 `BeautifulSoup` 对象后，我们可以在 **将 HTML 转换为 EPUB** 之前去除脚本、修复标签或注入样式表。

---

## 第三步 – 将 HTML 转换为 EPUB

既然我们已经能够 **在 Python 中加载 HTML 文件**，接下来把它转换为干净的 EPUB。下面的函数接受一个 `BeautifulSoup` 对象、目标路径以及可选的元数据。

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**工作原理：**  
- `ebooklib.epub.EpubBook` 抽象了 ZIP 容器及必需的清单文件。  
- 我们生成一个 UUID 作为标识符，避免在创建大量书籍时出现重复 ID。  
- `spine` 指定章节顺序；对于大多数简单的 HTML 源，仅需单章节即可。  

**运行转换：**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

执行脚本后，你会看到一个绿色对勾，确认 EPUB 文件已生成并显示其位置。

---

## 第四步 – 将 HTML 转换为 MHTML

MHTML（或 MHT）将 HTML 及其所有资源（图片、CSS）打包成单个 MIME 文件。Python 的 `email` 包可以在不依赖外部库的情况下构建此格式。

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**关键要点：**  

- `multipart/related` MIME 类型告诉浏览器，HTML 部分与其资源是关联在一起的。  
- 我们遍历 `<img>` 标签以嵌入图片；如果不需要图片，可跳过该块。  
- `Content-Location` 使用 `file://` URI，使浏览器能够在内部解析资源。  

**调用函数：**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

现在，你已经拥有 `sample.epub` 与 `sample.mhtml` 并排存放。

---

## 完整脚本 – 一文件实现全部步骤

下面是完整、可直接运行的脚本，整合了上述所有内容。将其保存为 `convert_html.py`，并将 `YOUR_DIRECTORY` 替换为存放 `sample.html` 的路径。

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
convert_html.py

A tiny utility that demonstrates:
- How to load an HTML file in Python
- How to convert HTML to EPUB (convert html to epub)
- How to convert HTML to MHTML (convert html to mhtml)

Author: Your Name
Date: 2026‑07‑18
"""

from pathlib import Path
import uuid
import mimetypes


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [How to Convert EPUB to Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}