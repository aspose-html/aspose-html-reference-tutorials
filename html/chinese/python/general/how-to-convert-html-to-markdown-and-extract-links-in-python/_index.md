---
category: general
date: 2026-10-28
description: 使用 Python 将 HTML 转换为 Markdown：学习如何从 HTML 中提取链接，并仅用三步将其保存为 GitLab 风格的
  Markdown。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- how to convert html document
language: zh
lastmod: 2026-10-28
og_description: 使用 Python 快速将 HTML 转换为 Markdown。本指南展示了如何从 HTML 中提取链接，并在三个简单步骤中生成 GitLab
  风格的 Markdown。
og_image_alt: Screenshot of Python script converting HTML to GitLab‑flavored Markdown
  with extracted links
og_title: 使用 Python 将 HTML 转换为 Markdown 并提取链接
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: 'convert html to markdown using Python: learn to extract links from
    HTML and save as GitLab‑flavored Markdown in just three steps.'
  headline: How to convert HTML to Markdown and extract links in Python
  type: TechArticle
- description: 'convert html to markdown using Python: learn to extract links from
    HTML and save as GitLab‑flavored Markdown in just three steps.'
  name: How to convert HTML to Markdown and extract links in Python
  steps:
  - name: Multiple input sources
    text: 'If you need to batch‑process a folder of HTML files, wrap the conversion
      in a loop:'
  - name: Missing links
    text: When an HTML document contains no `<a>` elements, the converter still creates
      a valid Markdown file containing only the permitted paragraphs. No additional
      error handling is required, but you can check `save_options.features` if you
      need to enforce the presence of links.
  - name: Custom output encoding
    text: 'If your target system expects UTF‑8 with a BOM, set the encoding on the
      `MarkdownSaveOptions`:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Conversion
title: 如何在 Python 中将 HTML 转换为 Markdown 并提取链接
url: /zh/python/general/how-to-convert-html-to-markdown-and-extract-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中将 HTML 转换为 Markdown 并提取链接

如果你需要 **将 HTML 转换为 Markdown**，本教程提供了一个完整、可直接运行的解决方案。你将看到如何从 HTML 中提取链接、选择 GitLab 风格的 Markdown 格式化器，以及仅用几行代码保存结果。

本指南涵盖了你所需的一切：必备的包、从不同来源加载 HTML、配置 `MarkdownSaveOptions`，以及处理缺失链接或自定义输出目录等边缘情况。完成后，你将能够回答 *如何将 HTML 文档* 转换为干净、富含链接的 Markdown，以供后续工作流使用。

## 前置条件

- Python 3.8 或更高版本
- `aspose-html` 包（官方的 Aspose.HTML Python 库）
- 对 Python 脚本和文件 I/O 有基本了解

你可以使用以下命令安装该库：

```bash
pip install aspose-html
```

> **小贴士：** 使用虚拟环境来保持依赖的隔离。

## 第一步：加载 HTML 内容

第一步是创建一个 `HTMLDocument` 对象。Aspose.HTML 接受字符串、文件路径或 URL，因此你可以选择最适合项目的来源。

```python
from aspose.html import HTMLDocument

# Example 1: Load from a raw HTML string
html_string = "<h1>Title</h1><p>Sample <a href='https://example.com'>link</a></p>"
html_doc = HTMLDocument(html_string)

# Example 2: Load from a local file
# html_doc = HTMLDocument("input.html")

# Example 3: Load from a remote URL
# html_doc = HTMLDocument("https://www.example.com")
```

> **为什么重要：** 只加载一次文档即可得到一个类似 DOM 的对象，转换器可以遍历它，确保所有链接和段落节点都可被提取。

## 第二步：配置 Markdown 保存选项

`MarkdownSaveOptions` 让你可以控制输出格式以及哪些 HTML 特性会被转换。要 **从 HTML 中提取链接** 并保留段落，请启用 `LINK` 和 `PARAGRAPH` 特性，并选择 GitLab 格式化器。

```python
from aspose.html import MarkdownSaveOptions

save_options = MarkdownSaveOptions()
# Use GitLab‑flavored Markdown (supports task lists, tables, etc.)
save_options.formatter = MarkdownSaveOptions.Formatter.GIT

# Export only links and paragraphs – other tags (e.g., images) are ignored
save_options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

> **为什么重要：** 限制特性可以减少输出噪声，并保证生成的 Markdown 只包含你关心的元素——这对文档流水线或静态站点生成器非常理想。

## 第三步：转换 HTML 文档并写入文件

现在调用 `Converter.convert_html`，传入文档、选项和目标路径。

```python
from aspose.html import Converter

output_path = "output.md"  # Change to your desired directory/file name
Converter.convert_html(html_doc, save_options, output_path)
print(f"Markdown file saved to {output_path}")
```

运行脚本后会生成一个 `output.md` 文件，内容如下：

```markdown
# Title

Sample [link](https://example.com)
```

可以看到，仅出现了标题、段落和链接——这正是我们在配置 `save_options` 时所要求的。

## 处理常见变体和边缘情况

### 多种输入来源

如果需要批量处理文件夹中的 HTML 文件，可将转换包装在循环中：

```python
import pathlib
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

input_folder = pathlib.Path("html_inputs")
output_folder = pathlib.Path("markdown_outputs")
output_folder.mkdir(exist_ok=True)

options = MarkdownSaveOptions()
options.formatter = MarkdownSaveOptions.Formatter.GIT
options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)

for html_path in input_folder.glob("*.html"):
    doc = HTMLDocument(str(html_path))
    md_path = output_folder / (html_path.stem + ".md")
    Converter.convert_html(doc, options, str(md_path))
    print(f"Converted {html_path.name} → {md_path.name}")
```

### 缺失链接

当 HTML 文档中没有 `<a>` 元素时，转换器仍会生成一个仅包含允许的段落的有效 Markdown 文件。无需额外的错误处理，但如果需要强制检查链接是否存在，可查看 `save_options.features`。

### 自定义输出编码

如果目标系统要求 UTF‑8 带 BOM，可在 `MarkdownSaveOptions` 上设置编码：

```python
save_options.encoding = "utf-8-sig"
```

## 完整、可运行的示例

将所有内容组合在一起，下面是一个可直接复制粘贴并立即运行的脚本：

```python
# convert_html_to_markdown.py
# -------------------------------------------------
# Demonstrates how to convert HTML to Markdown while
# extracting only links and paragraphs using Aspose.HTML.
# -------------------------------------------------

from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def main():
    # 1️⃣ Load HTML – replace this with your own source if needed
    html = "<h1>Title</h1><p>Sample <a href='https://example.com'>link</a></p>"
    document = HTMLDocument(html)

    # 2️⃣ Configure Markdown options (GitLab flavor, links + paragraphs only)
    options = MarkdownSaveOptions()
    options.formatter = MarkdownSaveOptions.Formatter.GIT
    options.features = (
        MarkdownSaveOptions.Features.LINK |
        MarkdownSaveOptions.Features.PARAGRAPH
    )

    # 3️⃣ Convert and save
    output_file = "output.md"
    Converter.convert_html(document, options, output_file)
    print(f"✅ Markdown saved to {output_file}")

if __name__ == "__main__":
    main()
```

使用以下方式执行：

```bash
python convert_html_to_markdown.py
```

你会看到 `output.md` 包含预期的 Markdown 表示。

## 结论

现在你已经掌握了如何在 Python 中 **将 HTML 转换为 Markdown**、从 HTML 中提取链接，并使用 `MarkdownSaveOptions` 控制输出格式。这种方法适用于单文件、批量或远程 URL， 为文档生成器、静态站点流水线或数据提取脚本提供了灵活的基础。

**后续步骤**

- 试验其他 `MarkdownSaveOptions.Features`（如 `TABLE` 或 `IMAGE`），以包含更多 HTML 元素。
- 如需严格遵循 CommonMark，可将格式化器切换为 `MarkdownSaveOptions.Formatter.CommonMark`。
- 将此转换与静态站点生成器（例如 MkDocs）结合，实现内容自动发布。

祝编码愉快！


## 接下来你应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式。每个资源都提供了完整的可运行代码示例和逐步解释。

- [将 HTML 转换为 Markdown（Python） – 提取链接和段落](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [将 HTML 转换为 Markdown（Python） – GitLab 风格指南](/html/english/python/general/convert-html-to-markdown-in-python-gitlab-flavored-guide/)
- [使用 Python 将 HTML 转换为 Markdown – 完整指南](/html/english/python/general/convert-html-to-markdown-with-python-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}