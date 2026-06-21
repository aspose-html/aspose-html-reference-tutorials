---
category: general
date: 2026-05-31
description: 学习如何使用 Python 下载图标。我们还将在同一个教程中介绍如何提取 favicon、使用 Python 读取 HTML 文档以及写入二进制文件。
draft: false
keywords:
- how to download icons
- how to extract favicon
- write binary file python
- read html document python
- load html python
language: zh
og_description: 如何使用 Python 下载图标，逐步讲解。学习提取 favicon、读取 HTML 文档以及用 Python 写入二进制文件。
og_title: 如何使用 Python 下载图标 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to download icons using Python. We'll also cover how to extract
    favicon, read HTML document Python, and write binary file python in a single tutorial.
  headline: How to Download Icons with Python – Complete Guide
  type: TechArticle
tags:
- python
- web-scraping
- favicon
- file-io
title: 如何使用 Python 下载图标——完整指南
url: /zh/python/general/how-to-download-icons-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 下载图标 – 完整指南

有没有想过 **如何下载图标** 而不必手动右键点击每一个？你并不是唯一有此需求的人。无论是构建品牌审计工具，还是仅仅想要本地保存遇到的每个 favicon，掌握这项任务都能为你节省时间和敲击键盘的次数。

在本教程中，我们将演示如何使用原生 Python 从 HTML 文件 **下载图标**。我们还会展示 **如何提取 favicon**，演示 **read html document python**，并解释 **write binary file python**，让你最终得到一个整洁的 .ico 文件夹，可用于任何项目。

---

## 你需要的条件

- Python 3.8+（标准库已足够）
- 你想要扫描的 HTML 页面本地副本（或可获取的 URL）
- 对 Python 中文件 I/O 的基本了解  
- 不需要外部包，但如果你愿意，`beautifulsoup4` 可以让过程更顺畅（可选）

准备好了吗？太好了——让我们开始吧。

![How to download icons example](https://example.com/placeholder.png "how to download icons example")

---

## 步骤 1：在 Python 中加载 HTML 文档  

首先，我们需要以 **load html python** 的方式读取文件——将文件读取到内存中，以便检查其中的 `<link>` 标签。最简单的方法是使用内置的 `open` 函数打开文件并以文本方式读取。

```python
# Step 1: Load the HTML document
HTML_PATH = "YOUR_DIRECTORY/sample.html"

# Using the built‑in open() to read the file as a string
with open(HTML_PATH, "r", encoding="utf-8") as f:
    html_content = f.read()
```

*为什么需要这一步？*  
读取 HTML 为我们提供了一个原始字符串，供后续解析使用。如果跳过这一步直接使用路径，解析器将没有内容可检查。

---

## 步骤 2：解析文档并查找图标链接  

现在我们需要以 **read html document python** 的方式进行操作。虽然可以使用正则表达式，但使用小型 HTML 解析器更可靠。Python 自带的 `html.parser` 可以被子类化以满足我们的需求。

```python
from html.parser import HTMLParser

class IconLinkParser(HTMLParser):
    """Collects href attributes from <link rel='icon'> tags."""
    def __init__(self):
        super().__init__()
        self.icon_hrefs = []

    def handle_starttag(self, tag, attrs):
        if tag.lower() != "link":
            return
        attrs_dict = dict(attrs)
        # Look for rel="icon" (or rel="shortcut icon")
        rel = attrs_dict.get("rel", "").lower()
        if "icon" in rel:
            href = attrs_dict.get("href")
            if href:
                self.icon_hrefs.append(href)

# Instantiate and feed the HTML content
parser = IconLinkParser()
parser.feed(html_content)

# Now we have a list of all icon URLs
icon_hrefs = parser.icon_hrefs
print(f"Found {len(icon_hrefs)} icon link(s):", icon_hrefs)
```

**解释**  
- `handle_starttag` 会在每个起始标签时触发。  
- 我们过滤出 `rel` 属性包含 *icon* 的 `<link>` 元素。这既包括 `rel="icon"`，也包括较旧的 `rel="shortcut icon"`。  
- `href` 值被存入 `icon_hrefs`，准备进行下一步。

---

## 步骤 3：解析相对路径（可选但有帮助）

如果 HTML 使用相对 URL，我们必须将其转换为绝对文件系统路径。这正是 **load html python** 知识与 `urllib.parse` 结合的地方。

```python
import os
from urllib.parse import urljoin

# Base directory where the HTML file lives
BASE_DIR = os.path.dirname(os.path.abspath(HTML_PATH))

def resolve_path(href):
    # If href already looks like an absolute path, return it unchanged
    if os.path.isabs(href):
        return href
    # Otherwise, join it with the base directory
    return os.path.normpath(os.path.join(BASE_DIR, href))

resolved_icon_paths = [resolve_path(h) for h in icon_hrefs]
print("Resolved paths:", resolved_icon_paths)
```

*为什么要这么做？*  
当你随后进行 **write binary file python** 时，需要一个真实的文件路径。像 `images/favicon.ico` 这样的相对 URL 否则会导致 `FileNotFoundError`。

---

## 步骤 4：将每个图标写入本地二进制文件  

这就是 **how to download icons** 的核心。我们将遍历已解析的路径，将每个图标以二进制数据读取，并写入专用的 `icons/` 文件夹中的新文件。

```python
import shutil

OUTPUT_DIR = "YOUR_DIRECTORY/icons"
os.makedirs(OUTPUT_DIR, exist_ok=True)

for index, icon_path in enumerate(resolved_icon_paths):
    # Guard against missing files
    if not os.path.isfile(icon_path):
        print(f"⚠️  Icon file not found: {icon_path}")
        continue

    # Destination filename: icon_0.ico, icon_1.ico, …
    dest_path = os.path.join(OUTPUT_DIR, f"icon_{index}.ico")

    # **write binary file python** – copy the binary data
    with open(icon_path, "rb") as src_file, open(dest_path, "wb") as dst_file:
        shutil.copyfileobj(src_file, dst_file)

    print(f"✅ Saved {dest_path}")
```

**发生了什么？**  

- `os.makedirs(..., exist_ok=True)` 确保输出文件夹存在。  
- `shutil.copyfileobj` 将字节从源流向目标，这是 **write binary file python** 最节省内存的方式。  
- 我们将每个文件命名为 `icon_<index>.ico`，以避免冲突。

**预期输出**

```
Found 2 icon link(s): ['images/favicon.ico', 'icons/custom.ico']
Resolved paths: ['/path/to/YOUR_DIRECTORY/images/favicon.ico',
                '/path/to/YOUR_DIRECTORY/icons/custom.ico']
✅ Saved YOUR_DIRECTORY/icons/icon_0.ico
✅ Saved YOUR_DIRECTORY/icons/icon_1.ico
```

脚本执行完毕后，你将拥有一整套整洁的图标文件，可用于任何后续任务。

---

## 步骤 5：额外内容 – 直接从远程 URL 下载图标  

如果你的 HTML 位于网络而非本地磁盘，请将文件读取部分替换为一个简短的 `requests` 调用。这演示了如何从任何在线页面 **how to extract favicon**。

```python
import requests

REMOTE_URL = "https://example.com"

# Grab the HTML
response = requests.get(REMOTE_URL)
response.raise_for_status()
html_content = response.text

# Re‑run the parser (same as before) to get icon URLs
parser = IconLinkParser()
parser.feed(html_content)
icon_hrefs = parser.icon_hrefs

# Download each icon via HTTP
for index, href in enumerate(icon_hrefs):
    # Resolve relative URLs against the page URL
    icon_url = urljoin(REMOTE_URL, href)
    r = requests.get(icon_url, stream=True)
    r.raise_for_status()
    dest_path = os.path.join(OUTPUT_DIR, f"remote_icon_{index}.ico")
    with open(dest_path, "wb") as out_file:
        shutil.copyfileobj(r.raw, out_file)
    print(f"✅ Downloaded {icon_url} → {dest_path}")
```

**为什么要添加这部分？**  
许多实际项目需要从实时站点抓取 favicon。此代码片段展示了只需几行额外代码，就能将相同的 **how to download icons** 逻辑扩展到互联网。

---

## 常见陷阱与专业技巧

- **Missing `rel="icon"`** – 某些站点通过 `<meta>` 标签或 CSS 嵌入图标。如果需要这些，请扩展解析器以查找 `<meta name="msapplication‑TileImage">` 或 CSS `background-image` URL。  
- **Non‑ICO formats** – 现代 favicon 常使用 `.png` 或 `.svg`。上述代码适用于任何二进制图像；如果你在意保留原始格式，只需在 `dest_path` 中调整文件扩展名。  
- **Permission errors** – 写入文件时，确保脚本对目标文件夹拥有写入权限。使用 `os.makedirs(..., exist_ok=True)` 可避免 “directory not found” 的崩溃。  
- **Large HTML files** – 对于超大页面，考虑逐行流式读取文件，而不是一次性将整个字符串加载到内存中。内置的 `HTMLParser` 能处理增量输入。  

---

## 结论

你刚刚学习了如何使用纯 Python 从 HTML 文档 **下载图标**。通过 **reading html document python**，解析 `<link rel="icon">` 标签，解析任何相对路径，最后使用 **write binary file python** 将每个图标本地保存，你现在拥有一个可复用的脚本，适用于本地和远程页面。

下一步？尝试扩展解析器以捕获 Apple touch icons（`rel="apple-touch-icon"`），或将脚本集成到更大的网络爬虫流水线中，以收集数百个域名的 favicon。这里涉及的基础——HTML 解析、路径解析和二进制文件处理——是许多网页自动化任务的构建块。

有问题或想分享有趣的用例？在下方留言吧，祝你玩得开心，图标狩猎顺利！

## 接下来你应该学习什么？

- [如何在 Aspose.HTML for Java 中编辑 HTML 文档树](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [如何使用 Aspose.HTML for Java 将 HTML 转换为 PDF](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [如何使用 Aspose.HTML for Java 将 HTML 转换为 JPEG](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}