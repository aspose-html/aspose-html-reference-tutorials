---
category: general
date: 2026-10-12
description: 快速将HTML转换为Markdown，并学习如何在Markdown中嵌入图片。本指南详细演示使用Python进行HTML到Markdown的转换，并提供完整代码。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to embed images in markdown
- html to markdown conversion python
- how to convert html page to markdown
language: zh
lastmod: 2026-10-12
og_description: 使用 Python 将 HTML 转换为 Markdown 并在 Markdown 中嵌入图片。请遵循本完整教程，实现可靠的 HTML
  转 Markdown 转换（Python）。
og_image_alt: Screenshot showing a Python script that converts an HTML file to a markdown
  file with base64‑encoded images
og_title: 在 Python 中将 HTML 转换为带嵌入图片的 Markdown – 步骤指南
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: convert HTML to markdown quickly and learn how to embed images in markdown.
    This guide walks through html to markdown conversion python with full code.
  headline: How to convert HTML to markdown with embedded images using Python
  type: TechArticle
tags:
- markdown
- html
- python
- document conversion
title: 如何使用 Python 将 HTML 转换为带嵌入图像的 Markdown
url: /zh/python/general/how-to-convert-html-to-markdown-with-embedded-images-using-p/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 将 HTML 转换为带嵌入图像的 Markdown

如果您需要在**将 HTML 转换为 markdown**的同时保留所有图像，本指南将准确展示如何操作。通过将转换引擎配置为以 Base64 形式嵌入图像，您可以得到一个单一的、独立的 `.md` 文件，可在任何地方使用——从 GitHub README 到静态站点生成器。

您还将学习**如何在 markdown 中嵌入图像**，了解内置资源处理选项为何是最可靠的选择，以及如何仅用几行代码完成**html to markdown conversion python**。

## 您将实现的目标

- 将任意本地 HTML 页面转换为干净的 Markdown 文档。  
- 将每个图像直接嵌入 Markdown 文件，作为 Base64 字符串，消除断链。  
- 在任何支持 Python 3.9+ 和 GroupDocs Conversion 库的平台上运行此过程。  

## 前置条件

| 需求 | 原因 |
|------------|--------|
| Python 3.9 或更高版本 | GroupDocs Conversion SDK 所需。 |
| `groupdocs-conversion` package | 提供 `Converter`、`HTMLDocument`、`MarkdownSaveOptions` 和 `ResourceHandlingOptions`。 |
| 已有的 HTML 文件（例如 `page.html`） | 您想要转换的源文件。 |
| 对输出文件夹的写入权限 | 用于保存生成的 `.md` 文件。 |

Install the SDK with pip:

```bash
pip install groupdocs-conversion
```

> **技巧提示：** 使用虚拟环境（`python -m venv .venv`）来保持依赖隔离。

## 步骤 1：配置资源处理以在 markdown 中嵌入图像

当转换引擎遇到 `<img>` 标签时，它可以将图像复制到单独的文件夹，或直接嵌入。嵌入会生成 Base64 编码的 data URI，这正是**how to embed images in markdown**所需的。

```python
from groupdocs.conversion import ResourceHandlingOptions

# Create a resource handling configuration
resource_options = ResourceHandlingOptions()
# Enable embedding of images as Base64 data URIs
resource_options.embed_images = True   # Embeds images directly in the Markdown file
```

**为什么这很重要：**  
嵌入确保 Markdown 文件保持可移植性。如果您共享 `.md` 文件而不附带图像文件夹，图像仍会在任何支持 data URI 的平台上正确渲染（GitHub、GitLab、VS Code 预览等）。

## 步骤 2：使用资源配置设置 Markdown 保存选项

`MarkdownSaveOptions` 类允许您传入上述创建的 `resource_options`。它还可以微调换行符、标题样式等，但在大多数情况下默认设置已足够。

```python
from groupdocs.conversion import MarkdownSaveOptions

# Attach the resource handling to the markdown save options
markdown_options = MarkdownSaveOptions(resource_handling_options=resource_options)
```

**内部工作原理：**  
在转换过程中，引擎会扫描 HTML DOM，将每个元素转换为对应的 Markdown，并将 `<img src="...">` 替换为 `![alt text](data:image/...;base64,...)`。`resource_options.embed_images` 标志会触发此行为。

## 步骤 3：将 HTML 文档转换为 markdown 并保存结果

现在将所有步骤串联起来：加载源 HTML，应用保存选项，并写入输出文件。

```python
from groupdocs.conversion import Converter, HTMLDocument

# Path to the source HTML file
source_path = "YOUR_DIRECTORY/page.html"
# Desired output path for the markdown file
output_path = "YOUR_DIRECTORY/page.md"

# Perform the conversion
Converter.convert_html(
    HTMLDocument(source_path),
    markdown_options,
    output_path
)

print(f"✅ Conversion complete! Markdown saved to: {output_path}")
```

**预期输出：**  

- `page.md` 包含 Markdown 文本、标题、列表以及作为 Base64 字符串的**嵌入图像**。  
- 在 Markdown 查看器中打开 `page.md`，会显示原始 HTML 布局，包括所有图像，无需任何外部资源。

### 完整脚本，快速复制粘贴

```python
# convert_html_to_markdown.py
from groupdocs.conversion import (
    Converter,
    HTMLDocument,
    MarkdownSaveOptions,
    ResourceHandlingOptions,
)

def convert_html_to_markdown(src_html: str, dst_md: str) -> None:
    """Convert an HTML file to markdown with images embedded as Base64."""
    # 1️⃣ Embed images
    resource_opts = ResourceHandlingOptions()
    resource_opts.embed_images = True

    # 2️⃣ Prepare markdown options
    md_opts = MarkdownSaveOptions(resource_handling_options=resource_opts)

    # 3️⃣ Run conversion
    Converter.convert_html(
        HTMLDocument(src_html),
        md_opts,
        dst_md
    )
    print(f"✅ Markdown file created at: {dst_md}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    convert_html_to_markdown(
        src_html="YOUR_DIRECTORY/page.html",
        dst_md="YOUR_DIRECTORY/page.md"
    )
```

运行脚本：

```bash
python convert_html_to_markdown.py
```

## 处理常见边缘情况

| 情况 | 解决方案 |
|-----------|----------|
| **大图像导致 markdown 文件体积过大** | 在嵌入之前通过在 HTML 中调整大小或使用图像优化库（如 Pillow）来限制图像尺寸。 |
| **相对图像 URL 指向项目外部** | 确保 HTML 引用可访问，或在转换前将这些图像复制到同一文件夹。 |
| **您需要将图像保存为单独文件而非嵌入** | 将 `resource_options.embed_images = False`，并提供用于保存图像的 `resource_folder` 路径。 |
| **转换在错误的 HTML 上失败** | 使用 `BeautifulSoup`（`html5lib` 解析器）预处理 HTML，清理破损标签后再交给转换器。 |

## 验证结果

在任意 Markdown 查看器中打开生成的 `page.md`：

```bash
code YOUR_DIRECTORY/page.md   # VS Code preview
```

您应该能看到原始的标题、段落和图像正确渲染。如果某个图像显示为断链，请再次确认 `embed_images` 已设置为 `True`，且源 HTML 包含有效的 `<img>` 标签。

## 后续步骤及相关主题

- **导出为其他格式** —— 同一个 `Converter` 类可以生成 PDF、DOCX 或纯文本。将 `MarkdownSaveOptions` 替换为 `PdfSaveOptions` 或 `DocxSaveOptions`。  
- **批量处理** —— 遍历 HTML 文件目录，生成一系列 Markdown 文档。  
- **自定义图像处理** —— 通过 `ResourceHandlingOptions` 实现回调，将图像存储到 CDN 并用 CDN URL 替换 data URI。  
- **高级 markdown 功能** —— 通过调整 `markdown_options` 属性启用 GitHub 风格的 markdown（表格、任务列表）。  

通过掌握 **html to markdown conversion python**，您现在拥有可重复、可投入生产的工作流，确保图像随内容一起保留。欢迎尝试上述选项，并将脚本适配到您自己的内容管道中。

---


## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [在 .NET 中使用 Aspose.HTML 将 HTML 转换为 Markdown](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [使用 Aspose HTML Converter (Java) 从 Markdown 创建 PDF](/html/english/java/conversion-html-to-other-formats/create-pdf-from-markdown-using-aspose-html-converter-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}