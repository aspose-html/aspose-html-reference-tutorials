---
category: general
date: 2026-05-31
description: 学习如何使用 Python 从 HTML 中提取 SVG。本分步教程展示了如何读取 HTML 文档、保存 SVG 文件以及高效保存内联 SVG。
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: zh
og_description: 如何使用 Python 从 HTML 中提取 SVG。通过本教程读取 HTML 文档，保存 SVG 文件，并轻松处理内联 SVG。
og_title: 使用 Python 从 HTML 中提取 SVG – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: 使用 Python 从 HTML 中提取 SVG 的完整指南
url: /zh/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 从 HTML 中提取 SVG – 完整指南

是否曾经想过 **如何从杂乱的 HTML 页面中提取 SVG** 而不抓狂？你并不孤单。无论你是在构建网页爬虫、设计流水线，还是仅仅需要批量导出图标，掌握 **如何提取 SVG** 都是一个省时省力的实用技巧。

在本教程中，我们将展示如何使用 Aspose.HTML for Python **提取 SVG**。我们会读取 HTML 文档，提取内联 `<svg>` 标记 **以及** 外部 SVG 引用，然后 **将 SVG 文件** 保存到磁盘——整个过程整洁且可复用。完成后，你将拥有一个可直接运行的解决方案，能够根据自己的项目进行适配。

> **小技巧：** 如果你只想快速嗅探页面，`BeautifulSoup` 也能工作，但 Aspose.HTML 提供完整的 DOM，使得提取内联和链接的 SVG 都轻而易举。

## 你需要准备的环境

在开始之前，请确保你拥有：

* Python 3.8+（代码使用 f‑string，最低要求 3.6+）
* `pip install aspose-html` – 为我们的 HTML 解析提供商业库
* 一个包含 `input.html` 文件的文件夹，文件中有你想提取的 SVG
* 对输出目录的写入权限（我们将其称为 `YOUR_DIRECTORY`）

就这些——无需额外的二进制文件，也不需要无头浏览器。很简单，对吧？

## 第一步：使用 Aspose.HTML 读取 HTML 文档

首先要 **读取 HTML 文档**，这样才能遍历其 DOM 树。Aspose.HTML 为你提供一个 `HTMLDocument` 对象，行为类似浏览器的 `document`。

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*为什么这很重要：* 将 HTML 加载到正式的 DOM 中，可以避免正则解析的陷阱，并且可以直接使用 `get_elements_by_tag_name`、`query_selector_all` 等方法。

## 第二步：收集所有内联 <svg> 元素

内联 SVG 是指直接写在 HTML 中的 `<svg>…</svg>` 块。要 **保存内联 SVG**，我们只需获取它们的 outer HTML。

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

请注意，我们直接将原始标记追加到 `svg_contents` 中。稍后我们会判断每个条目是标记还是文件路径。

## 第三步：查找外部 SVG 引用（img 与 object 标签）

许多页面通过 `<img src="icon.svg">` 或 `<object data="logo.svg">` 链接外部 SVG 文件。要 **从 HTML 中提取 SVG**，也需要捕获这些 URL。

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*边缘情况提示：* 如果 SVG URL 是相对路径，需要将其与 HTML 文件的基路径拼接。为简洁起见，这里假设 HTML 与 SVG 文件位于同一目录。

## 第四步：将每个 SVG 写入单独的文件

现在我们拥有一个混合了标记字符串和文件路径的列表，接下来遍历并 **保存 SVG 文件**。脚本会自动区分内联标记和已有文件的引用。

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**运行结果示例：** 脚本执行完毕后，`YOUR_DIRECTORY` 中会出现 `svg_0.svg`、`svg_1.svg`、… 等文件，每个文件保存的要么是原始的内联标记，要么是外部 SVG 的副本。

### 预期输出

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

如果某个引用的文件缺失，脚本会打印警告但继续执行——这样单个失效链接不会导致整个提取过程中断。

## 常见问题处理

| 问题 | 产生原因 | 快速解决方案 |
|------|----------|--------------|
| **相对 URL 失效** | `src` 属性可能是 `"../assets/icon.svg"` | 使用 `os.path.join(os.path.dirname(html_path), src)` 进行解析。 |
| **文件名冲突** | 两个 SVG 同名会被覆盖 | 在文件名中加入内容哈希，例如 `hashlib.md5(content.encode()).hexdigest()[:8]`。 |
| **大型内联 SVG 导致内存激增** | 在写入前将所有标记存入列表 | 直接将每个元素流式写入文件，避免缓冲。 |
| **非 SVG 图片误入** | 某些 `<img>` 标签以 `.svg?version=1` 结尾 | 在检查扩展名之前去除查询字符串 (`src.split('?')[0]`)。 |

## 完整脚本，复制即用

下面是完整、可直接运行的程序。将其保存为 `extract_svg.py`，修改 `YOUR_DIRECTORY`，然后运行 `python extract_svg.py`。

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## 回顾 – 提取 SVG 的要点概览

* 使用 `HTMLDocument` **读取 HTML 文档**。
* 通过 `get_elements_by_tag_name` **收集内联 `<svg>`**。
* 使用以 `.svg` 结尾的 CSS 选择器 **定位外部 SVG**。
* **保存每一块**——将标记直接写入文件或复制引用的文件。
* 处理相对路径、文件名冲突和缺失文件等 **边缘情况**。

这就是 **如何从 HTML 页面提取 SVG** 的完整答案，全部封装在一个易于修改的脚本中。

## 接下来可以做什么？

既然已经能够 **可靠地提取 SVG**，可以考虑以下后续思路：

* **批量处理：** 遍历一个 HTML 文件目录，构建图标库。
* **优化压缩：** 对每个保存的 SVG 运行 SVGO（Node.js 优化工具）以减小体积。
* **格式转换：** 使用 `cairosvg` 或 `svglib` 将 SVG 转为 PNG，兼容旧版浏览器。
* **元数据提取：** 解析每个 SVG 内的 `<title>` 或 `<desc>` 标签，生成可搜索的标签。

上述每个主题都涉及我们的二级关键词——**read HTML document**、**save svg files**、**save inline svg**、**extract svg from html**——你可以据此展开更多学习。

---

*祝编码愉快！如果遇到任何问题，欢迎在下方留言或在 GitHub 上私信我。SVG 的世界广阔无垠，但有了合适的工具，提取它们就是小菜一碟。*

## 接下来该学习什么？

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendre un document SVG au format PNG dans .NET avec Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}