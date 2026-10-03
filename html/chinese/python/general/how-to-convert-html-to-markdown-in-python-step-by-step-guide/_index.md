---
category: general
date: 2026-10-02
description: 在 Python 中将 HTML 转换为 Markdown，提供完整示例。了解如何将 HTML 保存为 Markdown，选择格式化器，并启用特定功能。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- save html as markdown
- how to convert html
- html to markdown conversion
- html to markdown python
language: zh
lastmod: 2026-10-02
og_description: 使用实用代码、格式化选项和功能标志，在 Python 中将 HTML 转换为 Markdown。按照本指南快速将 HTML 保存为
  Markdown。
og_image_alt: Screenshot of Python code converting HTML to Markdown
og_title: 在 Python 中将 HTML 转换为 Markdown – 完整教程
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: convert HTML to Markdown in Python with a complete example. Learn how
    to save HTML as Markdown, choose formatters, and enable specific features.
  headline: How to convert HTML to Markdown in Python – step‑by‑step guide
  type: TechArticle
- description: convert HTML to Markdown in Python with a complete example. Learn how
    to save HTML as Markdown, choose formatters, and enable specific features.
  name: How to convert HTML to Markdown in Python – step‑by‑step guide
  steps:
  - name: Enabling only the needed features
    text: You can fine‑tune the output by turning on specific feature flags. In this
      example we keep **links** and **paragraphs** while disabling images, tables,
      and other constructs.
  - name: Expected output (`output.md`)
    text: '```markdown # Project Overview'
  - name: Missing or malformed `href` attributes
    text: 'If an `<a>` tag lacks a valid `href`, the converter inserts the link text
      without a URL. To preserve readability, you may want to post‑process the Markdown:'
  - name: Converting large HTML files
    text: 'For multi‑megabyte HTML files, stream the input to avoid loading the entire
      markup into memory:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
title: 如何在 Python 中将 HTML 转换为 Markdown——一步步指南
url: /zh/python/general/how-to-convert-html-to-markdown-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中将 HTML 转换为 Markdown – 步骤指南

如果您需要 **将 HTML 转换为 Markdown**，本指南将为您展示一个完整、可运行的 Python 解决方案。您将了解如何 **将 HTML 保存为 Markdown**、选择合适的格式化器，以及仅启用您关心的功能。

将 HTML 转换为 Markdown 是在需要轻量文档、静态站点内容或受版本控制的文本文件时的常见任务。本教程涵盖从安装库到处理边缘情况的全部内容，帮助您将此技术应用于任何 HTML 源。

## 前置条件

在开始之前，请确保您具备：

* 已安装 Python 3.8 或更高版本。
* 可使用 `pip` 安装第三方包。
* 对 HTML 标签和 Markdown 语法有基本了解。

由于转换库是纯 Python 实现，无需额外的系统依赖。

## 安装 GroupDocs Conversion 库

代码示例使用 **GroupDocs.Conversion** Python 包，提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter`。使用以下命令进行安装：

```bash
pip install groupdocs-conversion
```

> **专业提示：** 使用虚拟环境（`python -m venv venv`）可以将该包与其他项目隔离。

## 第一步：从字符串创建 `HTMLDocument`

第一步是将原始 HTML 包装到 `HTMLDocument` 实例中。该对象抽象了源，无论是来自字符串、文件还是远程 URL。

```python
from groupdocs.conversion import HTMLDocument

# Example HTML – you can replace this with any valid markup
html_content = "<h1>Title</h1><p>Hello <a href='https://example.com'>world</a></p>"
html_doc = HTMLDocument(html_content)
```

*原因说明：* `HTMLDocument` 只会解析一次标记，使转换器能够使用规范化的表示，而不是原始文本。

## 第二步：配置 `MarkdownSaveOptions`

`MarkdownSaveOptions` 让您控制输出格式以及生成哪些 Markdown 特性。库支持两种格式化器：

* **DEFAULT** – 标准的 CommonMark 兼容 Markdown。
* **GIT** – Git 风格的 Markdown（支持表格、删除线等）。

在大多数版本控制场景下，推荐使用 **GIT** 格式化器。

```python
from groupdocs.conversion import MarkdownSaveOptions

md_opts = MarkdownSaveOptions()
md_opts.formatter = MarkdownSaveOptions.Formatter.GIT
```

### 仅启用所需特性

您可以通过打开特定的特性标志来微调输出。在本例中，我们保留 **links**（链接）和 **paragraphs**（段落），同时禁用 images（图片）、tables（表格）以及其他结构。

```python
md_opts.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

*原因说明：* 限制特性可以减小生成文件的体积，并防止下游工具不支持的意外 Markdown 元素。

## 第三步：转换文档

有了源 `HTMLDocument` 与配置好的 `MarkdownSaveOptions`，只需一次调用 `Converter.convert` 即可完成转换。为输出文件提供绝对或相对路径。

```python
from groupdocs.conversion import Converter

output_path = "output.md"
Converter.convert(html_doc, output_path, md_opts)
```

调用结束后，`output.md` 将包含原始 HTML 的 Markdown 表示。

## 可直接运行的完整脚本

下面是整合了上述所有步骤的完整、独立脚本。将其保存为 `html_to_md.py` 并运行 `python html_to_md.py`。

```python
# html_to_md.py
# Complete example that converts HTML to Markdown using GroupDocs.Conversion

from groupdocs.conversion import Converter, HTMLDocument, MarkdownSaveOptions

# 1️⃣  Create the HTMLDocument – replace the string with your own HTML source
html_content = """
<h1>Project Overview</h1>
<p>Welcome to the <a href="https://github.com/example">example repo</a>.</p>
<ul>
  <li>Feature A</li>
  <li>Feature B</li>
</ul>
"""
html_doc = HTMLDocument(html_content)

# 2️⃣  Prepare Markdown save options
md_opts = MarkdownSaveOptions()
md_opts.formatter = MarkdownSaveOptions.Formatter.GIT  # Git‑flavored Markdown
md_opts.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH |
    MarkdownSaveOptions.Features.LIST      # include lists for this example
)

# 3️⃣  Perform the conversion
output_path = "output.md"
Converter.convert(html_doc, output_path, md_opts)

print(f"Conversion complete – Markdown saved to {output_path}")
```

### 预期输出 (`output.md`)

```markdown
# Project Overview

Welcome to the [example repo](https://github.com/example).

- Feature A
- Feature B
```

输出保持了原始 HTML 的结构，仅保留我们启用的特性（链接、段落和列表）。

## 处理常见边缘情况

### 缺失或格式错误的 `href` 属性

如果 `<a>` 标签缺少有效的 `href`，转换器会仅插入链接文本而不带 URL。为保持可读性，您可能需要对生成的 Markdown 进行后处理：

```python
import re

def fix_broken_links(md_text):
    # Replace stray brackets like [text]() with just the text
    return re.sub(r'\[([^\]]+)\]\(\)', r'\1', md_text)

with open(output_path, "r+", encoding="utf-8") as f:
    content = f.read()
    f.seek(0)
    f.write(fix_broken_links(content))
    f.truncate()
```

### 转换大型 HTML 文件

对于多兆字节的 HTML 文件，建议流式读取输入，以避免一次性将全部标记加载到内存中：

```python
with open("large_input.html", "r", encoding="utf-8") as src:
    html_doc = HTMLDocument(src.read())
```

转换过程本身保持不变，因为 `HTMLDocument` 已抽象了源的大小。

## 替代格式化器

如果您更倾向于纯 CommonMark 而非 Git 风格的输出，只需切换格式化器：

```python
md_opts.formatter = MarkdownSaveOptions.Formatter.DEFAULT
```

这样会生成更简洁的 Markdown 文件，适用于不支持 Git 扩展的平台。

## 您可能想要探索的相关任务

* **将 Markdown 转回 HTML** – 便于预览文档。
* **将 HTML 导出为 PDF** – 另一个常见的 **html to markdown conversion** 相关工作流。
* **批量处理文件夹中的 HTML 文件** – 循环遍历文件并复用相同的 `MarkdownSaveOptions` 实例。

所有这些都遵循相同的模式：创建源文档、配置保存选项，然后调用 `Converter.convert`。

## 结论

现在，您已经掌握了在 Python 中 **将 HTML 转换为 Markdown** 的方法，了解了如何 **将 HTML 保存为 Markdown** 并精确控制特性，以及为何为下游工具选择合适的格式化器至关重要。示例展示了一种简洁、可复用的做法，适用于单个字符串、文件或 URL，并提供了处理缺失链接和大文件输入的技巧。

欢迎尝试更多 `MarkdownSaveOptions.Features`（如 `IMAGE`、`TABLE`），以根据项目需求定制输出。如果本指南对您有帮助，请与团队分享或在项目文档中链接。祝转换愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}