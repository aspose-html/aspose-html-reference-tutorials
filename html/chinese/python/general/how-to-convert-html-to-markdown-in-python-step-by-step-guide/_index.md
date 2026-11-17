---
category: general
date: 2026-11-17
description: 使用 Python 的 MarkdownSaveOptions 将 HTML 转换为 Markdown。了解如何将 HTML 保存为 Markdown，定制功能，并执行完整的
  HTML 到 Markdown 转换。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- save html as markdown
- html to markdown conversion
- how to convert html
- python html to markdown
language: zh
lastmod: 2026-11-17
og_description: 使用 MarkdownSaveOptions 将 HTML 转换为 Markdown（Python）。本教程展示了如何将 HTML
  保存为 Markdown，并涵盖所有转换选项。
og_image_alt: Screenshot of Python script converting an HTML file to a Markdown file
og_title: 在 Python 中将 HTML 转换为 Markdown – 完整指南
schemas:
- author: GroupDocs
  dateModified: '2026-11-17'
  description: Convert HTML to Markdown with Python using MarkdownSaveOptions. Learn
    how to save HTML as markdown, customize features, and run a full HTML to markdown
    conversion.
  headline: How to convert HTML to Markdown in Python – step‑by‑step guide
  type: TechArticle
tags:
- python
- markdown
- html
- conversion
title: 如何在 Python 中将 HTML 转换为 Markdown——一步一步的指南
url: /zh/python/general/how-to-convert-html-to-markdown-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中将 HTML 转换为 Markdown – 步骤指南

如果您需要 **将 HTML 转换为 Markdown**，本教程提供了一个可直接运行的 Python 脚本，能够完成此操作。您将看到如何 **将 HTML 保存为 markdown** 并进行细粒度的功能控制，使输出符合您的文档风格。

我们将逐步讲解整个过程：安装所需包、配置 `MarkdownSaveOptions`、运行转换以及验证结果。完成后，您只需一次函数调用即可对任意文件执行 **HTML 到 markdown 的转换**。

## 前置条件

在开始之前，请确保您具备以下条件：

* 已安装 Python 3.8 或更高版本。
* 拥有终端或命令提示符的访问权限。
* 已安装提供 `MarkdownSaveOptions`、`Converter` 和 `HTMLDocument` 的 `groupdocs-conversion`（或类似）包。  
  使用以下命令进行安装：

```bash
pip install groupdocs-conversion
```

> **专业提示：** 如果您在虚拟环境中工作，请先激活该环境，以免影响系统范围的包。

## 第一步：导入所需类

转换 API 位于 `groupdocs.conversion` 命名空间。导入您将使用的类：

```python
from groupdocs.conversion import Converter, HTMLDocument, MarkdownSaveOptions
```

这些导入让您能够使用 `Converter.convert` 方法、`HTMLDocument` 包装器以及 `MarkdownSaveOptions` 对象，从而 **将 HTML 保存为 markdown** 并自定义功能。

## 第二步：创建 Markdown 保存选项并选择所需功能

`MarkdownSaveOptions` 允许您启用或禁用特定的 Markdown 元素。在本示例中，我们保留标题、链接和段落——这些是大多数文档的常用构建块。

```python
# Step 2: Create Markdown save options and select the desired features
markdown_options = MarkdownSaveOptions()
markdown_options.features = (
    MarkdownSaveOptions.Feature.HEADER |
    MarkdownSaveOptions.Feature.LINK |
    MarkdownSaveOptions.Feature.PARAGRAPH
)
```

*为何重要：*  
仅启用所需功能可以减少输出噪声并加快 **html to markdown conversion**。例如，如果您不想要表格，只需省略 `MarkdownSaveOptions.Feature.TABLE`。

## 第三步：准备源 HTML 文档

将 `HTMLDocument` 构造函数指向您想要转换的文件。将 `YOUR_DIRECTORY/sample.html` 替换为实际的 HTML 文件路径。

```python
# Step 3: Load the source HTML file
source_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(source_path)
```

`HTMLDocument` 对象会读取文件、解析 DOM，并为转换引擎做好准备。

## 第四步：运行转换

现在调用 `Converter.convert`，传入 `HTMLDocument`、目标 Markdown 文件路径以及您配置的选项。

```python
# Step 4: Convert the HTML file to Markdown using the configured options
target_path = "YOUR_DIRECTORY/sample.md"
Converter.convert(html_doc, target_path, markdown_options)
print(f"Conversion complete: '{source_path}' → '{target_path}'")
```

该方法会生成一个遵循所选功能的 Markdown 文件。如果转换失败，会抛出带有详细信息的异常——在生产代码中请使用 try/except 块进行处理。

## 第五步：验证输出

在任意文本编辑器或 Markdown 查看器中打开生成的 `sample.md` 文件。您应当看到：

```markdown
# Sample Heading

This is a paragraph with a [link](https://example.com).

```

请注意，仅出现标题、链接和段落，因为我们已将转换限制在这些功能上。如需额外元素，请相应调整 `markdown_options.features`。

## 如何使用额外选项进行 HTML 转换

有时您希望保留图像、表格或代码块。可以这样扩展功能掩码：

```python
markdown_options.features = (
    MarkdownSaveOptions.Feature.HEADER |
    MarkdownSaveOptions.Feature.LINK |
    MarkdownSaveOptions.Feature.PARAGRAPH |
    MarkdownSaveOptions.Feature.IMAGE |
    MarkdownSaveOptions.Feature.TABLE |
    MarkdownSaveOptions.Feature.CODE_BLOCK
)
```

使用扩展后的掩码运行相同的转换，将实现更全面的 **html to markdown conversion**，并保留额外元素。

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|-------|----------------|-----|
| **缺少包** | `ImportError`，因为未安装 `groupdocs-conversion`。 | 在正确的环境中运行 `pip install groupdocs-conversion`。 |
| **文件路径错误** | `FileNotFoundError`，源 HTML 路径不正确。 | 使用绝对路径或确认相对于脚本工作目录的相对路径。 |
| **不受支持的 HTML 标签** | 某些全新的 HTML5 标签未映射到 Markdown。 | 在自动化步骤后手动转换这些部分，或添加自定义后处理器。 |

## 完整脚本 – 可直接复制运行

```python
"""
convert_html_to_markdown.py

A complete example that converts an HTML file to Markdown using
MarkdownSaveOptions. Adjust the feature mask to include or exclude
specific Markdown elements.
"""

from groupdocs.conversion import Converter, HTMLDocument, MarkdownSaveOptions

def convert_html_to_md(source_html: str, target_md: str, features: int) -> None:
    """Convert an HTML file to Markdown with the given feature mask."""
    # Create and configure save options
    md_options = MarkdownSaveOptions()
    md_options.features = features

    # Load the HTML document
    html_doc = HTMLDocument(source_html)

    # Perform the conversion
    Converter.convert(html_doc, target_md, md_options)
    print(f"Conversion complete: '{source_html}' → '{target_md}'")

if __name__ == "__main__":
    # Paths – replace with your own locations
    src = "YOUR_DIRECTORY/sample.html"
    dst = "YOUR_DIRECTORY/sample.md"

    # Choose which Markdown features to keep
    selected_features = (
        MarkdownSaveOptions.Feature.HEADER |
        MarkdownSaveOptions.Feature.LINK |
        MarkdownSaveOptions.Feature.PARAGRAPH
    )

    convert_html_to_md(src, dst, selected_features)
```

运行此脚本即可得到干净的 **HTML to markdown conversion**，可供静态站点生成器、文档流水线或任何支持 Markdown 的工具使用。

## 结论

现在您已经掌握了如何在 Python 中 **将 HTML 转换为 Markdown**，以及如何使用自定义功能选择 **将 HTML 保存为 markdown**，并了解如何扩展该过程以处理更复杂的文档。这种方法为您提供了一种可靠、可编程的方式来执行 **html to markdown conversion**，无需手动复制粘贴。

接下来，尝试通过遍历目录批量转换文件，或将该函数集成到 CI/CD 流水线中，实现从 HTML 报告自动生成文档。若需更深度的定制，可探索 `MarkdownSaveOptions` 的其他标志，如 `IMAGE`、`TABLE` 和 `CODE_BLOCK`。

祝转换愉快！


## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您在自己的项目中进一步掌握 API 功能并探索替代实现方式。每个资源都包含完整的可运行代码示例和逐步解释。

- [How to Use Aspose to Convert HTML to Markdown in Python – Complete Guide](/html/english/python/general/how-to-use-aspose-to-convert-html-to-markdown-in-python-comp/)
- [Convert HTML to Markdown in Python – save HTML as Markdown with Aspose.HTML](/html/english/python/general/convert-html-to-markdown-in-python-save-html-as-markdown-wit/)
- [How to embed images in HTML to Markdown conversion using Python](/html/english/python/general/how-to-embed-images-in-html-to-markdown-conversion-using-pyt/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}