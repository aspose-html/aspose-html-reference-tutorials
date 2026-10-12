---
category: general
date: 2026-10-12
description: 学习如何使用几行 Python 将 HTML 转换为 Markdown 并将 HTML 保存为 Markdown。包括导出 HTML 为
  Markdown 的技巧。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- save html as markdown
- export html to markdown
- convert html file md
language: zh
lastmod: 2026-10-12
og_description: 使用简单的 Python 脚本将 HTML 转换为 Markdown 并将 HTML 保存为 Markdown。请遵循本指南，获取可靠的
  HTML 转 Markdown 导出方案。
og_image_alt: Screenshot of Python code that converts HTML to Markdown
og_title: 在 Python 中将 HTML 转换为 Markdown – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-10-12'
  description: Learn how to convert HTML to Markdown and save HTML as Markdown using
    a few lines of Python. Includes export HTML to Markdown tips.
  headline: How to convert HTML to Markdown in Python – step‑by‑step guide
  type: TechArticle
tags:
- HTML conversion
- Markdown
- Python
- Aspose.HTML
title: 如何在 Python 中将 HTML 转换为 Markdown——一步步指南
url: /zh/python/general/how-to-convert-html-to-markdown-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中将 HTML 转换为 Markdown – 步骤指南

如果您需要**将 HTML 转换为 Markdown**，本教程将向您展示一个简洁、可用于生产的解决方案。无论是迁移博客、生成文档，还是构建静态站点流水线，您都可以仅用几行代码**将 HTML 导出为 Markdown**。

我们将演示如何加载 HTML 文件、配置转换选项，最后**将 HTML 保存为 Markdown**到磁盘。完成本指南后，您将拥有一个可复用的脚本，能够处理任何结构良好的 HTML 文档。

## 前置条件

在开始之前，请确保您具备以下条件：

* 已安装 Python 3.8 或更高版本。  
* 已安装 `aspose.html` 包（或任何提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 的兼容库）。使用以下方式安装：

```bash
pip install aspose-html
```

* 准备好要转换的 HTML 文件，例如放在可引用文件夹中的 `doc.html`。

> **小贴士：** 请确保您的 HTML 文件使用 UTF‑8 编码，以避免在转换过程中出现字符编码问题。

## 第 1 步：加载源 HTML 文档

第一步是将 HTML 文件读取为 `HTMLDocument` 对象。该对象让库能够访问 DOM、样式以及任何嵌入的资源。

```python
from aspose.html import HTMLDocument

# Replace YOUR_DIRECTORY with the actual path to your file
html_path = "YOUR_DIRECTORY/doc.html"
html_doc = HTMLDocument(html_path)
```

**为什么这很重要：** 加载文档将解析逻辑与文件系统分离，使转换器能够在内存中工作，避免部分读取或编码不匹配等副作用。

## 第 2 步：创建 Markdown 保存选项

`MarkdownSaveOptions` 让您可以细致地控制 Markdown 输出的生成方式。大多数场景下您会希望保留链接和段落，但以后也可以启用其他功能（表格、图片等）。

```python
from aspose.html import MarkdownSaveOptions

markdown_options = MarkdownSaveOptions()
```

> **边缘情况：** 如果源 HTML 包含自定义标签或脚本，可能需要通过设置 `markdown_options.ignore_unsupported = True` 来禁用它们，以防止转换错误。

## 第 3 步：启用所需的 Markdown 功能

这里我们打开两个最常用的功能：**链接**和**段落**。库使用位掩码枚举，因此我们使用按位或运算符 (`|`) 将标志组合起来。

```python
# Enable links and paragraphs in the output
markdown_options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

**为何要显式启用功能？** 显式的标志能够提供确定性的输出。如果以后需要**将 HTML 导出为 Markdown**并包含表格，只需在现有代码中添加 `MarkdownSaveOptions.Features.TABLE` 即可，无需修改其他部分。

## 第 4 步：将 HTML 转换为 Markdown 并保存结果

现在调用高级的 `Converter` 类。它读取 `HTMLDocument`，应用 `markdown_options`，并写入 `.md` 文件。

```python
from aspose.html import Converter

# Destination Markdown file
markdown_path = "YOUR_DIRECTORY/partial.md"

# Perform the conversion
Converter.convert_html(html_doc, markdown_options, markdown_path)
```

脚本执行完毕后，`partial.md` 将包含与原始 HTML 结构相匹配的干净 Markdown。

### 预期输出

如果 `doc.html` 包含：

```html
<h1>Welcome</h1>
<p>This is a <a href="https://example.com">sample link</a>.</p>
```

`partial.md` 将呈现为：

```markdown
# Welcome

This is a [sample link](https://example.com).
```

转换过程会保留标题层级、段落换行以及链接语法，这正是大多数文档流水线所期望的。

## 完整脚本（可直接复制粘贴）

将所有步骤整合后，下面的脚本即可直接运行：

```python
# convert_html_to_md.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def convert_html_to_markdown(html_path: str, markdown_path: str) -> None:
    """
    Loads an HTML file, configures Markdown options, and saves the result as .md.
    """
    # Load HTML
    html_doc = HTMLDocument(html_path)

    # Configure options
    options = MarkdownSaveOptions()
    options.features = (
        MarkdownSaveOptions.Features.LINK |
        MarkdownSaveOptions.Features.PARAGRAPH
    )

    # Convert and save
    Converter.convert_html(html_doc, options, markdown_path)

if __name__ == "__main__":
    # Example usage – adjust paths as needed
    src_html = "YOUR_DIRECTORY/doc.html"
    dst_md = "YOUR_DIRECTORY/partial.md"
    convert_html_to_markdown(src_html, dst_md)
    print(f"Conversion complete: '{src_html}' → '{dst_md}'")
```

在命令行中执行：

```bash
python convert_html_to_markdown.py
```

您应该会看到确认信息，Markdown 文件会出现在同一目录下。

## 常见变体与边缘情况处理

| 情况 | 调整 |
|-----------|------------|
| **HTML 包含表格** | 将 `MarkdownSaveOptions.Features.TABLE` 添加到位掩码中。 |
| **需要使用围栏代码块** | 包含 `MarkdownSaveOptions.Features.CODE_BLOCK`。 |
| **大文件（>10 MB）** | 若库支持，可使用 `HTMLDocument.open_stream()` 流式读取输入，以降低内存压力。 |
| **想保留内联 CSS** | 在转换前设置 `options.inline_css = True`（如果该选项存在）。 |
| **不同的输出文件夹** | 将任意绝对或相对路径传递给 `markdown_path`；转换器会在路径不存在时创建中间目录。 |

这些微调让您能够**将 HTML 保存为 Markdown**，并完全符合项目的具体需求。

## 测试转换

快速的完整性检查可以帮助您验证转换是否成功：

```python
def test_conversion():
    import pathlib
    src = "test.html"
    dst = "test.md"
    # Create a tiny HTML file for testing
    pathlib.Path(src).write_text("<h2>Test</h2><p>Hello <a href='https://a.com'>world</a></p>", encoding="utf-8")
    convert_html_to_markdown(src, dst)
    result = pathlib.Path(dst).read_text(encoding="utf-8")
    assert "# Test" in result
    assert "[world](https://a.com)" in result
    print("Test passed!")

test_conversion()
```

运行此测试会打印 **“Test passed!”**，确认核心转换逻辑按预期工作。

## 结论

现在您已经掌握了在 Python 中**将 HTML 转换为 Markdown**的完整流程，了解了如何配置转换选项，并能够**将 HTML 保存为 Markdown**以供后续处理。完整脚本展示了一种简洁、可复用的模式，您可以将其嵌入 CI 流水线、静态站点生成器或一次性迁移工具中。

接下来，您可以进一步探索：

* 使用额外功能（如表格、图片、脚注）**将 HTML 导出为 Markdown**。  
* 将脚本集成到 **GitHub Action** 中，实现 PR 合并时自动转换文档。  
* 使用相同的 `Converter` 类通过切换保存选项**将 HTML 导出为其他格式**（例如 PDF 或 DOCX）。

欢迎随意实验功能标志，并根据自己的工作流调整脚本。祝您转换愉快！

## 接下来应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 的其他功能，并在项目中探索替代实现方案。每篇资源都提供完整的可运行代码示例和逐步解释。

- [在 .NET 中使用 Aspose.HTML 将 HTML 转换为 Markdown](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Markdown 转 HTML（Java）— 使用 Aspose.HTML 进行转换](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}