---
category: general
date: 2026-11-24
description: 使用 GitLab 风格的选项在 Python 中将 HTML 转换为 Markdown，并轻松提取链接。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- save html as markdown
- html to markdown conversion
- extract links to markdown
language: zh
lastmod: 2026-11-24
og_description: 在 Python 中使用 GitLab 风格的选项将 HTML 转换为 Markdown，保存 HTML 为 Markdown，并提取链接到
  Markdown，附完整示例。
og_image_alt: Screenshot of a Python script converting HTML to GitLab‑flavored Markdown
og_title: 将 HTML 转换为 Markdown（GitLab 风格输出）– Python 指南
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Convert HTML to Markdown in Python using GitLab‑flavored options and
    extract links easily.
  headline: How to convert HTML to Markdown with GitLab‑flavored output in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Conversion
- GitLab
title: 如何在 Python 中将 HTML 转换为带 GitLab 风格输出的 Markdown
url: /zh/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 GitLab‑flavored 输出将 HTML 转换为 Markdown

如果您需要**将 HTML 转换为 Markdown**，本指南提供了一个完整、可直接运行的解决方案。您将看到如何使用 GitLab‑flavored 格式将 html 保存为 markdown，以及如何在不离开代码的情况下提取链接到 markdown。

该方法使用 Aspose.HTML for Python 库，该库提供单行转换 API 并可细粒度控制 Markdown 风格。教程结束时，您将拥有一个脚本，能够生成干净的 GitLab‑flavored markdown 文件并列出提取的链接。

## 前提条件

在开始之前，请确保您拥有：

* 已安装 Python 3.8 或更高版本。
* 可使用 `pip` 进行包安装。
* 本地 HTML 文件（例如 `article.html`），您想要转换。
* 基本了解如何在命令行运行 Python 脚本。

无需额外工具；库内部处理解析、转换和链接提取。

## 安装 Aspose.HTML for Python 库

转换 API 位于 `aspose.html` 包中。使用 `pip` 安装：

```bash
pip install aspose-html
```

该包捆绑了后续脚本中使用的 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 类。安装在几秒钟内完成，无需单独的运行时。

## 加载 HTML 文档

创建 `HTMLDocument` 对象会将源文件加载到内存中。构造函数接受文件路径或 URL。

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert.
doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

`doc` 实例现在代表完整的 DOM 树，使转换器能够读取每个元素，包括链接和段落标签。

## 配置 GitLab‑flavored Markdown 选项

GitLab‑flavored markdown 在处理链接和段落方面与标准 CommonMark 不同。`MarkdownSaveOptions` 类允许您指定格式化器和所需的功能集。

```python
from aspose.html import MarkdownSaveOptions

# Configure options for GitLab‑flavored output.
#   formatter="GIT"  -> GitLab markdown
#   features=["Link", "Paragraph"] -> keep only links and paragraphs.
opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])
```

将 `features` 设置为 `["Link", "Paragraph"]` 可确保转换专注于链接提取，同时保留段落结构，适用于文档或变更日志生成。

## 运行转换并保存为 Markdown

在文档已加载且选项已配置的情况下，调用静态 `Converter.convert` 方法。它会直接将结果写入目标文件。

```python
from aspose.html import Converter

# Perform the conversion and write the markdown file.
Converter.convert(doc, "YOUR_DIRECTORY/article.md", opts)
```

执行后，`article.md` 包含与原始 HTML 的链接和段落相匹配的 GitLab‑flavored markdown。

## 验证输出并提取链接到 markdown

打开生成的文件以确认转换。您应该看到链接语法（`[text](url)`）和与源匹配的段落换行。

```python
# Quick verification: read and print the first 10 lines.
with open("YOUR_DIRECTORY/article.md", "r", encoding="utf-8") as f:
    for i, line in enumerate(f):
        if i >= 10:
            break
        print(line.rstrip())
```

如果需要原始 URL 列表以进行进一步处理，可以在转换前从 `HTMLDocument` 中提取它们：

```python
# Extract all anchor href attributes.
links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
print("Extracted links:", links)
```

此步骤演示了使用已有 DOM **extract links to markdown**，避免二次解析。

## 完整脚本

将所有内容组合在一起即可得到一个可直接放入任何项目的单文件自包含脚本：

```python
# convert_html_to_gitlab_md.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def convert_html_to_markdown(src_path: str, dst_path: str) -> list:
    """
    Convert an HTML file to GitLab‑flavored Markdown and return a list of extracted links.

    Args:
        src_path: Path to the source HTML file.
        dst_path: Path where the Markdown file will be saved.

    Returns:
        A list of URLs found in the HTML document.
    """
    # Load the HTML document.
    doc = HTMLDocument(src_path)

    # Configure GitLab‑flavored Markdown options (links and paragraphs only).
    opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])

    # Convert and save as Markdown.
    Converter.convert(doc, dst_path, opts)

    # Extract links for additional processing.
    links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
    return links

if __name__ == "__main__":
    source = "YOUR_DIRECTORY/article.html"
    target = "YOUR_DIRECTORY/article.md"
    extracted_links = convert_html_to_markdown(source, target)

    print(f"Conversion complete. Markdown saved to {target}")
    print("Extracted links:", extracted_links)
```

运行脚本：

```bash
python convert_html_to_gitlab_md.py
```

会生成带有 GitLab‑flavored markdown 的 `article.md`，并打印提取的 URL 列表。

## 常见变体和边缘情况

| 场景                              | 调整                                                                 |
|-----------------------------------|----------------------------------------------------------------------|
| **完整 HTML（图像、表格等）**      | 将 `"Image"` 或 `"Table"` 添加到 `features` 以保留这些元素。       |
| **不同的 Markdown 风格**          | 将 `formatter="GIT"` 更改为 `"COMMONMARK"` 或 `"GFM"` 以适用于其他平台。 |
| **大文件（> 50 MB）**              | 使用流式 API（`HTMLDocument.open`）以避免加载整个文件。           |
| **Unicode 字符**                  | 确保源文件为 UTF‑8 编码；库会保留编码。                           |

这些变体让您能够在许多场景下复用相同模式来 **save html as markdown**。

## 专业技巧

* **复用选项：** 创建单个 `MarkdownSaveOptions` 实例，并在批量作业中转换多个文件时传递它。
* **验证链接：** 提取后，运行简单的 `requests.head(url)` 检查以标记失效的 URL。
* **版本锁定：** 固定 Aspose.HTML 版本 (`aspose-html==23.10`) 以避免意外的 API 更改。

## 结论

您现在已经了解如何使用 GitLab‑flavored 格式化器 **convert HTML to markdown**，save html as markdown，并使用简洁的 Python 脚本 **extract links to markdown**。该解决方案开箱即用，能够处理常见边缘情况，并可扩展至其他 Markdown 风格或额外的 HTML 功能。

### 接下来的步骤

* 探索 `features` 列表，以包含图像、表格或代码块。
* 将此脚本集成到 CI 流水线中，以自动从 HTML 源生成文档。
* 将提取的链接与链接检查服务结合，以维护健康的引用。

欢迎根据自己的工作流调整脚本，并与社区分享您的成果！

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方式。

- [将 HTML 转换为 Markdown Python – 提取链接和段落](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [如何在 Python 中使用 GitLab‑flavored markdown 将 HTML 转换为 Markdown](/html/english/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-markdow/)
- [将 HTML 转换为 Markdown Python – 使用 Python 保存 Markdown 文件](/html/english/python/general/convert-html-to-markdown-python-save-markdown-file-with-pyth/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}