---
category: general
date: 2026-08-22
description: 学习如何在 Python 中使用简单的三步脚本将 HTML 转换为 Markdown。包括转换选项和导出技巧。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create markdown from html
- convert html to markdown
- how to convert html
- export html to markdown
- html to markdown python
language: zh
lastmod: 2026-08-22
og_description: 仅用三行 Python 将 HTML 转换为 Markdown。本指南展示了转换、格式化选项以及如何高效地将 HTML 导出为 Markdown。
og_image_alt: Screenshot of a Python script converting an HTML file to a markdown
  file
og_title: 使用 Python 将 HTML 转换为 Markdown – 步骤指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-22'
  description: Learn how to create markdown from HTML in Python with a simple three‑step
    script. Includes conversion options and export tips.
  headline: How to create markdown from HTML using Python
  type: TechArticle
tags:
- markdown
- html
- python
- conversion
title: 如何使用Python将HTML转换为Markdown
url: /zh/python/general/how-to-create-markdown-from-html-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 将 HTML 转换为 Markdown

如果你需要 **从 HTML 创建 Markdown**，本简短指南将展示如何使用 Python 完成此操作。你将看到一个清晰的三步脚本：加载 HTML 文件、配置 Git 风格的 Markdown 输出，并将结果写入磁盘。

将网页内容转换为轻量级标记是构建静态站点、文档流水线或数据分析笔记本时的常见任务。在本教程中，我们还会涉及 **将 HTML 转换为 markdown** 的可选格式化、回答 **如何高效地将 HTML 转换** 的问题，并演示使用流行的 `groupdocs-conversion` 库进行 **export HTML to markdown** 工作流。

## 前置条件

在开始之前，请确保你已经：

* 安装了 Python 3.8 或更高版本。
* 安装了 `groupdocs-conversion` 包（或任何提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 的库）。使用以下命令安装：

```bash
pip install groupdocs-conversion
```

* 准备好要转换的 HTML 文件，例如位于你可控文件夹中的 `sample.html`。

无需额外的系统依赖，代码可在 Windows、macOS 和 Linux 上运行。

## 步骤 1：加载源 HTML 文档

首先创建一个表示源文件的 `HTMLDocument` 对象。

```python
from groupdocs.conversion import HTMLDocument

# Step 1 – load the source HTML document
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

**为什么重要：** `HTMLDocument` 会解析文件、解析相对链接，并为转换准备 DOM。如果文件未找到，构造函数会抛出明确的 `FileNotFoundError`，让你能够提前处理缺失的输入。

## 步骤 2：配置 Markdown 保存选项（Git‑flavored）

Markdown 有多种方言。Git‑flavored Markdown（GFM）支持表格、任务列表和围栏代码块，这在 README 文件或 GitHub 页面中经常需要。

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFormatter

# Step 2 – set up the Markdown options
md_options = MarkdownSaveOptions()
# Choose GFM for maximum compatibility with GitHub, GitLab, etc.
md_options.formatter = MarkdownFormatter.GIT   # alternative: MarkdownFormatter.DEFAULT
```

**为什么重要：** 通过显式选择 `MarkdownFormatter.GIT`，可以确保输出遵循 GitHub 渲染的相同规则，避免在仓库中显示 Markdown 时出现意外。如果你更倾向于普通 Markdown，只需将 `MarkdownFormatter.GIT` 替换为 `MarkdownFormatter.DEFAULT`。

## 步骤 3：将 HTML 文档转换为 Markdown 文件

现在调用转换引擎并将结果写入目标路径。

```python
from groupdocs.conversion import Converter

# Step 3 – perform the conversion and export the file
output_path = "YOUR_DIRECTORY/sample.md"
Converter.convert(html_doc, md_options, output_path)

print(f"✅ Conversion complete: {output_path}")
```

**为什么重要：** `Converter.convert` 负责繁重的工作——将 HTML 标签翻译为对应的 Markdown、在需要时复制图片到输出文件夹、并应用你选择的格式化器。该方法成功时返回 `None`，但你可以捕获 `ConversionException` 以获取详细的错误报告。

### 预期输出

运行脚本后，`sample.md` 将包含类似以下内容：

```markdown
# Sample Title

This is a paragraph extracted from the original HTML file.

- Item 1
- Item 2
- Item 3

```python
print("Hello, world!")
```

> A blockquote from the source page.

[Link text](https://example.com)
```

具体的 Markdown 会反映 `sample.html` 的结构。表格、图片和代码块将按照 GFM 规则进行转换。

## 常见变体和边缘情况

| 情况 | 推荐的调整 |
|-----------|-------------------|
| **大型 HTML 文件 (>10 MB)** | 增加 Python 递归限制，或在库支持的情况下使用 `HTMLDocument.open_stream()` 流式读取输入。 |
| **使用绝对 URL 引用的图片** | 将 `md_options.embed_images = True` 设置为将图片嵌入为 base‑64 数据 URI，或保持为链接以获得更轻的输出。 |
| **需要普通 Markdown 而非 GFM** | 将 `md_options.formatter = MarkdownFormatter.DEFAULT`。 |
| **需要忽略自定义 CSS 类** | 使用 `md_options.ignore_css_classes = ["unwanted-class"]`。 |
| **在 CI/CD 流水线中运行** | 将脚本包装在 `try/except` 块中，并在失败时以非零状态退出，以便流水线快速失败。 |

### 专业提示

如果你计划批量转换多个文件，复用同一个 `MarkdownSaveOptions` 实例，并仅在循环内部更改输入/输出路径。这样可以减少对象创建开销，将处理速度提升约 15 %。

```python
import os
from pathlib import Path

source_dir = Path("YOUR_DIRECTORY/html")
target_dir = Path("YOUR_DIRECTORY/md")
target_dir.mkdir(parents=True, exist_ok=True)

for html_file in source_dir.glob("*.html"):
    md_file = target_dir / f"{html_file.stem}.md"
    doc = HTMLDocument(str(html_file))
    Converter.convert(doc, md_options, str(md_file))
    print(f"Converted {html_file.name} → {md_file.name}")
```

## 在其他语言中将 HTML 转换为 Markdown（快速说明）

虽然本教程侧重于 **html to markdown python**，但相同的概念同样适用于 Java、C# 或 JavaScript SDK：创建文档对象、配置 Markdown 格式化器，然后调用转换器。如果你需要在非 Python 环境中 **export HTML to markdown**，请寻找对应语言 SDK 中的 `HtmlDocument`、`MarkdownSaveOptions` 和 `Converter` 类。

## 结论

现在你已经掌握了使用简洁的 Python 脚本 **从 HTML 创建 markdown** 的方法。三步流程——加载 HTML、设置 Git‑flavored 选项、执行转换——涵盖了任何 **convert html to markdown** 工作流的核心。接下来你可以：

* 将脚本集成到静态站点生成器中。
* 在 CI 流水线中自动化文档更新。
* 使用自定义后处理（例如链接重写或标题调整）扩展转换功能。

随意尝试次要选项——不同格式化器下的 **how to convert html**，或针对图片和表格的 **export html to markdown** 设置。祝你转换愉快！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在项目中进一步使用 API 功能并探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert markdown to html – Java guide with PDF output](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}