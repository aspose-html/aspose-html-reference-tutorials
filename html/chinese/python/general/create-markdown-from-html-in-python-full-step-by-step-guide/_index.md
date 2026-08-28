---
category: general
date: 2026-06-07
description: 使用 Python 快速将 HTML 转换为 Markdown。学习如何将 HTML 转换为 Markdown，处理边缘情况，并自动化 HTML
  到 Markdown 的 Python 工作流。
draft: false
keywords:
- create markdown from html
- convert html to markdown
- how to convert html
- html to markdown conversion
- html to markdown python
language: zh
og_description: 使用 Python 将 HTML 转换为 Markdown。本教程展示了如何将 HTML 转换为 Markdown，涵盖常见陷阱和最佳实践。
og_title: 使用 Python 将 HTML 转换为 Markdown – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Create markdown from html quickly with Python. Learn how to convert
    html to markdown, handle edge cases, and automate the html to markdown python
    workflow.
  headline: Create Markdown from HTML in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create markdown from html quickly with Python. Learn how to convert
    html to markdown, handle edge cases, and automate the html to markdown python
    workflow.
  name: Create Markdown from HTML in Python – Full Step‑by‑Step Guide
  steps:
  - name: Why this function works
    text: '- **`pathlib.Path`** gives you OS‑independent file handling—no more fiddling
      with slashes. - **`markdownify`** does the heavy lifting of the **html to markdown
      conversion**. It respects heading levels, list nesting, and even converts `<code>`
      blocks. - The optional arguments let you tweak the output'
  - name: How this helps with **html to markdown python** projects
    text: '- **Preserves hierarchy** – subfolders stay intact, which is crucial for
      navigation‑aware static sites. - **Zero‑configuration defaults** – just point
      to the source folder and let the script do the rest. - **Extensible** – you
      can add a `post_process` callback to further clean up the Markdown (e.g.,'
  - name: 5.1 Tables
    text: '`markdownify` renders tables as pipe‑separated Markdown by default, but
      some older versions struggle with colspan/rowspan. If you hit malformed tables,
      consider a fallback to `pandas.read_html` + `to_markdown`.'
  - name: 5.2 Code Blocks with Language Hints
    text: 'HTML often uses `<pre><code class="language-python">`. `markdownify` will
      keep the code but lose the language hint. A quick post‑process step restores
      it:'
  - name: 5.3 Relative Image Paths
    text: 'If your HTML references images like `<img src="assets/img.png">`, the generated
      Markdown will keep the same relative path, which may break when the Markdown
      file lives elsewhere. Solve it by passing a `base_url` parameter to the converter:'
  type: HowTo
tags:
- markdown
- python
- html
- conversion
title: 在 Python 中将 HTML 转换为 Markdown – 完整逐步指南
url: /zh/python/general/create-markdown-from-html-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中从 HTML 创建 Markdown – 完整分步指南

是否曾经需要**从 html 创建 markdown**但不确定该选哪个库？你并不孤单——许多开发者在尝试自动化文档流水线时都会遇到同样的难题。好消息是，只需几行 Python 代码，你就可以可靠地**将 html 转换为 markdown**，并且能够完全控制诸如表格、代码片段和 Unicode 字符等边缘情况。

在本指南中，我们将逐步讲解你需要了解的所有内容：从安装合适的包到处理棘手的标记，同时保持代码可读、输出干净。结束时，你将能够自信地回答“**如何转换 html**？”并将 **html to markdown python** 过程集成到任何 CI/CD 工作流中。

## 你将学到的内容

- 安装并配置一个轻量级库，用于 **html to markdown conversion**。  
- 编写一个可复用的函数，接受 HTML 文件并输出 Markdown 文件。  
- 解决常见陷阱，如嵌套列表、相对图片 URL 和 HTML 实体。  
- 将解决方案扩展为批量处理整个 HTML 文件目录。  

不需要任何 Markdown 库的先前经验；只需一个可用的 Python 3 环境以及对干净文档的好奇心。

## 前提条件

| 需求 | 原因 |
|-------------|----------------|
| Python 3.8 or newer | 保证与 `markdownify` 包的兼容性。 |
| `pip` (Python package manager) | 需要安装第三‑party libraries。 |
| A small HTML file (e.g., `input.html`) | 为 **html to markdown conversion** 演示提供具体的源文件。 |

如果你已经配置好 Python，便可以直接开始。

## 第一步 – 安装 `markdownify` 包

要 **从 html 创建 markdown**，我们将使用流行的 `markdownify` 库。它体积小、纯 Python，并且开箱即能处理大多数 HTML 标签。

```bash
pip install markdownify
```

> **专业提示：** 如果你在虚拟环境中工作（强烈推荐），请先激活它——这可以防止与其他项目的版本冲突。

## 第二步 – 编写一个简单的转换函数

下面是一个完整的、可直接运行的脚本，它读取 HTML 文件，进行转换，并将结果写入 Markdown 文件。该函数故意保持简短，便于在任何项目中直接使用。

```python
# convert_html_to_md.py
import pathlib
from markdownify import markdownify as md

def create_markdown_from_html(
    html_path: pathlib.Path,
    markdown_path: pathlib.Path,
    *,
    heading_style: str = "ATX",   # ATX => # Heading, Setext => Underline style
    strip: bool = True,
    convert_links: bool = True,
) -> None:
    """
    Convert an HTML document to Markdown.

    Parameters
    ----------
    html_path : pathlib.Path
        Path to the source HTML file.
    markdown_path : pathlib.Path
        Destination path for the generated .md file.
    heading_style : str, optional
        Either "ATX" (default) or "Setext". Controls how headings are rendered.
    strip : bool, optional
        Remove leading/trailing whitespace from the output.
    convert_links : bool, optional
        Preserve <a> tags as Markdown links when True.

    Returns
    -------
    None
    """
    # 1️⃣ Load the source HTML document
    raw_html = html_path.read_text(encoding="utf-8")

    # 2️⃣ Convert HTML to Markdown using markdownify's options
    markdown_text = md(
        raw_html,
        heading_style=heading_style,
        strip=strip,
        convert_links=convert_links,
    )

    # 3️⃣ Save the result to the target file
    markdown_path.write_text(markdown_text, encoding="utf-8")
    print(f"✅ {html_path.name} → {markdown_path.name} completed.")
```

### 为什么这个函数有效

- **`pathlib.Path`** 为你提供跨 OS 的文件处理——不再需要手动处理斜杠。  
- **`markdownify`** 完成 **html to markdown conversion** 的核心工作。它保留标题层级、列表嵌套，甚至会转换 `<code>` 块。  
- 可选参数让你在不修改核心逻辑的情况下微调输出，这在需要为特定平台使用不同标题样式时非常方便。

## 第三步 – 对单个文件运行转换器

在脚本所在的同一文件夹中创建一个小的 `input.html`：

```html
<!-- input.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Sample Document</title>
</head>
<body>
  <h1>Welcome to the Demo</h1>
  <p>This paragraph contains <strong>bold</strong> and <em>italic</em> text.</p>
  <ul>
    <li>First item</li>
    <li>Second item with <a href="https://example.com">a link</a></li>
  </ul>
  <pre><code>print("Hello, world!")</code></pre>
</body>
</html>
```

现在从一个简短的驱动脚本调用该函数：

```python
# run_converter.py
from pathlib import Path
from convert_html_to_md import create_markdown_from_html

if __name__ == "__main__":
    src = Path("input.html")
    dst = Path("output.md")
    create_markdown_from_html(src, dst)
```

运行 `python run_converter.py` 会生成 `output.md`，其内容如下：

```markdown
# Welcome to the Demo

This paragraph contains **bold** and *italic* text.

- First item
- Second item with [a link](https://example.com)

```python
print("Hello, world!")
```
```

> **刚才发生了什么？** 脚本通过将原始 HTML 传入 `markdownify`，**从 html 创建了 markdown**，返回了保持原始结构的干净 Markdown。

## 第四步 – 批量处理整个目录

大多数实际场景涉及数十甚至数百个 HTML 文件（比如导出的 Confluence 页面、旧版文档或静态站点生成器）。下面的代码片段将前面的函数扩展为遍历目录树并自动转换所有文件。

```python
# batch_convert.py
import pathlib
from convert_html_to_md import create_markdown_from_html

def batch_convert_html_to_md(
    source_dir: pathlib.Path,
    target_dir: pathlib.Path,
    *,
    pattern: str = "*.html"
) -> None:
    """
    Walk `source_dir`, convert each HTML file to Markdown,
    and preserve the original folder structure inside `target_dir`.
    """
    for html_file in source_dir.rglob(pattern):
        # Preserve sub‑folder layout
        relative_path = html_file.relative_to(source_dir).with_suffix(".md")
        markdown_file = target_dir / relative_path
        markdown_file.parent.mkdir(parents=True, exist_ok=True)

        create_markdown_from_html(html_file, markdown_file)

    print(f"✅ Batch conversion complete: {source_dir} → {target_dir}")

if __name__ == "__main__":
    batch_convert_html_to_md(
        source_dir=pathlib.Path("html_docs"),
        target_dir=pathlib.Path("markdown_docs")
    )
```

### 这对 **html to markdown python** 项目有何帮助

- **保留层级结构** —— 子文件夹保持完整，这对具备导航感知的静态站点至关重要。  
- **零配置默认值** —— 只需指向源文件夹，脚本会自动完成其余工作。  
- **可扩展** —— 你可以添加 `post_process` 回调，以进一步清理 Markdown（例如，替换图片 URL）。

## 第五步 – 处理边缘情况

虽然 `markdownify` 已经做得相当不错，但某些 HTML 模式仍需额外处理。以下是常见的陷阱及其解决方案。

### 5.1 表格

`markdownify` 默认将表格渲染为管道分隔的 Markdown，但某些旧版本在处理 colspan/rowspan 时会出现问题。如果遇到格式错误的表格，可考虑回退使用 `pandas.read_html` + `to_markdown`。

```python
import pandas as pd

def table_to_markdown(html_table: str) -> str:
    df = pd.read_html(html_table)[0]   # grabs the first table
    return df.to_markdown(index=False)
```

你可以通过正则预处理 HTML 字符串，提取 `<table>` 块并用函数的输出替换，从而将其挂接到转换器中。

### 5.2 带语言提示的代码块

HTML 常使用 `<pre><code class="language-python">`。`markdownify` 会保留代码，但会丢失语言提示。快速的后处理步骤可以恢复它：

```python
import re

def add_language_hints(md_text: str) -> str:
    pattern = r"```(\n)(.+?)```"
    return re.sub(pattern, r"```python\1\2```", md_text, flags=re.DOTALL)
```

在写入磁盘之前，对结果调用 `add_language_hints`。

### 5.3 相对图片路径

如果你的 HTML 引用了类似 `<img src="assets/img.png">` 的图片，生成的 Markdown 将保留相同的相对路径，这在 Markdown 文件位于其他位置时可能会失效。通过向转换器传递 `base_url` 参数可以解决此问题：

```python
def create_markdown_from_html(..., base_url: str = ""):
    # inside the function, after markdownify:
    if base_url:
        md_text = md_text.replace("](", f"]({base_url}")
    # then write out
```

当你知道资源将托管的位置时，设置 `base_url="https://mycdn.example.com/"`。

## 第六步 – 验证输出

快速的合理性检查可以节省后续数小时的调试时间。下面是一个小助手，用于断言 Markdown 文件非空且至少包含一个标题。

```python
def verify_markdown(md_path: pathlib.Path) -> bool:
    content = md_path.read_text(encoding="utf-8")
    if not content.strip():
        raise ValueError("Generated Markdown is empty.")
    if not any(line.startswith("#") for line in content.splitlines()):
        raise ValueError("No top‑level heading found.")
    return True
```

集成

## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本指南展示的技术。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [在 Aspose.HTML for .NET 中将 HTML 转换为 Markdown](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown 转 HTML（Java） - 使用 Aspose.HTML 转换](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}