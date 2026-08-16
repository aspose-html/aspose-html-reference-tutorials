---
category: general
date: 2026-05-25
description: 使用轻量级的 HTML 转 Markdown 库将 HTML 转换为 Markdown。了解如何仅用几行代码保存 Markdown 文件的
  HTML 输出。
draft: false
keywords:
- convert html to markdown
- html to markdown library
- save markdown file html
language: zh
og_description: 快速将 HTML 转换为 Markdown。本教程展示如何使用 HTML 转 Markdown 库并保存 Markdown 文件的
  HTML 结果。
og_title: 使用 Python 将 HTML 转换为 Markdown – 快速指南
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: convert html to markdown using a lightweight html to markdown library.
    Learn how to save markdown file html output in just a few lines.
  headline: convert html to markdown with Python – html to markdown lib
  type: TechArticle
- description: convert html to markdown using a lightweight html to markdown library.
    Learn how to save markdown file html output in just a few lines.
  name: convert html to markdown with Python – html to markdown lib
  steps:
  - name: Expected Output
    text: 'Running the script produces a file `links_and_paragraphs.md` containing:'
  - name: 1. What if I need to keep tables too?
    text: 'Just change the filter logic:'
  - name: 2. How does the library handle nested tags like `<strong>` or `<em>`?
    text: '`markdownify` automatically translates `<strong>` → `**bold**` and `<em>`
      → `*italic*`. If you only want links and paragraphs, those lines will be stripped
      by our filter, but you can relax the filter to keep them.'
  - name: 3. Is the conversion Unicode‑safe?
    text: ' ## Related Tutorials

      - [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
      - [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
      - [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Conversion
title: 使用 Python 将 HTML 转换为 Markdown – html to markdown 库
url: /zh/python/general/convert-html-to-markdown-with-python-html-to-markdown-lib/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# convert html to markdown – Full Python Walkthrough

是否曾经需要**convert html to markdown**却不确定该使用哪种工具？你并不孤单。在许多项目中——静态站点生成器、文档流水线或快速数据迁移——将原始 HTML 转换为干净的 Markdown 是日常任务。好消息是，只需一个小巧的**html to markdown library**和几行 Python 代码，你就可以自动化整个过程，甚至**save markdown file html**结果到磁盘，轻松搞定。

在本指南中，我们将从零开始，逐步演示如何安装合适的库、配置转换选项，最后将输出持久化到文件。完成后，你将拥有一个可在任何脚本中直接使用的可复用代码片段，并提供处理链接、表格以及其他棘手 HTML 元素的技巧。

## What You’ll Learn

- 为什么选择合适的**html to markdown library**对保真度和性能至关重要。  
- 如何设置转换选项，只挑选你需要的功能（例如链接和段落）。  
- 完整的代码，能够一次性**convert html to markdown**并**save markdown file html**。  
- 表格、图片和嵌套元素的边缘案例处理。  

不需要任何 Markdown 转换器的先前经验；只需基本的 Python 环境。

---

## Step 1: Pick the Right HTML to Markdown Library

有多个 Python 包声称可以将 HTML 转换为 Markdown，但并非所有都提供细粒度的控制。本文教程将使用**markdownify**，这是一个维护良好的库，允许你通过`markdownify.MarkdownConverter`对象切换单独的特性。它轻量、纯 Python，且在 Windows 与类 Unix 系统上均可运行。

```bash
pip install markdownify
```

> **专业提示:** 如果你在受限环境（例如 AWS Lambda）中运行，请锁定版本（`markdownify==0.9.3`），以避免意外的破坏性更改。

使用**markdownify**满足了我们的次要关键词需求——*html to markdown library*——同时保持代码可读。

## Step 2: Prepare Your HTML Source

让我们定义一个包含标题、带链接的段落以及一个简单表格的小 HTML 片段。这与从博客文章或电子邮件模板中提取的内容相似。

```python
# Step 2: Define the source HTML content
html = """
<h1>Title</h1>
<p>Paragraph with a <a href="https://example.com">link</a>.</p>
<table><tr><td>Cell</td></tr></table>
"""
```

请注意，HTML 被存放在三引号字符串中以提升可读性。你也可以轻松地从文件或网络请求中读取；转换逻辑保持不变。

## Step 3: Configure the Converter with Desired Features

有时你只需要特定的 Markdown 结构。`markdownify`库允许你传入`heading_style`和`bullets`标志，但为了模拟原始示例，我们将重点放在链接和段落上。虽然`markdownify`没有提供位掩码 API，但我们可以通过后处理输出来实现相同效果。

```python
from markdownify import markdownify as md

def convert_html_to_markdown(html_content, keep_links=True, keep_paragraphs=True):
    """
    Convert HTML to Markdown, optionally stripping out unwanted elements.
    """
    # Convert everything first
    full_md = md(html_content, heading_style="ATX")

    # If we only want links and paragraphs, filter the lines
    lines = full_md.splitlines()
    filtered = []

    for line in lines:
        stripped = line.strip()
        if not stripped:
            continue  # skip empty lines

        if keep_links and "[" in stripped and "](" in stripped:
            filtered.append(stripped)
        elif keep_paragraphs and not stripped.startswith("#") and not stripped.startswith("-"):
            # Assume plain text lines are paragraphs
            filtered.append(stripped)

    return "\n\n".join(filtered)
```

辅助函数`convert_html_to_markdown`负责核心工作：它先进行完整转换，然后剔除除链接和段落之外的所有内容。这与原始代码中**html to markdown library**的特性选择模式相呼应。

## Step 4: Save the Markdown Output to a File

现在我们拥有了干净的 Markdown 字符串，持久化它非常直接。我们将结果写入名为`links_and_paragraphs.md`的文件，存放在你指定的目录下。

```python
import os

def save_markdown(markdown_text, directory, filename="output.md"):
    """
    Ensure the target directory exists and write the markdown text to a file.
    """
    os.makedirs(directory, exist_ok=True)  # creates the folder if needed
    file_path = os.path.join(directory, filename)

    with open(file_path, "w", encoding="utf-8") as f:
        f.write(markdown_text)

    print(f"✅ Markdown saved to {file_path}")
```

这里我们满足了**save markdown file html**的需求：函数明确处理路径，并使用 UTF‑8 编码以保留可能出现的非 ASCII 字符。

## Step 5: Put It All Together – Full Working Script

下面是完整、可运行的脚本，将所有步骤整合在一起。复制粘贴到名为`html_to_md.py`的文件中，然后执行`python html_to_md.py`。根据需要修改`output_dir`变量，以指定 Markdown 文件的保存位置。

```python
# html_to_md.py
# ----------------------------------------------------
# Complete example: convert html to markdown and save
# ----------------------------------------------------
from markdownify import markdownify as md
import os

# --- Step 1: Define source HTML ------------------------------------------------
html = """
<h1>Title</h1>
<p>Paragraph with a <a href="https://example.com">link</a>.</p>
<table><tr><td>Cell</td></tr></table>
"""

# --- Step 2: Conversion helper -------------------------------------------------
def convert_html_to_markdown(html_content, keep_links=True, keep_paragraphs=True):
    """
    Convert HTML to Markdown, optionally keeping only links and paragraphs.
    """
    full_md = md(html_content, heading_style="ATX")
    lines = full_md.splitlines()
    filtered = []

    for line in lines:
        stripped = line.strip()
        if not stripped:
            continue

        if keep_links and "[" in stripped and "](" in stripped:
            filtered.append(stripped)
        elif keep_paragraphs and not stripped.startswith("#") and not stripped.startswith("-"):
            filtered.append(stripped)

    return "\n\n".join(filtered)

# --- Step 3: Save helper -------------------------------------------------------
def save_markdown(markdown_text, directory, filename="links_and_paragraphs.md"):
    """
    Save markdown_text to `directory/filename`. Creates the directory if missing.
    """
    os.makedirs(directory, exist_ok=True)
    file_path = os.path.join(directory, filename)

    with open(file_path, "w", encoding="utf-8") as f:
        f.write(markdown_text)

    print(f"✅ Markdown saved to {file_path}")

# --- Step 4: Execute conversion & saving ---------------------------------------
if __name__ == "__main__":
    # Choose which features you need – here we keep links & paragraphs only
    markdown_result = convert_html_to_markdown(html, keep_links=True, keep_paragraphs=True)

    # Define where you want the .md file to live
    output_dir = "YOUR_DIRECTORY"

    # Finally, write the file
    save_markdown(markdown_result, output_dir)
```

### Expected Output

运行脚本后会生成文件`links_and_paragraphs.md`，内容如下：

```markdown
Paragraph with a [link](https://example.com).

Cell
```

- 标题（`# Title`）被省略，因为我们只请求了链接和段落。  
- 表格单元格被渲染为纯文本，展示了过滤器的工作方式。

---

## Common Questions & Edge Cases

### 1. What if I need to keep tables too?

只需修改过滤逻辑：

```python
elif keep_tables and stripped.startswith("|"):
    filtered.append(stripped)
```

在函数签名中添加`keep_tables`标志，并在调用时将其设为`True`。

### 2. How does the library handle nested tags like `<strong>` or `<em>`?

`markdownify`会自动将`<strong>`转换为`**bold**`，将`<em>`转换为`*italic*`。如果你只想保留链接和段落，这些行会被我们的过滤器剔除，但你可以放宽过滤条件以保留它们。

### 3. Is the conversion Unicode‑safe?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}