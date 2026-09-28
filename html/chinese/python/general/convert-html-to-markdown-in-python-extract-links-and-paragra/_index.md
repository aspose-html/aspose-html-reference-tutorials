---
category: general
date: 2026-09-26
description: 使用 Python 将 HTML 转换为 Markdown，提取 HTML 中的链接并将 HTML 保存为 Markdown。学习一步一步的
  HTML 转换方法。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: zh
lastmod: 2026-09-26
og_description: 使用 Python 将 HTML 转换为 Markdown，提取 HTML 中的链接并将 HTML 保存为 Markdown。请遵循本完整指南。
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: 在 Python 中将 HTML 转换为 Markdown – 提取链接和段落
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: 在 Python 中将 HTML 转换为 Markdown ——轻松提取链接和段落
url: /zh/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为 Markdown – 轻松提取链接和段落

如果你需要 **将 HTML 转换为 Markdown** 并且只保留有用的部分，本指南将展示如何仅用几行 Python 代码实现。无论是抓取博客文章、归档文档，还是清理电子邮件正文，你都能学到一种可靠的方法来从 HTML 中提取链接并将 HTML 保存为 Markdown。

本教程涵盖了从安装所需包到处理空 `<a>` 标签或嵌套段落等边缘情况的全部内容。完成后，你将拥有一个可直接运行的脚本，能够 **将 HTML 转换为 Markdown**、**从 HTML 中提取链接**，以及在需要时 **从 HTML 中提取段落**。

---

## 前置条件

在开始之前，请确保你已经：

* 安装了 Python 3.8 或更高版本  
* 能够访问 `groupdocs-conversion` Python 包（该库提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter`）  
* 拥有一个本地的 HTML 文件（例如 `article.html`）需要处理

你可以使用 pip 安装该库：

```bash
pip install groupdocs-conversion
```

> **小贴士：** 使用虚拟环境（`python -m venv venv`）可以让依赖保持隔离。

---

## 第一步：加载源 HTML 文档

首先创建一个指向源文件的 `HTMLDocument` 对象。该对象抽象了原始 HTML，并为转换器提供了干净的入口点。

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*为什么重要：* 以这种方式加载文档可以让库只解析一次 DOM，从而使后续操作（如提取链接或段落）既快速又节省内存。

---

## 第二步：创建 Markdown 保存选项并选择所需功能

`MarkdownSaveOptions` 让你决定哪些 HTML 元素会在转换后保留下来。`features` 标志使用按位或来组合选项。

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*为什么重要：* 通过指定 `LINKS` 和 `PARAGRAPHS`，你可以 **从 HTML 中提取链接** 并 **从 HTML 中提取段落**，同时丢弃其他所有内容（样式、脚本、图片）。如果以后只需要链接，只需将 `MarkdownFeatures.PARAGRAPHS` 替换为 `0`（或直接省略）。

---

## 第三步：使用配置好的选项将 HTML 转换为 Markdown

现在调用静态的 `convert_html` 方法，传入源文档、目标路径以及刚才构建的选项。

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*为什么重要：* 转换在一次遍历中完成，并应用了你定义的特性过滤器。生成的文件（`article_links.md`）仅包含 Markdown 格式的链接和段落，这正是你在 **将 HTML 保存为 Markdown** 以供后续处理时所需要的。

---

## 完整脚本 – 整合所有步骤

下面是一段完整、可运行的脚本，你可以直接复制粘贴到名为 `html_to_md.py` 的文件中。根据你的环境自行调整路径。

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### 预期输出

运行脚本后会生成类似以下内容的文件（具体内容取决于源 HTML）：

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

仅会出现链接文本和段落文本，所有其他 HTML 元素都会被剔除。

---

## 仅提取链接或仅提取段落（高级变体）

有时你只需要 **将 HTML 转换为** 包含单一类型元素的 Markdown 文件。

### 1. 仅提取链接

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. 仅提取段落

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

这两种变体都复用了同一个 `convert_html` 调用，无需编写额外的转换逻辑。

---

## 处理边缘情况

| 情况                                   | 推荐的解决方案 |
|----------------------------------------|-----------------|
| HTML 文件包含空的 `<a>` 标签          | 转换器会自动跳过空链接。如果看到多余的 `[]()` 条目，可设置 `md_options.removeEmptyLinks = True`。 |
| 嵌套段落（`<p>` 位于 `<div>` 内）      | 库会将嵌套段落展平，保持文本顺序。无需额外代码。 |
| 链接标题中出现非 ASCII 字符            | 确保你的 Python 文件以 UTF-8 编码保存，并在后续读取输出文件时使用 `encoding="utf-8"`。 |
| 超大 HTML 文件（≥ 50 MB）               | 使用 `HTMLDocument(stream=io.BytesIO(...))` 分块处理文件，避免一次性加载整个文件到内存。 |

---

## 常见问题

**问：这能处理没有 `<html>` 根标签的 HTML 片段吗？**  
答：可以。`HTMLDocument` 接受任何格式良好的片段，转换器会将片段视为文档主体。

**问：我能把图片保留为 Markdown 的图片语法吗？**  
答：在 `features` 标志中加入 `MarkdownFeatures.IMAGES` 即可：  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**问：如何一次性转换目录中的多个文件？**  
答：将 `convert_html_to_markdown` 包装在循环中，使用 `os.listdir` 或 `pathlib.Path.rglob("*.html")` 遍历目录。

---

## 结论

现在你已经掌握了如何在 Python 中 **将 HTML 转换为 Markdown**，并且能够有选择地 **从 HTML 中提取链接** 与 **从 HTML 中提取段落**。本脚本演示了标准流程——加载文档、配置 `MarkdownSaveOptions`、运行 `Converter.convert_html`。只需少量调整，你还可以 **将 HTML 保存为仅包含链接、仅包含段落或完整保真的 Markdown**。

接下来，你可以尝试：

* 添加 `MarkdownFeatures.HEADINGS` 以保留章节标题。  
* 将生成的 Markdown 用作 MkDocs、Hugo 等静态站点生成器的输入。  
* 为整个文档库实现批量转换自动化。

祝你转换愉快！

## 接下来你应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索在项目中的其他实现方式。每篇资源都提供完整可运行的代码示例和逐步解释。

- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}