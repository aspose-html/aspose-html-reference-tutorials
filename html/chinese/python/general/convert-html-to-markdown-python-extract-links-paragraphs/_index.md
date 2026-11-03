---
category: general
date: 2026-08-03
description: 使用 Python 将 HTML 转换为 Markdown。了解如何在一次高效的转换中从 HTML 中提取链接和段落。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- extract paragraphs from html
language: zh
lastmod: 2026-08-03
og_description: 在 Python 中将 HTML 转换为 Markdown，提供一个简洁示例，展示如何从 HTML 中提取链接和段落，并将结果保存为
  Markdown 文件。
og_image_alt: Screenshot of Python code converting an HTML file to Markdown with selected
  links and paragraphs
og_title: 在 Python 中将 HTML 转换为 Markdown – 完整提取指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-03'
  description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  headline: Convert HTML to Markdown Python – extract links & paragraphs
  type: TechArticle
- description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  name: Convert HTML to Markdown Python – extract links & paragraphs
  steps:
  - name: Load the HTML document you want to convert
    text: '```python from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions,
      Converter'
  - name: Create a feature set that includes only the elements you need
    text: '```python # Instantiate the feature collection. selected_features = MarkdownSaveOptions.Features()'
  - name: Attach the feature set to the Markdown save options
    text: '```python md_options = MarkdownSaveOptions() md_options.features = selected_features
      ```'
  - name: Perform the conversion and save the result as a Markdown file
    text: '```python output_path = "YOUR_DIRECTORY/links_and_paragraphs.md" Converter.convert_html(html_doc,
      md_options, output_path) print(f"Conversion complete. Markdown saved to {output_path}")
      ```'
  type: HowTo
tags:
- HTML conversion
- Markdown
- Python
title: 将HTML转换为Markdown（Python）——提取链接和段落
url: /zh/python/general/convert-html-to-markdown-python-extract-links-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为 Markdown（Python）——提取链接和段落

如果您需要 **将 HTML 转换为 Markdown**，本教程将向您展示在 Python 中实现此操作的实用方法，同时有选择地 **从 HTML 中提取链接** 和 **从 HTML 中提取段落**。您将看到一个完整、可运行的示例，它会将过滤后的内容保存为干净的 Markdown 文件。

将 HTML 转换为 Markdown 是在需要轻量、版本控制的文档、静态站点内容或仅仅是网页的纯文本表示时的常见步骤。阅读完本指南后，您将拥有一个脚本，能够：

1. 从磁盘加载 HTML 文档。  
2. 配置仅保留链接和段落元素的特性集合。  
3. 使用 GroupDocs Conversion SDK for Python 执行转换。  
4. 将结果写入 `.md` 文件。

## 前置条件

在开始之前，请确保您具备以下条件：

| 要求 | 为什么重要 |
|------|------------|
| Python 3.9+ | SDK 目标是现代 Python 版本。 |
| `groupdocs-conversion` 包 | 提供示例中使用的 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 类。 |
| 用于测试的 HTML 文件（例如 `sample.html`） | 您将要转换的源文件。 |

使用 pip 安装 SDK：

```bash
pip install groupdocs-conversion
```

> **小技巧：** 使用虚拟环境（`python -m venv .venv`）来保持依赖隔离。

## 使用 Python 将 HTML 转换为 Markdown

转换的核心包含几个直接的步骤。下面逐一说明，每一步都有解释，完整脚本位于文章末尾。

### 步骤 1：加载要转换的 HTML 文档

```python
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, Converter

# Replace YOUR_DIRECTORY with the path that contains your HTML file.
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*为什么要这一步？*  
`HTMLDocument` 解析源文件并构建内部 DOM 表示，供转换器使用。如果不先加载文档，SDK 将无可处理的内容。

### 步骤 2：创建仅包含所需元素的特性集合

```python
# Instantiate the feature collection.
selected_features = MarkdownSaveOptions.Features()

# Keep only hyperlinks.
selected_features.add(MarkdownSaveOptions.Features.LINK)

# Keep only paragraph tags.
selected_features.add(MarkdownSaveOptions.Features.PARAGRAPH)
```

*为什么要添加这些特性*  
`MarkdownSaveOptions.Features` 充当过滤器。通过添加 `LINK` 和 `PARAGRAPH`，我们告诉转换器 **从 HTML 中提取链接** 并 **从 HTML 中提取段落**，忽略图片、表格、脚本等在最终 Markdown 中可能不需要的标记。

### 步骤 3：将特性集合附加到 Markdown 保存选项

```python
md_options = MarkdownSaveOptions()
md_options.features = selected_features
```

*为什么要这一步？*  
`MarkdownSaveOptions` 保存所有转换偏好。将先前构建的 `selected_features` 赋值进去，可确保转换遵循我们的过滤配置。

### 步骤 4：执行转换并将结果保存为 Markdown 文件

```python
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert_html(html_doc, md_options, output_path)
print(f"Conversion complete. Markdown saved to {output_path}")
```

*为什么要调用 `convert_html`*  
`Converter.convert_html` 是 SDK 进行 HTML‑to‑Markdown 转换的入口。它读取 `HTMLDocument`，应用 `md_options`，并将过滤后的输出写入 `output_path`。

#### 预期输出

生成的 `links_and_paragraphs.md` 将仅包含超链接和段落文本的 Markdown 表示，例如：

```markdown
[Visit the homepage](https://example.com)

This is the first paragraph of the article, describing the main topic.

Another paragraph with more details.
```

所有其他 HTML 元素，如 `<img>`、`<table>` 或 `<script>` 均被省略，使文件保持轻量且易于编辑。

## 从 HTML 中提取链接（可选深入）

如果您的目标是 **仅从 HTML 中提取链接** 并丢弃其他所有内容，可以简化特性集合：

```python
link_only_features = MarkdownSaveOptions.Features()
link_only_features.add(MarkdownSaveOptions.Features.LINK)

md_options.features = link_only_features
```

使用此配置运行转换后，会得到一个每行仅包含一个链接的 Markdown 文件，例如：



所有其他 HTML 元素均被过滤掉，只保留链接。

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每个资源均提供完整的可运行代码示例和逐步解释。

- [将 HTML 转换为 Markdown（Aspose.HTML for Java）](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [将 HTML 转换为 Markdown（.NET 版 Aspose.HTML）](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [如何使用 Aspose.HTML for Java 将 HTML 转换为 PDF（Java）](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}