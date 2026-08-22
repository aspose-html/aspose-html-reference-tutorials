---
category: general
date: 2026-08-22
description: 如何从HTML导出链接并转换为Markdown文件，包括段落。HTML转Markdown的分步指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export links
- convert html to markdown
- how to convert html
- how to extract paragraphs
- html to markdown file
language: zh
lastmod: 2026-08-22
og_description: 如何从HTML文档中导出链接并转换为Markdown文件，包括段落。请遵循本完整教程，实现可靠的HTML到Markdown转换。
og_image_alt: How to export links while converting HTML to Markdown
og_title: 在将HTML转换为Markdown时如何导出链接——分步指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-22'
  description: How to export links from HTML and convert it to a markdown file, including
    paragraphs. Step‑by‑step guide for HTML to markdown conversion.
  headline: How to export links while converting HTML to Markdown
  type: TechArticle
tags:
- HTML conversion
- Markdown
- Python
title: 在将HTML转换为Markdown时如何导出链接
url: /zh/python/general/how-to-export-links-while-converting-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在将 HTML 转换为 Markdown 时导出链接

如果您需要 **how to export links** 从 HTML 页面并将结果转换为干净的 **html to markdown file**，本指南向您展示具体步骤。您还将发现 **how to extract paragraphs**，以便 markdown 输出包含您关心的主要内容。教程结束时，您可以使用即用即跑的脚本回答 “**how to convert html** to markdown” 这一问题。

在将网页内容迁移到静态站点、文档门户或无头 CMS 后端时，导出链接和提取段落是常见任务。下面的方法适用于 GroupDocs Conversion SDK for Python，但其概念同样适用于任何允许配置导出功能的库。

---

## 您需要的环境

- Python 3.9 或更高版本  
- `groupdocs-conversion` 包（使用 `pip install groupdocs-conversion` 安装）  
- 您想要处理的 HTML 文件（例如 `input.html`）  
- 对 Python 脚本有基本了解  

---

## 使用 HTML 转 Markdown 转换导出链接的方法

第一步是配置转换，使得仅将所需的特性——链接和段落——写入 **html to markdown file**。SDK 允许您设置 `MarkdownFeature` 值的位掩码；我们将 `LINKS` 和 `PARAGRAPHS` 组合，以保持输出的聚焦。

```python
# Import the required classes from the GroupDocs Conversion SDK
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/input.html")

# Step 2: Create Markdown save options and select the features to export
markdown_options = MarkdownSaveOptions()
# Export only links and paragraphs from the HTML
markdown_options.features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

# Step 3: Convert the HTML to Markdown using the configured options
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)

print(f"Conversion complete. Markdown saved to {output_path}")
```

### 为什么这样有效

- **`HTMLDocument`** 解析原始文件并构建一个转换器可以遍历的 DOM。  
- **`MarkdownSaveOptions`** 为您提供对 SDK 写入内容的细粒度控制。将 `features` 设置为 `LINKS | PARAGRAPHS` 告诉引擎忽略图片、表格或脚本，从而降低最终 **html to markdown file** 中的噪声。  
- **`Converter.convert`** 执行繁重的转换工作。它遵循特性掩码，提取锚点标签（`<a>`）和段落标签（`<p>`），并使用标准的 Markdown 语法写入。  

---

## 将 HTML 完全转换为 Markdown（可选）

如果您之后决定需要整个页面——而不仅是链接和段落——只需调整特性掩码：

```python
# Export everything the SDK supports (links, paragraphs, images, tables, etc.)
markdown_options.features = MarkdownFeature.ALL
```

现在运行相同的转换会生成完整的 **html to markdown file**，其布局与原始页面相匹配。这展示了以灵活方式 **how to convert html**：您可以通过切换特性标志来控制输出。

---

## 仅提取段落

有时您只关心文章的文本内容，而不是超链接。您可以通过将掩码仅设置为 `PARAGRAPHS` 来单独提取段落：

```python
markdown_options.features = MarkdownFeature.PARAGRAPHS
output_path = "YOUR_DIRECTORY/only_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)
```

生成的 markdown 将包含干净、换行的文本，不含任何链接标记。此代码片段回答了 **how to extract paragraphs** 从 HTML 源中提取段落的问题。

---

## 常见陷阱及规避方法

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Empty output file | 源 HTML 中没有匹配所选特性的 `<a>` 或 `<p>` 标签。 | 检查 HTML 结构或扩大特性掩码（例如，包含 `HEADINGS`）。 |
| Encoding problems | HTML 使用非 UTF‑8 编码，导致 SDK 读取错误。 | 为 `HTMLDocument` 传递显式编码，例如 `HTMLDocument(path, encoding="iso-8859-1")`。 |
| Over‑writing existing markdown | 多次运行脚本会覆盖之前的文件。 | 为输出文件名添加时间戳，或在写入前检查 `os.path.exists`。 |

**Pro tip:** 在处理文件夹中的大量文件时，将转换逻辑包装在循环中并记录每个结果。这能为您提供清晰的审计轨迹，并在失败后轻松恢复。

---

## 完整脚本，复制粘贴即可使用

下面是一个独立的 Python 文件（`convert_links_paragraphs.py`），您可以直接运行。它包含参数解析，您可以在不修改代码的情况下指定输入和输出路径。

```python
#!/usr/bin/env python3
"""
convert_links_paragraphs.py

A complete example that shows how to export links and extract paragraphs
when converting HTML to a markdown file using GroupDocs Conversion SDK.
"""

import argparse
import os
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

def convert_html_to_md(input_html: str, output_md: str, features: int) -> None:
    """Perform the conversion with the given feature mask."""
    if not os.path.isfile(input_html):
        raise FileNotFoundError(f"Input file not found: {input_html}")

    # Load the HTML document
    html_doc = HTMLDocument(input_html)

    # Configure markdown options
    md_options = MarkdownSaveOptions()
    md_options.features = features

    # Run the conversion
    Converter.convert(html_doc, md_options, output_md)
    print(f"✅ Conversion finished – markdown saved to: {output_md}")

def main() -> None:
    parser = argparse.ArgumentParser(
        description="How to export links while converting HTML to Markdown."
    )
    parser.add_argument("input", help="Path to the source HTML file.")
    parser.add_argument(
        "output",
        help="Path for the resulting markdown file (e.g., links_and_paragraphs.md).",
    )
    parser.add_argument(
        "--links",
        action="store_true",
        help="Include links in the markdown output.",
    )
    parser.add_argument(
        "--paragraphs",
        action="store_true",
        help="Include paragraphs in the markdown output.",
    )
    args = parser.parse_args()

    # Build the feature mask based on user flags
    selected_features = 0
    if args.links:
        selected_features |= MarkdownFeature.LINKS
    if args.paragraphs:
        selected_features |= MarkdownFeature.PARAGRAPHS

    # Default to both links and paragraphs if no flag is provided
    if selected_features == 0:
        selected_features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

    try:
        convert_html_to_md(args.input, args.output, selected_features)
    except Exception as exc:
        print(f"❌ Conversion failed: {exc}")

if __name__ == "__main__":
    main()
```

**如何运行**

```bash
python convert_links_paragraphs.py YOUR_DIRECTORY/input.html YOUR_DIRECTORY/links_and_paragraphs.md --links --paragraphs
```

上述命令演示了在一次调用中 **how to export links** 和 **how to extract paragraphs**。省略 `--links` 或 `--paragraphs` 可根据需求定制输出。

---

## 验证 – 输出示例

给定以下简单的 HTML（`input.html`）：

```html
<!DOCTYPE html>
<html>
<head><title>Sample page</title></head>
<body>
  <p>Welcome to the tutorial.</p>
  <p>Visit <a href="https://example.com">our site</a> for more info.</p>
</body>
</html>
```

使用两个标志运行脚本会生成 `links_and_paragraphs.md`：

```markdown
Welcome to the tutorial.

Visit [our site](https://example.com) for more info.
```

您可以看到仅包含两个段落和超链接——正是您在搜索 **how to export links** 并执行 **convert html to markdown** 时所期望的结果。

---

## 后续步骤及相关主题

- **How to convert html to markdown**（包含图片）：在掩码中添加 `MarkdownFeature.IMAGES`。  
- **How to extract paragraphs** 并随后进行后处理  

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [Convert HTML to Markdown – Complete C# Guide](/html/english/java/conversion-html-to-other-formats/convert-html-to-markdown-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}