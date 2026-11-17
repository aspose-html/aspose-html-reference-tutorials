---
category: general
date: 2026-08-12
description: 在 Python 中快速加载 HTML 文件。学习如何使用 Python 读取 HTML 文件、从 URL 加载 HTML，以及在单个教程中从字符串创建
  HTML 文档。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load html from file
- read html file using python
- how to load html in python
- load html from url
- create htmldocument from string
language: zh
lastmod: 2026-08-12
og_description: 使用 HTMLDocument 类在 Python 中从文件加载 HTML。请按照本指南使用 Python 读取 HTML 文件、从
  URL 加载 HTML，并从字符串创建 HTMLDocument，以实现强大的网页内容处理。
og_image_alt: Screenshot of Python code that loads html from file using HTMLDocument
og_title: 在 Python 中从文件加载 HTML – 快速编程指南
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Load html from file in Python quickly. Learn how to read html file
    using python, load html from url, and create htmldocument from string in a single
    tutorial.
  headline: Load html from file in Python – step‑by‑step guide
  type: TechArticle
tags:
- HTML
- Python
- File I/O
- Web scraping
title: 在 Python 中从文件加载 HTML – 步骤指南
url: /zh/python/general/load-html-from-file-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中从文件加载 HTML – 步骤指南

如果你需要 **在 Python 中从文件加载 HTML**，本指南将为你展示完整步骤。你还将学习如何 **使用 python 读取 html 文件**、从 URL 加载 HTML，以及 **从字符串创建 htmldocument**，从而处理任何来源的 HTML 内容。

示例使用 `html_document` 包中的 `HTMLDocument` 类，该类为本地文件、远程 URL 和原始 HTML 字符串提供统一的 API。此方法适用于 Python 3.8+，并能与标准库如 `pathlib` 和 `requests` 无缝集成。

![在 Python 中从文件加载 HTML 的代码截图](image.png)

## 在 Python 中从文件加载 HTML – 基础示例

从本地文件系统加载 HTML 文件是处理静态页面时最常见的第一步。`HTMLDocument` 构造函数接受文件路径，自动检测文件编码并解析标记。

```python
from html_document import HTMLDocument
from pathlib import Path

# Step 1: Define the path to the HTML file
file_path = Path("YOUR_DIRECTORY/page.html")

# Step 2: Create an HTMLDocument instance from the file
doc_from_file = HTMLDocument(file_path)

# Verify that the document was loaded
print("Title:", doc_from_file.title)
```

**工作原理说明：**  
* `Path` 抽象了操作系统特定的路径分隔符，使代码在 Windows、macOS 和 Linux 上均可移植。  
* `HTMLDocument` 以二进制模式读取文件，检测 UTF‑8 或 UTF‑16 BOM，并在必要时回退到系统默认编码。  

**预期输出（假设 HTML 包含 `<title>Example</title>`）：**

```
Title: Example
```

### 加载文件时的常见陷阱

* **FileNotFoundError** – 确认路径正确且文件存在。可使用 `file_path.is_file()` 进行预检查。  
* **编码错误** – 如果页面使用非 UTF‑8 字符集，请向构造函数传入 `encoding="iso-8859-1"`：`HTMLDocument(file_path, encoding="iso-8859-1")`。  

## 使用 python 读取 html 文件 – 详细说明

开发者在需要从已保存的网页中提取数据时，常会搜索 **read html file using python**。虽然 `HTMLDocument` 已封装大部分工作，你仍可以手动加载原始文本并将其传递给解析器。

```python
# Alternative: read the file yourself and pass the string
with open(file_path, "r", encoding="utf-8") as f:
    raw_html = f.read()

doc_from_string = HTMLDocument(raw_html)

print("Number of <p> tags:", len(doc_from_string.find_all("p")))
```

**选择此方式的原因：**  
* 需要在解析前对 HTML 进行预处理（例如去除脚本）。  
* 想要缓存原始标记以便后续复用，而无需再次读取文件。  

## 从 URL 加载 html – 获取远程页面

直接从网络地址加载 HTML 可以将工作流扩展到实时内容。**load html from url** 步骤依赖 `requests` 库进行 HTTP 处理，然后将响应文本交给 `HTMLDocument`。

```python
import requests
from html_document import HTMLDocument

# Step 1: Request the remote page
response = requests.get("https://example.com", timeout=10)

# Raise an exception for HTTP errors (4xx, 5xx)
response.raise_for_status()

# Step 2: Create an HTMLDocument from the response text
doc_from_url = HTMLDocument(response.text)

print("Page title:", doc_from_url.title)
```

**工作原理说明：**  
* `requests.get` 自动跟随重定向并默认支持 HTTPS。  
* `response.raise_for_status()` 确保仅在成功响应时进行解析，防止静默失败。  

**边缘情况处理：**  
* **网络慢** – 调整 `timeout` 参数或使用 `requests.Session` 实现连接池。  
* **非 HTML 内容** – 在解析前检查 `Content-Type` 头部 (`response.headers["Content-Type"]`)。  

## 从字符串创建 htmldocument – 处理原始 HTML

有时你会动态生成 HTML（例如通过模板引擎），并希望在不写入磁盘的情况下将其视为文档。**create htmldocument from string** 操作非常直接。

```python
from html_document import HTMLDocument

# Step 1: Define raw HTML content
html_content = """
<!DOCTYPE html>
<html>
  <head><title>Inline Demo</title></head>
  <body><h1>Hello</h1><p>Generated on the fly.</p></body>
</html>
"""

# Step 2: Instantiate HTMLDocument directly from the string
doc_from_string = HTMLDocument(html_content)

print("Header text:", doc_from_string.find("h1").text)
```

**此方式的优势：**  
* 消除临时文件的需求，提升无服务器环境下的性能。  
* 在将生成的标记发送给客户端或存储之前进行验证。  

**字符串处理技巧：**  
* 使用三引号字符串保持标记的可读性。  
* 若 HTML 包含 Unicode 字符，确保源文件以 UTF‑8 编码保存。  

## 完整端到端示例

将上述四种加载策略组合在一起，展示了一个灵活的管道，能够在本地、远程和内存中的来源之间自由切换。

```python
from pathlib import Path
import requests
from html_document import HTMLDocument

def load_from_file(path_str: str) -> HTMLDocument:
    return HTMLDocument(Path(path_str))

def load_from_url(url: str) -> HTMLDocument:
    resp = requests.get(url, timeout=10)
    resp.raise_for_status()
    return HTMLDocument(resp.text)

def load_from_string(html: str) -> HTMLDocument:
    return HTMLDocument(html)

# Example usage
file_doc = load_from_file("samples/local_page.html")
url_doc = load_from_url("https://example.com")
string_doc = load_from_string("<html><body><h2>Inline</h2></body></html>")

print("File title:", file_doc.title)
print("URL title:", url_doc.title)
print("String heading:", string_doc.find("h2").text)
```

**代码展示的要点：**  

* 单一的 `HTMLDocument` 类处理所有输入类型，降低 API 接口复杂度。  
* 辅助函数封装错误处理，使调用代码简洁。  
* 该模式可扩展至批量处理：遍历文件路径或 URL 列表，将每个文档传入爬虫或转换器。  

## 结论

现在你已经掌握了如何使用 `HTMLDocument` 类 **在 Python 中从文件加载 HTML**，以及如何 **read html file using**（未完）。


## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索在项目中的替代实现方式。每个资源都提供完整的可运行代码示例和逐步解释。

- [Load HTML Documents from URL in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-url/)
- [Load HTML Documents from Stream with Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}