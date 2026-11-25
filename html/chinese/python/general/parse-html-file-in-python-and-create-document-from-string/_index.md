---
category: general
date: 2026-09-16
description: 在 Python 中解析 HTML 文件，从文件加载 HTML 文档，并使用简洁、可直接运行的代码从字符串创建 HTML 文档。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- parse html file in python
- create html document from string
- load html document from file
- read local html file python
language: zh
lastmod: 2026-09-16
og_description: 在 Python 中解析 HTML 文件，以快速可靠地读取本地 HTML 文件并从字符串创建 HTML 文档。
og_image_alt: Screenshot of Python code parsing an HTML file and creating a document
  from a string
og_title: 在 Python 中解析 HTML 文件 – 从字符串创建文档
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  headline: Parse HTML file in Python and create document from string
  type: TechArticle
- description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  name: Parse HTML file in Python and create document from string
  steps:
  - name: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
    text: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
  - name: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
    text: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
  - name: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
    text: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
  type: HowTo
tags:
- python html parsing
- html document creation
- file handling python
title: 在 Python 中解析 HTML 文件并从字符串创建文档
url: /zh/python/general/parse-html-file-in-python-and-create-document-from-string/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中解析 HTML 文件并从字符串创建文档

如果您需要**parse HTML file in Python**，本指南将准确展示如何读取本地 HTML 文件、从文件加载 HTML 文档，以及**create HTML document from string**。无论是爬取数据、测试模板，还是生成动态内容，下面的步骤都为您提供完整、可运行的解决方案。

在本教程中，您将学习如何：

* 使用 Python 标准库读取本地 HTML 文件。
* 从文件路径加载 HTML 文档。
* 直接从 HTML 字符串创建 HTML 文档。
* 处理常见的边缘情况，例如文件缺失和编码问题。

唯一的前置条件是 Python 3.8+ 和 `beautifulsoup4` 库，我们将在第一步中进行安装。

## 前置条件

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8 或更高版本 | 确保与类型提示和现代语法兼容。 |
| `beautifulsoup4` 和 `lxml` 包 | 提供强大的解析器，能够处理错误的 HTML 并为您提供便利的 `HTMLDocument`‑like 对象。 |
| 项目文件夹中的示例 HTML 文件（`index.html`） | 作为 **load html document from file** 示例的输入。 |

使用 pip 安装依赖：

```bash
pip install beautifulsoup4 lxml
```

## 在 Python 中解析 HTML 文件

本教程的核心是**parse html file in python**操作。我们将把 BeautifulSoup 包装在一个名为 `HTMLDocument` 的小型辅助类中，以使 API 与您之前看到的示例保持一致。

```python
from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """
    Simple wrapper that mimics a “document” object.
    Accepts either a file path or a raw HTML string.
    """
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            # Load html document from file
            self._load_from_file(Path(source))
        else:
            # Assume source is a raw HTML string
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            # read local html file python – explicit UTF‑8 handling
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        """Return the content of the <title> tag, or an empty string."""
        if self.soup.title:
            return self.soup.title.string.strip()
        return ""

    def pretty(self) -> str:
        """Return a nicely formatted HTML representation."""
        return self.soup.prettify()
```

### 工作原理

1. **Detect source type** – 构造函数检查提供的 `source` 是否在磁盘上存在。如果存在，我们**load html document from file**；否则将其视为原始字符串，以满足**create html document from string**的需求。  
2. **Read the file** – 我们使用 `Path.read_text(encoding="utf-8")`，这是安全地**read local html file python**的推荐方式。  
3. **Parse with BeautifulSoup** – `lxml` 解析器速度快且能容忍错误的标记。

## 从文件加载 HTML 文档

现在我们已有 `HTMLDocument` 类，加载文件变得简单直观：

```python
# Step 1: Load an HTML document from a local file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")

# Verify that the file was parsed correctly
print("Document title:", doc.title())
```

**预期输出**（假设 `index.html` 包含 `<title>My Page</title>`）：

```
Document title: My Page
```

如果文件不存在，类会抛出明确的 `FileNotFoundError`，您可以在生产代码中捕获它。

## 从字符串创建 HTML 文档

直接从字符串创建文档对于测试或即时生成 HTML 非常有用：

```python
# Step 2: Create an HTML document directly from an HTML string
html_content = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
doc_from_string = HTMLDocument(html_content)

print("String‑based title:", doc_from_string.title())
```

**预期输出**：

```
String-based title: Hello
```

由于相同的 `HTMLDocument` 类处理这两种情况，您可以获得一致的 API 来**parse html file in python**，无论源是文件还是字符串。

## 读取本地 HTML 文件 Python – 处理边缘情况

在处理真实文件时，您常会遇到：

* **Missing files** – 已由 `FileNotFoundError` 处理。  
* **Different encodings** – 您可以让 BeautifulSoup 猜测编码，但显式使用 UTF‑8 最安全。  
* **Large files** – 将整个文件读取到内存可能代价高昂；如有需要，可使用 `BeautifulSoup(open(...), "lxml")` 进行流式处理。

下面是一个防御性包装器，添加了这些安全措施：

```python
def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """
    Load an HTML file safely, handling missing files and encoding issues.
    Returns an HTMLDocument instance or raises a descriptive exception.
    """
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; consider specifying the correct encoding.")
```

现在您可以调用 `safe_load_html("index.html")`，并确信错误会被清晰报告，从而获得相同的 `HTMLDocument` 对象。

## 专业提示和常见陷阱

* **Avoid “just” using `open(...).read()`** – `Path.read_text` 在一行中处理路径展开和编码。  
* **Don’t forget to close file handles** – `Path.read_text` 会自动关闭；如果使用 `open()`，请将其包装在 `with` 块中。  
* **Prefer `lxml` over the default parser** – 它更快且更能容忍破损的标记，这在您从网络**parse html file in python**时至关重要。  
* **When creating from a string, ensure it’s a complete HTML document** – 缺少 `<html>` 或 `<body>` 标签可能导致查询元素时出现意外的 `None` 结果。

## 完整脚本，复制粘贴即可

下面是一个独立的脚本，演示了所有讨论的步骤。将其保存为 `html_demo.py` 并运行 `python html_demo.py`。



## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。每个资源均包含完整的可运行代码示例和逐步解释。

- [在 Aspose.HTML for Java 中将 HTML 文档保存到文件](/html/english/java/saving-html-documents/save-html-to-file/)
- [在 Aspose.HTML for Java 中从文件加载 HTML 文档](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [使用 Aspose.HTML 创建 HTML 文档 – 步骤指南](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}