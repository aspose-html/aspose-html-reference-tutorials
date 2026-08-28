---
category: general
date: 2026-06-07
description: 快速将 HTML 生成 Markdown。学习如何在 Python 中将 HTML 转换为 Markdown，导出 HTML 为 Markdown
  并处理边缘情况。
draft: false
keywords:
- create markdown from html
- convert html to markdown
- how to convert html
- html to markdown python
- export html to markdown
language: zh
og_description: 在 Python 中将 HTML 转换为 Markdown。本指南展示了如何将 HTML 转换为 Markdown，导出 HTML
  为 Markdown，并处理常见的陷阱。
og_title: 从HTML创建Markdown – 完整的Python教程
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Create markdown from HTML quickly. Learn how to convert HTML to markdown
    in Python, export html to markdown and handle edge cases.
  headline: Create markdown from HTML – Full Python Guide
  type: TechArticle
- description: Create markdown from HTML quickly. Learn how to convert HTML to markdown
    in Python, export html to markdown and handle edge cases.
  name: Create markdown from HTML – Full Python Guide
  steps:
  - name: 1. Tables That Look Wonky
    text: '`markdownify` converts `<table>` tags into pipe‑separated Markdown tables.
      However, if your source HTML uses `colspan` or `rowspan`, the conversion may
      lose alignment. A quick fix is to pre‑process the HTML with **BeautifulSoup**:'
  - name: 2. Code Blocks Need Fencing
    text: 'If the HTML contains `<pre><code>` blocks, `markdownify` will output them
      as indented blocks, which some Markdown parsers misinterpret. Pass the option
      `code_language="python"` (or whatever language you expect) to force fenced code
      blocks:'
  - name: 3. Unicode and Emojis
    text: 'Python’s default UTF‑8 handling usually does the trick, but if you encounter
      mojibake, explicitly encode/decode:'
  type: HowTo
tags:
- python
- markdown
- html
title: 从HTML生成Markdown – 完整Python指南
url: /zh/python/general/create-markdown-from-html-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 完整指南将 HTML 转换为 Markdown

有没有想过如何 **从 HTML 创建 markdown** 而不抓狂？你并不是唯一的困惑者。无论是爬取博客、提取邮件，还是仅仅想让文档保持整洁，将 HTML 转换为干净的 Markdown 常常像追逐野鹅一样困难。

好消息是？在本指南中，我们将一步步演示一个简洁的端到端解决方案，让你使用纯 Python **convert HTML to markdown**。我们会解释每一步背后的 *why*，展示完整可运行的脚本，并提供一些可靠导出 HTML 为 markdown 的专业技巧。

---

## 本教程涵盖内容

- **前置条件**：Python 3.9+、一个小型第三方库，以及一个示例 HTML 文件。  
- **逐步代码**：加载 HTML 文档、配置转换选项、将生成的 Markdown 写入磁盘。  
- **为何此方法有效**——我们会比较内置的 `html2text` 与更灵活的 `markdownify`。  
- **边缘情况处理**：表格、代码块和 Unicode 字符。  
- **后续步骤**：批量处理、自定义过滤器以及将转换集成到 CI 流水线。

阅读完本文后，你将能够自信地 **export html to markdown**，并且了解如何为自己的项目微调该过程。

---

## 前置条件

在开始之前，请确保你已经具备：

1. **Python 3.9 或更高版本**——`typing` 的改进提升了可读性。  
2. **pip**——标准的包安装工具。  
3. 一个 **示例 HTML 文件**（`input.html`），放置在你可控的文件夹中。  

如果这些都已经准备好，太好了——继续下一步。如果没有，运行 `python --version` 可以查看当前版本，使用 `pip install --upgrade pip` 可保持安装器为最新。

---

## 步骤 1：Create markdown from HTML – Load Your File

首先，需要把 HTML 源码读取到内存中。这正是关键关键词首次登场的地方。

```python
# step1_load_html.py
from pathlib import Path

def load_html(file_path: str) -> str:
    """
    Reads an HTML file and returns its contents as a string.
    """
    html_path = Path(file_path)
    if not html_path.is_file():
        raise FileNotFoundError(f"HTML file not found: {file_path}")
    return html_path.read_text(encoding="utf-8")

# Example usage
html_content = load_html("YOUR_DIRECTORY/input.html")
print("✅ HTML loaded – length:", len(html_content))
```

**为什么这很重要：**  
- 使用 `pathlib.Path` 能实现跨平台的路径处理。  
- 抛出明确的 `FileNotFoundError` 可以避免后期出现神秘的 `NoneType` 错误。  

---

## 步骤 2：Choose the Right Converter – How to Convert HTML

Python 提供了几款可靠的库来完成此任务。最流行的两款是：

| 库 | 优点 | 缺点 |
|---------|------|------|
| `html2text` | 快速，适用于简单页面 | 对复杂表格处理不佳 |
| `markdownify` | 支持表格、代码块以及自定义回调 | 稍慢，需额外依赖 |

为了获得平衡的解决方案，我们将使用 **markdownify**，因为它提供了细粒度的控制——在生产流水线中 **export html to markdown** 时尤为合适。

```bash
pip install markdownify
```

现在，将转换封装进可复用的函数：

```python
# step2_convert.py
from markdownify import markdownify as md

def convert_html_to_markdown(html: str, **options) -> str:
    """
    Converts HTML string to Markdown using markdownify.
    Accepts any markdownify options via **options.
    """
    # Default options can be overridden by callers
    defaults = {
        "heading_style": "ATX",   # # Heading
        "bullets": "*",           # bullet list marker
        "strip": ["script", "style"],  # remove these tags
        "convert": ["a", "img", "code"],  # explicit conversion list
    }
    defaults.update(options)
    return md(html, **defaults)

# Example usage
markdown_content = convert_html_to_markdown(html_content)
print("✅ Conversion done – preview:")
print(markdown_content[:200] + "...")
```

**为何采用这种方式？**  
`markdownify` 允许你传入 `strip`、`convert` 等选项，进而控制哪些标签被移除或转换。当你需要编写 **convert html to markdown python** 脚本以处理多种输入时，这种灵活性至关重要。

---

## 步骤 3：Export HTML to Markdown – Save the Result

得到 Markdown 字符串后，最后一步是将其写入文件。这正是 *export html to markdown* 发光发热的时刻。

```python
# step3_save.py
from pathlib import Path

def save_markdown(markdown: str, output_path: str) -> None:
    """
    Writes the Markdown string to the given file.
    Creates parent directories if they don't exist.
    """
    out_path = Path(output_path)
    out_path.parent.mkdir(parents=True, exist_ok=True)
    out_path.write_text(markdown, encoding="utf-8")
    print(f"✅ Markdown saved to {out_path}")

# Example usage
save_markdown(markdown_content, "YOUR_DIRECTORY/output.md")
```

**为何要写一个辅助函数？**  
将 I/O 与转换分离可以让代码更易于测试。这样，你可以在不触及文件系统的情况下对 `convert_html_to_markdown` 进行单元测试，这是资深开发者的常用模式。

---

## 完整端到端脚本

下面是把上述三步串联起来的完整可运行脚本。将其复制粘贴到名为 `html_to_md.py` 的文件中，调整路径后运行 `python html_to_md.py`。

```python
#!/usr/bin/env python3
"""
html_to_md.py – Convert an HTML file to Markdown and save the result.
Demonstrates how to create markdown from html, convert html to markdown,
and export html to markdown using Python.
"""

from pathlib import Path
from markdownify import markdownify as md

def load_html(file_path: str) -> str:
    html_path = Path(file_path)
    if not html_path.is_file():
        raise FileNotFoundError(f"HTML file not found: {file_path}")
    return html_path.read_text(encoding="utf-8")

def convert_html_to_markdown(html: str, **options) -> str:
    defaults = {
        "heading_style": "ATX",
        "bullets": "*",
        "strip": ["script", "style"],
        "convert": ["a", "img", "code"],
    }
    defaults.update(options)
    return md(html, **defaults)

def save_markdown(markdown: str, output_path: str) -> None:
    out_path = Path(output_path)
    out_path.parent.mkdir(parents=True, exist_ok=True)
    out_path.write_text(markdown, encoding="utf-8")
    print(f"✅ Markdown saved to {out_path}")

def main():
    # Adjust these paths to your environment
    input_html = "YOUR_DIRECTORY/input.html"
    output_md = "YOUR_DIRECTORY/output.md"

    # Load, convert, and save
    html = load_html(input_html)
    markdown = convert_html_to_markdown(html)
    save_markdown(markdown, output_md)

if __name__ == "__main__":
    main()
```

**预期输出：** 运行后，你应该在控制台看到类似如下的信息：

```
✅ Markdown saved to YOUR_DIRECTORY/output.md
```

打开 `output.md`，你会看到格式良好的 Markdown——标题、列表、链接，甚至如果原 HTML 包含表格的话，也会有相应的表格。

---

## 处理常见边缘情况

### 1. 表格显示异常

`markdownify` 会把 `<table>` 标签转换为管道分隔的 Markdown 表格。然而，如果源 HTML 使用了 `colspan` 或 `rowspan`，转换后可能会失去对齐。快速的解决办法是使用 **BeautifulSoup** 预处理 HTML：

```python
from bs4 import BeautifulSoup

def normalize_tables(html: str) -> str:
    soup = BeautifulSoup(html, "html.parser")
    for table in soup.find_all("table"):
        # Remove colspan/rowspan attributes (Markdown can't express them)
        for cell in table.find_all(["td", "th"]):
            cell.attrs.pop("colspan", None)
            cell.attrs.pop("rowspan", None)
    return str(soup)
```

在将字符串传递给 `convert_html_to_markdown` 之前，调用 `normalize_tables(html)`。

### 2. 代码块需要围栏

如果 HTML 包含 `<pre><code>` 块，`markdownify` 默认会输出为缩进块，而某些 Markdown 解析器会误解。传入 `code_language="python"`（或你期望的语言）选项即可强制使用围栏代码块：

```python
markdown = convert_html_to_markdown(html, code_language="python")
```

### 3. Unicode 与表情符号

Python 默认的 UTF‑8 处理通常足够，但若出现乱码（mojibake），可显式进行编码/解码：

```python
html = load_html(input_html).encode("utf-8", errors="ignore").decode()
```

---

## 专业技巧与注意事项

- **批量转换**：将 `main()` 逻辑包装在 `Path.glob("*.html")` 循环中，以处理整个目录。  
- **自定义链接处理**：如果需要重写相对 URL，可向 `markdownify` 提供 `link_callback`。  
- **性能**：处理成千上万的文件时，考虑使用 `multiprocessing.Pool` 并行化转换步骤。  
- **测试**：保存若干已知输出的 `.md` 固件，断言转换结果相符——这对 CI 非常有帮助。  

---

## 结论

我们已经完整演示了如何使用 Python **create markdown from html**。脚本读取 HTML 文档，智能转换为 Markdown，并干净地 **exports html to markdown**。通过理解每一步背后的 *why*——库的选择、表格处理以及安全的文件 I/O——你现在拥有了在真实项目中扩展此流程的坚实基础。

准备好迎接下一个挑战了吗？试着将此脚本接入静态站点生成器，或构建一个小型 Flask 接口，接受 HTML 负载并即时返回 Markdown。天地无限，而你已经装备齐全，尽情实现吧。

有问题或发现了巧妙的改进？在下方留言，让我们一起讨论。祝编码愉快！

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [在 .NET 中使用 Aspose.HTML 将 HTML 转换为 Markdown](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown 转 HTML（Java）——使用 Aspose.HTML 进行转换](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}