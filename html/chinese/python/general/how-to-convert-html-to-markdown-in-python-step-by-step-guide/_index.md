---
category: general
date: 2026-10-09
description: 使用 Python 快速将 HTML 转换为 Markdown。在本简明教程中学习完整的 Markdown 转换、Git 预设以及其他技巧。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to convert html
- html to markdown python
- markdown conversion with git
language: zh
lastmod: 2026-10-09
og_description: 使用 Python 和 Git 风格的预设将 HTML 转换为 Markdown。遵循本教程，即可在几秒钟内获得干净的 Markdown
  输出。
og_image_alt: Screenshot of Python code converting an HTML file to a git‑flavoured
  Markdown file
og_title: 在 Python 中将 HTML 转换为 Markdown – 完整指南
schemas:
- author: GroupDocs
  dateModified: '2026-10-09'
  description: convert html to markdown quickly with Python. Learn the full markdown
    conversion with git preset and other tips in this concise tutorial.
  headline: How to convert HTML to Markdown in Python – step‑by‑step guide
  type: TechArticle
- description: convert html to markdown quickly with Python. Learn the full markdown
    conversion with git preset and other tips in this concise tutorial.
  name: How to convert HTML to Markdown in Python – step‑by‑step guide
  steps:
  - name: '**Source** – a string containing HTML.'
    text: '**Source** – a string containing HTML.'
  - name: '**Destination path** – where the markdown file will be written.'
    text: '**Destination path** – where the markdown file will be written.'
  - name: '**Options** – the `MarkdownSaveOptions` we configured earlier.'
    text: '**Options** – the `MarkdownSaveOptions` we configured earlier.'
  type: HowTo
tags:
- Python
- HTML
- Markdown
- Document conversion
title: 如何在 Python 中将 HTML 转换为 Markdown——一步步指南
url: /zh/python/general/how-to-convert-html-to-markdown-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中将 HTML 转换为 Markdown – 步骤指南

如果你需要 **快速将 HTML 转换为 markdown**，本教程提供了一个可直接运行的 Python 解决方案。无论是提取博客内容、迁移文档，还是构建静态站点生成器，下面的示例演示了在保留 Git 风格 markdown 特性的前提下，最可靠的转换方式。

你还将学习 **使用 `markdown conversion with git` 预设将 HTML 转换**，了解常见陷阱，并获得完整可运行的脚本。无需外部网络服务——全部在本地完成。

## 本指南涵盖内容

* 安装所需库（`groupdocs-conversion`）。
* 为 Git 风格输出设置 **MarkdownSaveOptions**。
* 使用 **Converter.convert** 将 HTML 字符串或文件转换。
* 在转换过程中处理图片、表格和代码块。
* 验证结果并排查常见问题。

阅读完本指南后，你可以自信地说自己彻底掌握了 **html to markdown python** 转换。

## 前置条件

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | 该库使用了现代语言特性。 |
| `pip` access | 用于安装转换 SDK。 |
| Basic familiarity with Python functions | 运行脚本并修改选项所必需的基础。 |

如果你已经安装了 Python，便可以继续。

## 第一步：安装 GroupDocs Conversion SDK

```bash
pip install groupdocs-conversion
```

`groupdocs-conversion` 包提供了 `Converter` 类和 `MarkdownSaveOptions` 类型，供 **html to markdown python** 转换使用。安装时会自动拉取所有本地依赖，无需额外系统软件包。

> **Pro tip:** 使用虚拟环境（`python -m venv .venv`）将 SDK 与其他项目隔离。

## 第二步：导入所需类

```python
from groupdocs.conversion import Converter, MarkdownSaveOptions
```

`Converter` 是读取源文档的引擎，而 `MarkdownSaveOptions` 让你可以细调输出格式。将它们放在文件顶部导入，可使脚本更清晰、可复用。

## 第三步：准备 Markdown 保存选项

```python
# Step 1: Create Markdown save options
md_opts = MarkdownSaveOptions()

# Step 2: Enable the Git‑flavoured preset
md_opts.git = True
```

*为什么要启用 Git 风格预设？*  
Git 预设 (`md_opts.git = True`) 生成的 markdown 与 GitHub、GitLab、Bitbucket 使用的语法保持一致。它确保围栏代码块、表格和任务列表在这些平台上正确渲染。

如果不需要 Git 特有功能，可省略 `git` 行，得到普通的 CommonMark 输出。

## 第四步：加载 HTML 源

你可以将 HTML 作为字符串、文件路径或 URL 提供。下面示例读取本地的 `example.html` 文件：

```python
# Load HTML from a file (you can also use a string or request a remote page)
with open("example.html", "r", encoding="utf-8") as f:
    html_doc = f.read()
```

> **常见边缘情况:** 如果 HTML 中的 `<meta charset>` 与 UTF‑8 不同，请使用正确的编码打开文件，以免出现乱码。

## 第五步：执行转换

```python
# Step 3: Convert the HTML document to Markdown using the configured options
# The output file will be placed in the specified directory.
output_path = "output/git_style.md"
Converter.convert(html_doc, output_path, md_opts)
print(f"Conversion complete – Markdown saved to {output_path}")
```

`Converter.convert` 接受三个参数：

1. **Source** – 包含 HTML 的字符串。  
2. **Destination path** – markdown 文件的写入路径。  
3. **Options** – 前面配置好的 `MarkdownSaveOptions`。

因为我们使用了 Git 预设，标题会变为 `#`，表格使用管道语法，任务列表显示为 `- [ ]`。

### 验证结果

在任意 markdown 查看器（如 VS Code、GitHub 预览）中打开 `output/git_style.md`，应看到：

```markdown
# Sample Document

This is a paragraph extracted from the original HTML.

## Table Example

| Header 1 | Header 2 |
|----------|----------|
| Cell A   | Cell B   |

- [ ] Task item 1
- [x] Completed task
```

如果输出为空或缺少元素，请检查传入的 HTML 是否结构良好。标签不完整常导致转换器跳过相应部分。

## 处理图片和外部资源

默认情况下，SDK 会原样复制图片 URL。若想将图片以相对路径嵌入：

```python
md_opts.embed_images = True   # Embed images as base64 (optional)
md_opts.images_folder = "output/images"  # Directory for extracted images
```

将 `embed_images` 设置为 `True` 会把每个 `<img>` 标签转换为 base64 编码的 data URI，使 markdown 成为自包含文件。这在需要可移植文档时非常有用。

## 批量转换多个文件

如果需要 **convert html to markdown** 大量文件，可将转换包装在循环中：

```python
import pathlib

source_dir = pathlib.Path("html_sources")
output_dir = pathlib.Path("markdown_output")
output_dir.mkdir(exist_ok=True)

for html_path in source_dir.glob("*.html"):
    with html_path.open("r", encoding="utf-8") as f:
        html_content = f.read()
    md_file = output_dir / f"{html_path.stem}.md"
    Converter.convert(html_content, str(md_file), md_opts)
    print(f"Converted {html_path.name} → {md_file.name}")
```

该脚本对每个文件都使用相同的 **markdown conversion with git** 设置，确保整个项目的输出保持一致。

## 常见陷阱及规避方法

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| Missing tables | HTML tables are built with `<table>` tags that lack `<thead>` or `<tbody>` | Ensure the HTML includes proper table sections or pre‑process with BeautifulSoup to add them. |
| Code blocks appear as plain text | `<pre>` tags lack language class (e.g., `class="language-python"`) | Add a language identifier or set `md_opts.detect_code_language = True`. |
| Images appear broken in markdown preview | Relative paths are incorrect | Use `md_opts.images_folder` to control where images are saved, then adjust the markdown links accordingly. |
| Output file is empty | `html_doc` variable is `None` or empty | Verify that the file read operation succeeded and that the HTML source is not empty. |

## 完整可运行示例

将以下脚本保存为 `convert_html_to_md.py` 并运行 `python convert_html_to_md.py`。

```python
# convert_html_to_md.py
"""
Complete example: convert an HTML file to Git‑flavoured Markdown using
GroupDocs Conversion SDK.
"""

from pathlib import Path
from groupdocs.conversion import Converter, MarkdownSaveOptions

def convert_html_to_markdown(html_path: Path, md_path: Path, git_preset: bool = True):
    # Load HTML content
    html_content = html_path.read_text(encoding="utf-8")

    # Configure Markdown options
    md_opts = MarkdownSaveOptions()
    md_opts.git = git_preset          # enable markdown conversion with git
    md_opts.embed_images = False      # change to True if you need embedded images
    md_opts.images_folder = str(md_path.parent / "images")

    # Perform conversion
    Converter.convert(html_content, str(md_path), md_opts)
    print(f"✅ {html_path.name} → {md_path.name}")

if __name__ == "__main__":
    # Paths – adjust to your environment
    source_html = Path("example.html")
    destination_md = Path("output/git_style.md")

    # Ensure output directory exists
    destination_md.parent.mkdir(parents=True, exist_ok=True)

    convert_html_to_markdown(source_html, destination_md)
```

**预期输出**（在控制台显示）：

```
✅ example.html → git_style.md
Conversion complete – Markdown saved to output/git_style.md
```

打开 `output/git_style.md`，检查标题、表格、列表和代码块是否与原始 HTML 结构相匹配。

## 结论

现在，你拥有了一套使用 Python **将 HTML 转换为 markdown** 的可靠、可投入生产的方法。通过在 `MarkdownSaveOptions` 中启用 `git` 标志，转换会遵循 Git 风格的 markdown 约定，使结果可直接用于 GitHub、GitLab 或任何支持 markdown 的 CI 流水线。

记住：

* 只需安装一次 `groupdocs-conversion`，即可在多个项目中复用。  
* 使用 Git 预设 (`md_opts.git = True`) 可获得最兼容的 markdown。  
* 根据部署需求调整图片处理方式（`embed_images`、`images_folder`）。  
* 当需要大规模 **html to markdown python** 时，使用批处理目录。

接下来，你可以探索 **how to convert html** 为 PDF、DOCX 等其他格式，或将此脚本集成到 MkDocs 等静态站点生成器中。无论哪种方式，本指南的基础都为任何 markdown 转换任务提供了可靠的支撑。祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert markdown to html – Java guide with PDF output](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}