---
category: general
date: 2026-09-10
description: 使用 GitLab 风格的 Markdown 快速将 HTML 转换为 Markdown。学习如何使用完整的 Python 示例将 HTML
  导出为 Markdown。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- export html as markdown
- html to markdown conversion
- convert html markdown
language: zh
lastmod: 2026-09-10
og_description: 使用 GitLab 风格的 Markdown 将 HTML 转换为 Markdown。本教程展示了完整的 Python 工作流，将
  HTML 导出为 Markdown。
og_image_alt: Screenshot of a Python script converting HTML to markdown
og_title: 使用 GitLab 风格的 Markdown 将 HTML 转换为 Markdown – Python 指南
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: convert HTML to markdown quickly using GitLab‑flavored markdown. Learn
    export HTML as markdown with a complete Python example.
  headline: How to convert HTML to Markdown with GitLab‑flavored markdown in Python
  type: TechArticle
- description: convert HTML to markdown quickly using GitLab‑flavored markdown. Learn
    export HTML as markdown with a complete Python example.
  name: How to convert HTML to Markdown with GitLab‑flavored markdown in Python
  steps:
  - name: Expected output
    text: 'Assuming `input.html` contains a simple heading and paragraph, the generated
      markdown will look like:'
  - name: a) Images with relative paths
    text: If the HTML references images using relative URLs, the converter will embed
      them as markdown image links. Ensure the images are available in the same repository,
      or copy them alongside the generated `.md` file.
  - name: b) Unsupported HTML tags
    text: Tags like `<script>` or `<style>` are ignored by the converter. If you need
      their content in markdown, extract it manually before conversion.
  - name: c) Large documents
    text: For files larger than 10 MB, consider streaming the conversion to avoid
      high memory usage. The library offers a `save` method that writes directly to
      a stream.
  type: HowTo
tags:
- Python
- markdown
- HTML processing
title: 如何在 Python 中使用 GitLab 风格的 Markdown 将 HTML 转换为 Markdown
url: /zh/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-markdow/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 GitLab 风格的 markdown 将 HTML 转换为 markdown

如果你需要为 GitLab 项目 **将 HTML 转换为 markdown**，本指南提供了一个可直接运行的解决方案。阅读前两句话后，你将知道要安装哪个库、哪些选项可以启用 GitLab 风格的 markdown 格式化器，以及如何将结果写入文件。该方法适用于任何你拥有的 HTML 文档，无论是 README、博客文章，还是生成的文档。

本教程涵盖了可靠的 **HTML 转 markdown 转换** 所需的全部内容：安装依赖、加载源文件、配置格式化器、处理边缘情况以及验证输出。无需外部服务，代码可在 Python 3.9+ 上运行。

## 前置条件

在开始之前，请确保你具备以下条件：

- 已在机器上安装 Python 3.9 或更高版本。
- 对命令行有基本了解。
- 能够访问你想要转换的 HTML 文件。

你还需要 `aspose-words` 包（或任何提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 的库）。示例使用的是 Aspose.Words for Python via .NET 的免费社区版，开箱即支持 GitLab 风格的 markdown。

```bash
pip install aspose-words
```

> **小贴士：** 如果你在虚拟环境中工作，请在安装包之前激活该环境，以免污染全局 site‑packages。

## 第 1 步：加载要转换的 HTML 文档

首先创建一个表示源文件的 `HTMLDocument` 对象。构造函数接受 HTML 文件的完整路径。

```python
from aspose.words import HTMLDocument

# Replace YOUR_DIRECTORY with the absolute or relative path to your file
html_path = "YOUR_DIRECTORY/input.html"
doc = HTMLDocument(html_path)
```

**为什么重要：** 将文件加载到文档对象后，库能够完全控制 DOM，从而在转换过程中保留标题、列表和表格等结构。跳过此步骤会迫使你手动解析 HTML，容易出错。

## 第 2 步：创建 markdown 保存选项

接下来实例化一个 `MarkdownSaveOptions` 对象。该对象保存所有会影响输出格式的设置。

```python
from aspose.words import MarkdownSaveOptions

opts = MarkdownSaveOptions()
```

你可以调整许多属性（例如换行、图片处理），但默认值已经能够为大多数使用场景生成干净的 markdown。

## 第 3 步：选择 GitLab 风格的 markdown 格式化器

GitLab 在标准 CommonMark 基础上增加了一些扩展，如任务列表和表格语法。库通过 `Formatter.GIT` 枚举值公开这些扩展。

```python
# Enable GitLab‑flavored markdown
opts.formatter = MarkdownSaveOptions.Formatter.GIT
```

**为什么重要：** 如果不设置格式化器，库会生成通用的 markdown，可能会遗漏 GitLab 特有的功能，例如带属性的代码块或表情快捷方式。启用 GitLab 格式化器可确保输出与 GitLab 原生渲染保持一致。

## 第 4 步：将 HTML 文档转换为 markdown 并保存结果

最后，调用静态的 `convert_html` 方法，传入文档、选项以及目标路径。

```python
from aspose.words import Converter

output_path = "YOUR_DIRECTORY/output.md"
Converter.convert_html(doc, opts, output_path)
print(f"Markdown saved to {output_path}")
```

脚本执行完毕后，`output.md` 即为 `input.html` 的 GitLab 风格 markdown 版本。

### 预期输出

假设 `input.html` 包含一个简单的标题和段落，生成的 markdown 将如下所示：

```markdown
# Sample Heading

This is a paragraph converted from HTML.
```

如果源 HTML 包含任务列表，GitLab 风格的语法 (`- [ ]`) 将自动出现。

## 第 5 步：验证转换（可选但推荐）

自动化测试可以帮助你在源 HTML 变化时捕获回归。一个最小的验证步骤读取输出文件并检查预期的 markdown 模式。

```python
import pathlib

def verify_markdown(path: str, expected_snippet: str) -> bool:
    content = pathlib.Path(path).read_text(encoding="utf-8")
    return expected_snippet in content

# Example verification
if verify_markdown(output_path, "# Sample Heading"):
    print("Verification passed: heading found.")
else:
    print("Verification failed: heading missing.")
```

**为什么重要：** HTML 可能包含复杂结构（嵌套表格、自定义标签）。快速的完整性检查可以确认关键元素在转换后仍然存在。

## 第 6 步：处理常见边缘情况

### a) 使用相对路径的图片

如果 HTML 使用相对 URL 引用图片，转换器会将其嵌入为 markdown 图片链接。请确保这些图片在同一仓库中，或将它们与生成的 `.md` 文件一起复制。

```python
# Example: copy images to the markdown folder
import shutil, os

image_folder = pathlib.Path("YOUR_DIRECTORY/images")
target_folder = pathlib.Path("YOUR_DIRECTORY/markdown_images")
target_folder.mkdir(exist_ok=True)

for img in image_folder.iterdir():
    shutil.copy(img, target_folder / img.name)
```

### b) 不受支持的 HTML 标签

`<script>` 或 `<style>` 等标签会被转换器忽略。如果你需要这些标签的内容出现在 markdown 中，请在转换前手动提取。

```python
# Strip <script> tags using BeautifulSoup before conversion
from bs4 import BeautifulSoup

with open(html_path, "r", encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
    for script in soup(["script", "style"]):
        script.decompose()
    cleaned_html = str(soup)

# Save cleaned HTML to a temporary file for conversion
temp_path = "temp_clean.html"
with open(temp_path, "w", encoding="utf-8") as f:
    f.write(cleaned_html)

doc = HTMLDocument(temp_path)
# Continue with steps 2‑4 as before
```

### c) 大文档

对于大于 10 MB 的文件，建议使用流式转换以避免高内存占用。库提供了 `save` 方法，可直接写入流。

```python
with open(output_path, "w", encoding="utf-8") as out_stream:
    Converter.convert_html(doc, opts, out_stream)
```

## 第 7 步：为多个文件自动化工作流

如果需要为整个目录 **导出 HTML 为 markdown**，一个简单的循环可以为你节省时间。

```python
import glob

html_files = glob.glob("YOUR_DIRECTORY/*.html")
for html_file in html_files:
    doc = HTMLDocument(html_file)
    opts = MarkdownSaveOptions()
    opts.formatter = MarkdownSaveOptions.Formatter.GIT

    md_file = pathlib.Path(html_file).with_suffix(".md")
    Converter.convert_html(doc, opts, str(md_file))
    print(f"Converted {html_file} → {md_file}")
```

该脚本会处理每个 `.html` 文件，应用 GitLab 风格的格式化器，并生成对应的 `.md` 文件。

## 结论

现在，你已经掌握了一套完整的、可投入生产的 **将 HTML 转换为 markdown** 方法，使用 Python 并利用 GitLab 风格的 markdown。指南涵盖了加载源文件、配置格式化器、执行转换以及处理常见坑点（如图片路径和大文件）。按照这些步骤，你可以可靠地 **导出 HTML 为 markdown**，将脚本集成到 CI 流水线，或批量处理文档文件夹。

接下来，探索其他风格（GitHub、CommonMark）的 **HTML 转 markdown 转换**，或将工作流集成到静态站点生成器中。尝试自定义 `MarkdownSaveOptions` 设置，以微调换行、表格渲染或代码块属性，适配你的特定 GitLab 环境。

祝转换愉快！

## 接下来你应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，每个资源都提供了完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert markdown to html – Java guide with PDF output](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}