---
category: general
date: 2026-10-18
description: 在 Python 中将 HTML 转换为 Markdown，并学习如何插入链接和段落，以生成干净的 Markdown 文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to include links
- save html as markdown
- how to convert html
- include links markdown
language: zh
lastmod: 2026-10-18
og_description: 在 Python 中将 HTML 转换为 Markdown，并了解如何在结构良好的 Markdown 文件中加入链接和段落。
og_image_alt: Screenshot of converted HTML to Markdown output showing links
og_title: 将 HTML 转换为带链接的 Markdown – Python 指南
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Convert HTML to Markdown in Python and learn how to include links and
    paragraphs for clean markdown files.
  headline: How to convert HTML to Markdown with links in Python
  type: TechArticle
- description: Convert HTML to Markdown in Python and learn how to include links and
    paragraphs for clean markdown files.
  name: How to convert HTML to Markdown with links in Python
  steps:
  - name: Expected output
    text: 'Assuming `sample.html` contains:'
  - name: Images
    text: 'Images are not covered by `MarkdownFeature.LINK`. If you also need to **include
      links markdown** for images, enable the `IMAGE` feature:'
  - name: Tables and code blocks
    text: The default conversion already maps `<table>` and `<pre>` tags to markdown
      tables and fenced code blocks. If you want tighter control, explore `MarkdownFeature.TABLE`
      and `MarkdownFeature.CODE_BLOCK`.
  - name: Encoding
    text: 'Make sure the source HTML is UTF‑8 encoded; otherwise you might see garbled
      characters in the markdown file. You can enforce UTF‑8 when reading the file:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
title: 如何在 Python 中将 HTML 转换为带链接的 Markdown
url: /zh/python/general/how-to-convert-html-to-markdown-with-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中将 HTML 转换为带链接的 Markdown

如果您需要快速 **将 HTML 转换为 Markdown**，本指南将向您展示在保留超链接和段落结构的情况下完成此操作的确切步骤。您还将了解 **如何包含链接**，使生成的 markdown 读取自然。  

在接下来的章节中，我们将涵盖从安装库到处理相对 URL 等边缘情况的所有内容。教程结束时，您只需几行代码即可 **将 HTML 保存为 Markdown**。

## 前置条件

在开始之前，请确保您拥有：

* 已安装 Python 3.8 或更高版本。
* 能够访问 `aspose.html` 包（示例使用 Aspose.HTML for Python，但任何提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 的库都可以类似使用）。
* 您想要转换的示例 HTML 文件（`sample.html`）。

您可以使用 pip 安装 Aspose.HTML 包：

```bash
pip install aspose-html
```

> **技巧提示：** 使用虚拟环境（`python -m venv venv`）来保持依赖隔离。

## 第一步：加载 HTML 文档

第一步是将源 HTML 文件读取到 `HTMLDocument` 对象中。该对象表示 DOM 树，并为转换器提供对页面内容的完整访问。

```python
from aspose.html import HTMLDocument

# Load the HTML document from the file system
doc = HTMLDocument("YOUR_DIRECTORY/sample.html")
```

*为什么这很重要：* 加载文档可确保所有元素——标题、表格、图像，尤其是链接——在转换前被正确解析。

## 第二步：配置 Markdown 保存选项以包含链接和段落

默认情况下，某些转换器可能会丢弃超链接或折叠段落标签。要在 markdown 输出中 **包含链接**，必须启用相应的功能。

```python
from aspose.html import MarkdownSaveOptions, MarkdownFeature

# Create save options and enable link and paragraph features
opt = MarkdownSaveOptions()
opt.features = MarkdownFeature.LINK | MarkdownFeature.PARAGRAPH
```

*解释：*
* `MarkdownFeature.LINK` 告诉转换器将 `<a>` 标签保留为 `[text](url)` 的 markdown 语法。
* `MarkdownFeature.PARAGRAPH` 将 `<p>` 元素保留为独立的行，防止句子连在一起。

## 第三步：将 HTML 文档转换为 Markdown 文件

现在调用静态的 `Converter.convert` 方法，传入已加载的文档、目标文件路径以及配置好的选项。

```python
from aspose.html import Converter

# Perform the conversion and write the markdown file
Converter.convert(doc, "YOUR_DIRECTORY/partial.md", opt)
```

运行此行后，`partial.md` 将包含 `sample.html` 的 markdown 表示，且所有链接保持完整。

## 完整可运行示例

将上述三步组合在一起即可得到一个可直接运行的简洁脚本：

```python
# convert_html_to_markdown.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

def convert_html_to_md(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown while preserving links and paragraphs.
    """
    # 1️⃣ Load the HTML document
    doc = HTMLDocument(source_path)

    # 2️⃣ Set conversion options (include links and paragraphs)
    opt = MarkdownSaveOptions()
    opt.features = MarkdownFeature.LINK | MarkdownFeature.PARAGRAPH

    # 3️⃣ Execute the conversion
    Converter.convert(doc, target_path, opt)

if __name__ == "__main__":
    # Example usage
    convert_html_to_md(
        source_path="YOUR_DIRECTORY/sample.html",
        target_path="YOUR_DIRECTORY/partial.md"
    )
```

### 预期输出

假设 `sample.html` 包含以下内容：

```html
<p>Visit the <a href="https://example.com">example site</a> for more info.</p>
```

生成的 `partial.md` 将如下所示：

```markdown
Visit the [example site](https://example.com) for more info.
```

请注意，链接已正确转换，段落保持在单独的行上。

## 如何在处理相对链接时转换 HTML

如果您的 HTML 使用相对 URL（例如 `<a href="/about">About</a>`），转换器会保持原样。若要在 markdown 中生成绝对 URL，您可以对文件进行后处理：

```python
import pathlib

def make_links_absolute(md_path: str, base_url: str) -> None:
    md_file = pathlib.Path(md_path)
    content = md_file.read_text(encoding="utf-8")
    # Replace markdown link patterns with absolute URLs
    updated = re.sub(r'\[([^\]]+)\]\((/[^)]+)\)', fr'[\1]({base_url}\2)', content)
    md_file.write_text(updated, encoding="utf-8")
```

在转换后运行 `make_links_absolute("YOUR_DIRECTORY/partial.md", "https://example.com")`，以确保所有链接指向正确的域名。

## 将 HTML 保存为 Markdown – 其他注意事项

### 图像

图像不受 `MarkdownFeature.LINK` 的覆盖。如果您还需要为图像 **包含链接 markdown**，请启用 `IMAGE` 功能：

```python
opt.features |= MarkdownFeature.IMAGE
```

### 表格和代码块

默认转换已经将 `<table>` 和 `<pre>` 标签映射为 markdown 表格和围栏代码块。如果您想要更精细的控制，可探索 `MarkdownFeature.TABLE` 和 `MarkdownFeature.CODE_BLOCK`。

### 编码

确保源 HTML 使用 UTF‑8 编码；否则您可能在 markdown 文件中看到乱码。读取文件时可以强制使用 UTF‑8：

```python
doc = HTMLDocument(open(source_path, "r", encoding="utf-8").read())
```

## 常见陷阱及其避免方法

| 症状 | 可能原因 | 解决方案 |
|------|----------|----------|
| Links disappear | `MarkdownFeature.LINK` not set | Add `opt.features = MarkdownFeature.LINK` |
| Paragraphs run together | `MarkdownFeature.PARAGRAPH` missing | Include `| MarkdownFeature.PARAGRAPH` |
| Images show as plain text | `MarkdownFeature.IMAGE` not enabled | Use `opt.features |= MarkdownFeature.IMAGE` |
| Relative URLs break in downstream tools | No post‑processing | Run `make_links_absolute` after conversion |

## 测试转换

您可以通过读取生成的 markdown 文件快速验证转换是否成功：

```python
with open("YOUR_DIRECTORY/partial.md", "r", encoding="utf-8") as f:
    print(f.read())
```

如果输出包含 markdown 链接语法（`[text](url)`）且段落分离，则您已成功 **将 html 保存为 markdown**。

## 结论

本教程演示了如何在 Python 中 **将 HTML 转换为 Markdown**，并明确说明了 **如何包含链接** 以及保留段落换行。通过配置 `MarkdownSaveOptions`，您可以对输出进行细粒度控制，从而轻松 **将 html 保存为 markdown**，用于文档、静态站点生成器或内容管道。

您可以进一步探索以下内容：

* 在生成的表格中 **包含链接 markdown**。
* 使用批处理脚本转换多个 HTML 文件。
* 将转换集成到静态站点构建流程中（例如使用 MkDocs 或 Jekyll）。

欢迎随意尝试这些选项，将其与后处理脚本结合，并根据项目需求调整工作流。祝您 markdown 写作愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方法。

- [如何使用 Aspose – 将 HTML 转换为 Markdown 并提取链接](/html/english/python/general/how-to-use-aspose-convert-html-to-markdown-and-extract-links/)
- [如何导出链接：使用 Aspose.Words 将 HTML 转换为 Markdown](/html/english/python/general/how-to-export-links-convert-html-to-markdown-with-aspose-wor/)
- [使用 Aspose 将 HTML 转换为 Markdown – 完整 Python 指南](/html/english/python/general/convert-html-to-markdown-with-aspose-complete-python-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}