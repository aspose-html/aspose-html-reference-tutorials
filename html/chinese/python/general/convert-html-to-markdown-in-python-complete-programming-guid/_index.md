---
category: general
date: 2026-08-06
description: 使用 Python 将 HTML 转换为 Markdown。了解如何设置格式化器、将 HTML 保存为 Markdown，以及通过一步一步的示例导出
  HTML 为 Markdown。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to set formatter
- save html as markdown
- how to convert html
- export html to markdown
language: zh
lastmod: 2026-08-06
og_description: 使用 Python 将 HTML 转换为 Markdown。本教程展示如何设置格式化器、将 HTML 保存为 Markdown，以及高效地将
  HTML 导出为 Markdown。
og_image_alt: Diagram illustrating convert html to markdown workflow
og_title: 在 Python 中将 HTML 转换为 Markdown – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to Markdown using Python. Learn how to set formatter,
    save HTML as Markdown, and export HTML to Markdown with a step‑by‑step example.
  headline: Convert HTML to Markdown in Python – complete programming guide
  type: TechArticle
- description: Convert HTML to Markdown using Python. Learn how to set formatter,
    save HTML as Markdown, and export HTML to Markdown with a step‑by‑step example.
  name: Convert HTML to Markdown in Python – complete programming guide
  steps:
  - name: '**Load the source HTML document** – creates an in‑memory representation
      of the file.'
    text: '**Load the source HTML document** – creates an in‑memory representation
      of the file.'
  - name: '**Configure Markdown save options** – tells the library which Markdown
      dialect to generate (Git‑flavored in this case).'
    text: '**Configure Markdown save options** – tells the library which Markdown
      dialect to generate (Git‑flavored in this case).'
  - name: '**Execute the conversion** – writes the Markdown output to disk.'
    text: '**Execute the conversion** – writes the Markdown output to disk.'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- conversion
- automation
title: 在 Python 中将 HTML 转换为 Markdown —— 完整编程指南
url: /zh/python/general/convert-html-to-markdown-in-python-complete-programming-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为 Markdown（Python）— 完整编程指南

如果您需要 **快速将 HTML 转换为 Markdown**，本指南将手把手教您。阅读前两句话后，您就能了解核心工作流，并看到一个可直接运行的脚本，能够 **将 HTML 导出为 Markdown**，并使用 Git 风格的格式化器。

您还将学习 **如何设置 formatter** 选项、这些设置为何重要，以及在 **保存 HTML 为 Markdown** 时如何避免格式丢失。教程涵盖前置条件、边缘情况以及可在任何需要 HTML‑to‑Markdown 转换的项目中应用的实用技巧。

## 前置条件

在开始之前，请确保您已具备：

* Python 3.8 或更高版本。
* `aspose.html` 包（或任何提供 `HTMLDocument`、`MarkdownSaveOptions` 与 `Converter` 的库）。使用以下方式安装：

```bash
pip install aspose-html
```

* 一个示例 HTML 文件（`sample.html`），放置在您可以引用的目录中，例如 `YOUR_DIRECTORY/`。

这些要求确保代码能够在 Windows、macOS 或 Linux 上直接运行。

## 转换过程概览

转换包括三个逻辑步骤：

1. **加载源 HTML 文档** – 在内存中创建文件的表示。
2. **配置 Markdown 保存选项** – 告诉库生成哪种 Markdown 方言（本例为 Git‑flavored）。
3. **执行转换** – 将 Markdown 输出写入磁盘。

每一步都封装在独立函数中，便于后续复用或替换。

![convert html to markdown workflow](workflow.png){alt="展示 HTML 转换为 Markdown 工作流的示意图"}

## 步骤 1：加载 HTML 文档

```python
from aspose.html import HTMLDocument

def load_html(path: str) -> HTMLDocument:
    """
    Loads an HTML file from the given path and returns an HTMLDocument object.
    The object provides a DOM‑like API that the converter later consumes.
    """
    # The constructor reads the file and parses it into a document tree.
    return HTMLDocument(path)
```

**此步骤的重要性：**  
`HTMLDocument` 类会解析原始 HTML，解析相对 URL 并标准化 DOM。没有正确的文档对象，转换器无法正确解释标题、列表或表格等元素。

**提示：** 如果您的 HTML 包含外部资源（图片、CSS），请确保文件系统路径或基础 URL 正确；否则转换器可能会丢失这些资源。

## 步骤 2：为 Git‑flavored Markdown 设置 formatter

```python
from aspose.html import MarkdownSaveOptions

def configure_markdown_options() -> MarkdownSaveOptions:
    """
    Creates a MarkdownSaveOptions instance and sets the formatter to Git‑flavored Markdown.
    This matches the syntax used by GitLab, GitHub, and many static site generators.
    """
    options = MarkdownSaveOptions()
    # The Formatter enum contains several dialects; GIT produces Git‑flavored output.
    options.formatter = options.Formatter.GIT
    return options
```

**为何需要设置 formatter：**  
不同平台对 Markdown 语法的细微差别（例如表格、任务列表）有所要求。选择 `GIT` 后，库会生成可无缝在 GitLab、GitHub 以及其他基于 Git 的工具中使用的输出。

**常见变体：**  
如果您需要 **将 html 导出为 markdown** 到更倾向于 CommonMark 的平台，请将 `options.Formatter.GIT` 替换为 `options.Formatter.COMMON_MARK`。

## 步骤 3：转换 HTML 并保存为 Markdown 文件

```python
from aspose.html import Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Executes the full conversion pipeline:
    1. Loads the HTML document.
    2. Configures the Markdown formatter.
    3. Writes the Markdown file to the target location.
    """
    # Load the source HTML.
    html_doc = load_html(source_path)

    # Prepare the formatter options.
    markdown_options = configure_markdown_options()

    # Perform the conversion and write the result.
    Converter.convert_html(html_doc, markdown_options, target_path)

# Example usage:
if __name__ == "__main__":
    src = "YOUR_DIRECTORY/sample.html"
    dst = "YOUR_DIRECTORY/sample.md"
    convert_html_to_markdown(src, dst)
    print(f"Conversion complete: '{dst}' now contains Markdown.")
```

**各参数说明：**

| 参数 | 用途 |
|----------|---------|
| `html_doc` | 第一步中解析得到的 HTML 文档对象。 |
| `markdown_options` | 第二步中定义的输出方言选项对象。 |
| `target_path` | Markdown 文件将要保存的文件系统路径。 |

**边缘情况处理：**  

* **大文件：** 对于大于 50 MB 的文件，考虑使用 `Converter.convert_html_to_stream`（若库提供）进行流式转换，以避免高内存占用。  
* **不受支持的标签：** 某些 HTML5 标签（如 `<details>`）没有直接的 Markdown 对应，转换器会将其丢弃，如这些元素至关重要，您可能需要后处理步骤。  

**专业提示：** 转换完成后，在 Markdown 预览器中打开生成的 `.md` 文件，检查标题、列表和表格是否如预期显示。如发现格式缺失，请再次确认源 HTML 的结构是否良好（使用 HTML 验证器）。

## 为其他 Markdown 方言设置 formatter

如果工作流需要不同的方言，请修改 `configure_markdown_options` 函数：

```python
def configure_markdown_options(dialect: str = "GIT") -> MarkdownSaveOptions:
    options = MarkdownSaveOptions()
    if dialect.upper() == "COMMON_MARK":
        options.formatter = options.Formatter.COMMON_MARK
    elif dialect.upper() == "GITHUB":
        options.formatter = options.Formatter.GITHUB
    else:
        options.formatter = options.Formatter.GIT
    return options
```

随后即可使用自定义方言调用 `convert_html_to_markdown`：

```python
markdown_options = configure_markdown_options("GITHUB")
```

此灵活性展示了 **如何将 html 转换** 为多个目标平台而无需重写核心逻辑。

## 保存 HTML 为 Markdown – 验证输出

脚本执行完毕后，您应当看到类似以下内容的文件（摘录）：

```markdown
# Sample Document

This is a paragraph extracted from the original HTML.

## Subheading

- Item 1
- Item 2
- Item 3

| Header 1 | Header 2 |
|----------|----------|
| Cell A1  | Cell B1  |
| Cell A2  | Cell B2  |
```

示例表明标题（`<h1>`、`<h2>`）、列表和表格已被忠实转换。如果您需要在 CI 流水线中 **将 HTML 保存为 markdown**，只需将此脚本加入构建步骤即可。

## 转换 HTML 为 Markdown 时的常见坑

| 症状 | 可能原因 | 解决方案 |
|---------|--------------|-----|
| 图片缺失 | `<img>` 标签使用相对 URL | 在转换前将 `html_doc.base_url` 设置为包含资源的文件夹路径。 |
| 表格错乱 | 复杂的嵌套表格 | 简化 HTML 或在 Markdown 中后处理以展平结构。 |
| 多余换行 | `<br>` 标签被转换为双换行 | 若库支持，可使用 `markdown_options.remove_extra_line_breaks = True`。 |

提前处理这些问题，可避免后期手动编辑的麻烦。

## 快速复制‑粘贴的完整脚本

```python
# convert_html_to_markdown.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def load_html(path: str) -> HTMLDocument:
    return HTMLDocument(path)

def configure_markdown_options(dialect: str = "GIT") -> MarkdownSaveOptions:
    options = MarkdownSaveOptions()
    fmt = dialect.upper()
    if fmt == "COMMON_MARK":
        options.formatter = options.Formatter.COMMON_MARK
    elif fmt == "GITHUB":
        options.formatter = options.Formatter.GITHUB
    else:
        options.formatter = options.Formatter.GIT
    return options

def convert_html_to_markdown(source_path: str, target_path: str, dialect: str = "GIT") -> None:
    html_doc = load_html(source_path)
    markdown_options = configure_markdown_options(dialect)
    Converter.convert_html(html_doc, markdown_options, target_path)

if __name__ == "__main__":
    src_file = "YOUR_DIRECTORY/sample.html"
    dst_file = "YOUR_DIRECTORY/sample.md"
    convert_html_to_markdown(src_file, dst_file, "GIT")
    print(f"Conversion complete: {dst_file}")
```

使用以下方式运行脚本：

```bash
python convert_html_to_markdown.py
```

您将得到一个适用于版本控制、文档站点或静态站点生成器的 Git‑flavored Markdown 文件。

## 结论

现在，您已经掌握了在 Python 中 **将 HTML 转换为 Markdown** 的完整流程，包括 **设置 formatter**、**保存 HTML 为 Markdown** 以及 **将 HTML 导出为 Markdown**（Git‑flavored） 的具体步骤。完整可运行的示例展示了最佳实践、常见边缘情况的处理方式，并可集成到自动化流水线中。

**后续步骤**

* 通过更改 formatter 探索其他 Markdown 方言（例如 **如何为 CommonMark 设置 formatter**）。  
* 将此脚本与文件监视器结合，实现新添加的 HTML 文件自动转换。  
* 如需更多转换功能，可研究 `pandoc` 等后处理工具。

祝您转换愉快！


## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在自己的项目中进一步掌握 API 功能并探索替代实现方式。每篇资源均提供完整可运行的代码示例和逐步解释。

- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}