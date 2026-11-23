---
category: general
date: 2026-09-23
description: 学习如何使用 GitLab 风格的格式化器将 HTML 转换为 Markdown 并导出为 Markdown。一步一步的指南，附完整的 Python
  代码。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- export html as markdown
- set markdown formatter
- how to convert html
- convert html document
language: zh
lastmod: 2026-09-23
og_description: 使用 GitLab 风格的格式化器将 HTML 转换为 Markdown 并导出为 Markdown。请按照本完整教程获取可直接运行的
  Python 脚本。
og_image_alt: Terminal window showing a Python script that converts an HTML file to
  a Markdown file
og_title: 在 Python 中将 HTML 转换为 Markdown – 完整指南及自定义格式化器
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to convert HTML to Markdown and export HTML as Markdown using
    the GitLab‑flavored formatter. Step‑by‑step guide with full Python code.
  headline: How to convert HTML to Markdown with a custom formatter in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Conversion
title: 如何在 Python 中使用自定义格式化器将 HTML 转换为 Markdown
url: /zh/python/general/how-to-convert-html-to-markdown-with-a-custom-formatter-in-p/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 中的自定义格式化器将 HTML 转换为 Markdown

如果您需要**将 HTML 转换为 Markdown**，本教程将向您展示以编程方式完成此操作的确切步骤。您将看到如何**将 HTML 导出为 Markdown**、配置所需的格式化器，并通过一次 Python 调用运行转换。

我们将使用提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 的 `aspose-words-cloud` 风格 API。完成本指南后，您将拥有一个可重用的脚本，能够处理任何 HTML 文件并生成符合 GitLab 风格预设的 Markdown 文件。

## 前提条件

在开始之前，请确保您拥有：

* Python 3.9 或更高版本已安装  
* `aspose-words-cloud`（或等效）包，提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter`。使用以下命令安装：

```bash
pip install aspose-words-cloud
```

* 一个包含您想要转换的源 HTML 文件的文件夹（例如 `sample.html`）。

## 步骤 1：加载源 HTML 文档

第一步是将 HTML 文件读取到 `HTMLDocument` 对象中。该对象抽象了 DOM 并为转换准备内容。

```python
# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/sample.html")
```

*此步骤的重要性* —— 加载文件会创建一个内存中的表示，转换器可以高效遍历。如果跳过此步骤，转换器将反复读取文件，导致性能下降。

## 步骤 2：设置 Markdown 格式化器

不同平台对 Markdown 的解释略有差异。库允许您选择预设的格式化器；通过将 `MarkdownSaveOptions.formatter` 设置为 `GIT` 可以选择 GitLab 风格的预设。这满足了 **set markdown formatter** 的要求。

```python
# Step 2: Configure Markdown save options to use the GitLab‑flavored preset
md_options = MarkdownSaveOptions()
md_options.formatter = MarkdownSaveOptions.Formatter.GIT   # GIT = GitLab flavor (default for standard)
```

*为何需要自定义格式化器* —— 某些服务（GitHub、GitLab、Bitbucket）对语法有细微差别。通过显式设置格式化器，您可以确保标题、表格和代码块在目标平台上正确渲染。

## 步骤 3：将 HTML 转换为 Markdown 并保存文件

现在调用静态的 `Converter.convert_html` 方法。它接受已加载的文档、配置好的选项以及目标路径。

```python
# Step 3: Convert the HTML to Markdown and save the output file
Converter.convert_html(html_doc, md_options, "YOUR_DIRECTORY/sample.md")
```

调用完成后，`sample.md` 包含原始 HTML 的 Markdown 表示。您可以在任意编辑器中打开该文件以验证结果。

### 预期输出

假设 `sample.html` 包含一个简单的段落和一个标题，生成的 `sample.md` 将如下所示：

```markdown
# Sample Heading

This is a paragraph extracted from the original HTML file.
```

如果源 HTML 包含表格、列表或代码块，格式化器会将它们转换为兼容 GitLab 的 Markdown 等价形式。

## 如何批量转换 HTML 文档

通常您需要批量**转换 html 文档**文件。将上述三个步骤封装在函数中，并遍历目录：

```python
import os

def convert_html_to_md(src_path: str, dst_path: str, formatter=MarkdownSaveOptions.Formatter.GIT):
    """Convert a single HTML file to Markdown using the chosen formatter."""
    html_doc = HTMLDocument(src_path)

    md_options = MarkdownSaveOptions()
    md_options.formatter = formatter

    Converter.convert_html(html_doc, md_options, dst_path)

# Batch conversion example
source_dir = "YOUR_DIRECTORY/html_files"
target_dir = "YOUR_DIRECTORY/md_output"
os.makedirs(target_dir, exist_ok=True)

for filename in os.listdir(source_dir):
    if filename.lower().endswith(".html"):
        src_file = os.path.join(source_dir, filename)
        dst_file = os.path.join(target_dir, os.path.splitext(filename)[0] + ".md")
        convert_html_to_md(src_file, dst_file)
        print(f"Converted {filename} → {os.path.basename(dst_file)}")
```

*专业提示*：对 GitLab 使用 `formatter=MarkdownSaveOptions.Formatter.GIT`，对 GitHub 使用 `MarkdownSaveOptions.Formatter.GFM`，或使用 `MarkdownSaveOptions.Formatter.DEFAULT` 获取通用输出。这展示了 **set markdown formatter** 在不同工作流中的灵活性。

## 常见陷阱及避免方法

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Images are missing in the Markdown file | The converter does not embed image data; it only copies the `src` attribute. | Ensure the image URLs are absolute or copy the image files to the same folder as the Markdown output. |
| Table alignment is off | Different formatters handle column alignment differently. | Choose the formatter that matches your target platform or manually adjust the generated table. |
| Unicode characters become garbled | The source HTML uses a different encoding than UTF‑8. | Open the HTML file with the correct encoding before creating `HTMLDocument`. |

翻译后：

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| Markdown 文件中缺少图片 | 转换器不会嵌入图片数据，只复制 `src` 属性。 | 确保图片 URL 为绝对路径，或将图片文件复制到与 Markdown 输出相同的文件夹中。 |
| 表格对齐错误 | 不同的格式化器对列对齐的处理方式不同。 | 选择与目标平台匹配的格式化器，或手动调整生成的表格。 |
| Unicode 字符出现乱码 | 源 HTML 使用的编码不同于 UTF‑8。 | 在创建 `HTMLDocument` 之前，以正确的编码打开 HTML 文件。 |

## 验证转换

运行脚本后，在 Markdown 预览器（例如 VS Code、GitLab UI）中打开生成的 `.md` 文件。检查标题、列表和代码块是否如预期显示。如果发现差异，请重新查看 **set markdown formatter**，选择更合适的预设。

## 结论

现在您已经了解如何**将 HTML 转换为 Markdown**、**将 HTML 导出为 Markdown**，以及**设置 markdown formatter**以匹配 GitLab 风格。完整的解决方案——加载 HTML、配置格式化器并调用转换器——覆盖了最常见的使用场景，并可扩展至批量处理或自定义格式化需求。

欢迎尝试其他格式化器选项（`GFM`、`DEFAULT`），或将此脚本集成到 CI/CD 流水线中，自动从 HTML 源生成文档。祝转换愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [在 .NET 中使用 Aspose.HTML 将 HTML 转换为 Markdown](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown 转 HTML（Java）- 使用 Aspose.HTML 转换](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}