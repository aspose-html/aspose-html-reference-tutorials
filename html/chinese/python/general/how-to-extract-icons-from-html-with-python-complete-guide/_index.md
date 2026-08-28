---
category: general
date: 2026-07-02
description: 如何使用 Python 从 HTML 文件中提取图标。学习读取 HTML 文件（Python），解析 HTML 文档，并提取 href 属性以获取
  favicon URL。
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: zh
og_description: 如何使用 Python 从 HTML 页面提取图标。本教程展示了如何读取 HTML 文件、解析文档并提取 favicon URL。
og_title: 如何从HTML中提取图标 – Python指南
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: 使用 Python 从 HTML 中提取图标 – 完整指南
url: /zh/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 从 HTML 中提取图标 – 完整指南

是否曾想过 **如何在不打开浏览器的情况下提取网页图标**？也许你在构建站点目录、SEO 审计工具，或只是对标签页中出现的微小 favicon 感到好奇。好消息是，你只需几行 Python 代码即可实现——无需 Selenium、无需无头 Chrome，只需一个纯文本 HTML 文件。

在本教程中，我们将逐步演示如何读取 HTML 文件（python 读取 html 文件）、解析 HTML 文档，最后 **提取 `<link rel="icon">` 标签的 href 属性** 以获取 favicon URL。完成后，你将拥有一个可在任何静态 HTML 上复用的代码片段，并了解如何处理相对路径或多个图标声明等边缘情况。

## 你将学到

- 使用 Python 加载本地 HTML 文件（read html file python）  
- 使用轻量级解析器安全地 **解析 html 文档**  
- 定位声明图标的 `<link>` 元素  
- **提取 href 属性** 并将其转换为绝对 URL  
- 收集并打印所有发现的 **favicon URL**  

无需外部服务——只需标准库和流行的 **BeautifulSoup** 包。

---

![展示 Python 脚本提取图标的截图 – 如何提取图标](https://example.com/images/extract-icons-python.png "如何提取图标")

*图片 alt 文本：“使用 Python 脚本提取图标”*

## 前置条件

- 已安装 Python 3.8+  
- `beautifulsoup4` 库（`pip install beautifulsoup4`）  
- 需要扫描的本地 HTML 文件（例如 `sample.html`）  

如果你已经具备上述条件，下面开始吧。

## 步骤 1：读取 HTML 文件 Python – 加载文档

首先要做的事是打开文件并将其内容传递给解析器。使用 `with open(..., "r", encoding="utf‑8")` 能保证文件自动关闭，UTF‑8 编码能够处理大多数现代页面。

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**为什么这很重要：** 使用正确的编码打开文件可以防止出现神秘的 `�` 字符，这些字符可能会导致解析器出错。使用标准库中的 `Path` 还能让代码跨平台运行。

## 步骤 2：解析 HTML 文档 – 查找所有图标链接

接下来我们将原始 HTML 交给 **BeautifulSoup**，它会构建可遍历的树结构。我们会查找每个 `rel` 属性包含 `icon` 的 `<link>` 标签。需要注意的是，`rel` 可能是空格分隔的列表（如 `rel="shortcut icon"`），因此需要灵活的检查方式。

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**为什么这一步至关重要：** 直接使用 `soup.find_all("link", rel="icon")` 会漏掉 `rel="shortcut icon"` 或 `rel="apple-touch-icon"` 等变体。我们的辅助函数 `is_icon_link` 能覆盖这些情况，使提取更稳健。

## 步骤 3：提取 href 属性 – 获取 URL

收集到相关标签后，我们从每个标签中提取 `href` 属性。有些页面可能会遗漏 `href`（虽然少见），因此需要对 `None` 做防护。此外，favicon 常常使用相对 URL，所以我们会在已知页面基准 URL 时将其解析为绝对路径。对于本地文件则保持原路径不变。

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**为什么要去除空白字符：** HTML 编写者有时会在 URL 周围不小心添加空格，这会导致后续请求失败。去除空格可以确保得到干净的字符串。

## 步骤 4：提取 Favicon URL – 输出结果

最后，我们打印（或返回）收集到的 URL 列表。在实际脚本中，你可能会将它们写入 CSV、下载图标，或传递给其他服务。下面的简单循环演示了在控制台上显示结果的方式。

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### 处理边缘情况

- **多个 rel 值：** 我们的 `is_icon_link` 检查已经能够捕获 `rel="shortcut icon"` 和 `rel="apple-touch-icon"`。  
- **相对路径：** 如需绝对 URL，可使用 `urllib.parse.urljoin(base_url, href)`。  
- **缺失 href：** `if href:` 的判断会跳过格式错误的标签，避免 `NoneType` 错误。  
- **重复条目：** 可以使用 `icon_urls = list(dict.fromkeys(icon_urls))` 去重。

---

## 完整脚本 – 一站式解决方案

将上述所有代码整合后，这就是完整、可直接运行的程序。将其保存为 `extract_icons.py`，并将 `html_path` 指向任意你想要的文件。

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**预期输出**（假设 `sample.html` 包含两个图标）：

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

使用 `python extract_icons.py` 运行它，你将在控制台看到打印出的 URL。

---

## 常见问题

**问：如果 HTML 使用 `<meta>` 标签来声明图标怎么办？**  
答：有些站点会通过 `<meta itemprop="image">` 嵌入图标。可以扩展 `is_icon_link`，同时检查 `meta` 且 `itemprop="image"`，并提取其 `content` 属性。

**问：我能自动下载这些图标吗？**  
答：可以——只需将每个 URL 传入 `requests.get(url, stream=True)` 并将内容写入文件。记得使用 `urljoin` 处理相对 URL。

**问：这能用于远程页面吗？**  
答：完全可以。将读取文件的步骤替换为 `requests.get(page_url).text`，并将返回的 HTML 字符串传给 BeautifulSoup。只需注意 robots.txt 和请求频率限制。

---

## 小结

我们已经完整演示了 **如何使用 Python 从任意静态 HTML 中提取图标**，从读取文件、解析文档、定位标签到提取 `href` 属性的全过程。这些核心思路——读取文件、解析文档、定位目标标签、获取属性值——在许多网页抓取任务中都非常实用。

接下来可以尝试扩展脚本：

- 将相对 URL 解析为基于页面的绝对 URL  
- 下载每个图标并保存到本地  
- 支持更多图标格式（如 Safari 的 `rel="mask-icon"`）  

欢迎实验，如果遇到问题，欢迎在下方留言。祝你抓取愉快！

## 接下来你可以学习什么？

以下教程与本指南紧密相关，能够帮助你进一步掌握相关 API 功能并探索替代实现方式：

- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}