---
category: general
date: 2026-11-17
description: 如何快速将 HTML 转换为 Git 风格的 Markdown，提取标题、链接和表格，同时高效处理大型 HTML 文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to convert html
- extract headings from html
- html to git markdown
- convert large html
language: zh
lastmod: 2026-11-17
og_description: 如何将HTML转换为Git风格的Markdown，提取标题、链接和表格，并在适当的资源处理下处理大型HTML文件。
og_image_alt: Screenshot showing how to convert HTML to Git‑flavored Markdown using
  code options
og_title: 如何将HTML转换为Git风格的Markdown——完整指南
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: How to convert HTML to Git‑flavored Markdown quickly, extracting headings,
    links, and tables while handling large HTML files efficiently.
  headline: How to convert HTML to Git‑flavored Markdown
  type: TechArticle
- description: How to convert HTML to Git‑flavored Markdown quickly, extracting headings,
    links, and tables while handling large HTML files efficiently.
  name: How to convert HTML to Git‑flavored Markdown
  steps:
  - name: '**`HTMLDocument`** – loads the source HTML while respecting a maximum resource‑handling
      depth.'
    text: '**`HTMLDocument`** – loads the source HTML while respecting a maximum resource‑handling
      depth.'
  - name: '**`MarkdownSaveOptions`** – tells the converter which markdown features
      to keep and which formatter to use.'
    text: '**`MarkdownSaveOptions`** – tells the converter which markdown features
      to keep and which formatter to use.'
  - name: '**`ResourceHandlingOptions`** – controls how external assets such as images
      are saved.'
    text: '**`ResourceHandlingOptions`** – controls how external assets such as images
      are saved.'
  type: HowTo
tags:
- HTML conversion
- Markdown
- Git‑flavored markdown
- Resource handling
title: 如何将 HTML 转换为 Git 风格的 Markdown
url: /zh/python/general/how-to-convert-html-to-git-flavored-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何将 HTML 转换为 Git‑flavored Markdown

如果您需要 **how to convert html** 成为干净的 Git‑flavored Markdown 文件，本指南将向您展示具体步骤。您将学习如何仅保留标题、链接和表格，限制大型页面的资源嵌套深度，并将外部图片存储在专用文件夹中。

本教程涵盖了将大型 HTML 文档转换、从 HTML 中提取标题以及生成在 GitHub‑flavored 渲染下完美工作的 Markdown 所需的全部内容。

## 如何将 HTML 转换为 Git‑flavored Markdown

转换过程围绕三个对象：

1. **`HTMLDocument`** – 在遵守最大资源处理深度的前提下加载源 HTML。
2. **`MarkdownSaveOptions`** – 告诉转换器保留哪些 Markdown 功能以及使用哪种格式化器。
3. **`ResourceHandlingOptions`** – 控制外部资源（如图片）的保存方式。

在调用 `Converter.convert` 之前配置这些对象，即可获得仅包含您关心元素的确定性 Markdown 输出。

```python
# Step 1: Limit resource nesting depth while loading the HTML document
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 3
html_doc = HTMLDocument(
    "YOUR_DIRECTORY/huge_page.html",
    ResourceHandlingOptions=resource_opts
)
```

**为什么这很重要：**  
大型 HTML 页面常常嵌入脚本、iframe 或深度嵌套的 CSS，可能导致解析器无限递归。将 `max_handling_depth` 设置为较低的值（例如 3）可防止内存使用失控并加快加载阶段，这在您 **convert large html** 文件时尤为关键。

## 使用 MarkdownSaveOptions 从 HTML 中提取标题

下一步告诉转换器仅保留您需要的 Markdown 功能。对于大多数文档工作流，您只想要标题、链接和表格。

```python
# Step 2: Set up Markdown conversion to Git‑flavored format and keep only headings, links, and tables
markdown_opts = MarkdownSaveOptions()
markdown_opts.formatter = MarkdownSaveOptions.Formatter.GIT
markdown_opts.features = (
    MarkdownSaveOptions.Feature.HEADER |
    MarkdownSaveOptions.Feature.LINK |
    MarkdownSaveOptions.Feature.TABLE
)
```

**为什么这很重要：**  
`features` 标志充当过滤器。启用 `HEADER` 后，您会自动 **extract headings from html** 并将其转换为 `#`、`##` 等，这是任何 Markdown 大纲的核心。添加 `LINK` 和 `TABLE` 可确保导航和数据保持完整，而其余所有内容（脚本、样式、注释）都会被剥离。

## 高效转换大型 HTML

在处理巨大的页面时，您可能担心转换会超时或生成巨大的 Markdown 文件。上述配置已经缓解了大多数性能问题，但以下几点额外提示可帮助您更安全地进行转换：

* **分块处理** – 如果源 HTML 超过几百兆，先将其拆分为逻辑章节后再进行转换。
* **使用流式 I/O** – `Converter.convert` 方法直接写入目标文件，避免将整个 Markdown 完整复制到内存中。
* **监控资源使用** – 在 `ResourceHandlingOptions` 上启用日志记录，以查看处理了多少外部文件。

这些实践使得在 **convert large html** 场景下的流程更加稳健。

## 配置外部图片处理

Git‑flavored Markdown 会渲染仓库内的图片。为保持 Markdown 干净，请将每个外部图片存储为 `assets` 文件夹中的单独文件，并使用相对路径引用。

```python
# Step 3: Configure external image handling – save them as separate files in the "assets" folder
markdown_resource_opts = ResourceHandlingOptions()
markdown_resource_opts.save_external_resources = True
markdown_opts.resource_handling_options = markdown_resource_opts
```

**为什么这很重要：**  
当 `save_external_resources` 为 `True` 时，转换器会下载每个 `<img>` 标签，将图片文件写入 `assets/`，并相应地重写 Markdown 图片链接。这样即可生成一个自包含的仓库，能够在 GitHub、GitLab 或任何静态站点生成器上正常工作。

## 执行转换

准备好所有选项后，最终调用会写入 Markdown 文件。

```python
# Step 4: Convert the HTML document to Markdown using the configured options
Converter.convert(html_doc, "YOUR_DIRECTORY/output.md", markdown_opts)
```

**预期输出：**  

```markdown
# Main Title

## Section One

Some introductory text with a [link](https://example.com).

| Header 1 | Header 2 |
|----------|----------|
| Cell A1  | Cell B1  |

![Image description](assets/image1.png)
```

文件仅包含标题、链接和表格，所有外部图片均位于 `assets/` 下。

## 完整工作示例

下面是一段可直接放入项目的完整脚本。请将占位路径替换为您实际的目录。

```python
# -*- coding: utf-8 -*-

from aspose.html import HTMLDocument, Converter, MarkdownSaveOptions, ResourceHandlingOptions

# ----------------------------------------------------------------------
# 1. Load the HTML file with a safe resource‑handling depth
# ----------------------------------------------------------------------
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 3          # Prevent deep recursion on huge pages
html_doc = HTMLDocument(
    "YOUR_DIRECTORY/huge_page.html",
    ResourceHandlingOptions=resource_opts
)

# ----------------------------------------------------------------------
# 2. Define markdown options – Git‑flavored, keep only needed features
# ----------------------------------------------------------------------
markdown_opts = MarkdownSaveOptions()
markdown_opts.formatter = MarkdownSaveOptions.Formatter.GIT
markdown_opts.features = (
    MarkdownSaveOptions.Feature.HEADER |
    MarkdownSaveOptions.Feature.LINK |
    MarkdownSaveOptions.Feature.TABLE
)

# ----------------------------------------------------------------------
# 3. Save external images into an assets folder
# ----------------------------------------------------------------------
image_opts = ResourceHandlingOptions()
image_opts.save_external_resources = True
markdown_opts.resource_handling_options = image_opts

# ----------------------------------------------------------------------
# 4. Run the conversion
# ----------------------------------------------------------------------
Converter.convert(html_doc, "YOUR_DIRECTORY/output.md", markdown_opts)

print("Conversion complete. Markdown saved to output.md")
```

使用 Python 3.8+ 和最新的 Aspose.HTML for Python 库运行脚本。执行后，您将在同目录下看到 `output.md` 和 `assets/` 目录。

## 常见问题与边缘情况

| 问题 | 回答 |
|------|------|
| **如果 HTML 包含相对图片 URL 会怎样？** | 转换器会在下载前根据 HTML 文件所在位置解析这些相对路径。请确保源目录可访问。 |
| **我可以保留额外的 Markdown 功能吗（例如代码块）？** | 在 `markdown_opts.features` 中加入 `MarkdownSaveOptions.Feature.CODE` 即可保留围栏代码段。 |
| **如何完全跳过图片？** | 将 `image_opts.save_external_resources = False`。`<img>` 标签将从输出中移除。 |
| **输出是否兼容其他 Markdown 风格？** | `GIT` 格式化器遵循 GitHub‑flavored Markdown 规则，属于 CommonMark 的超集。若需纯 CommonMark，可使用 `MarkdownSaveOptions.Formatter.COMMONMARK`。 |
| **如果 HTML 损坏怎么办？** | Aspose.HTML 的解析器具有容错能力，会尝试修复破损的标记。但极度损坏的文件可能需要先使用 HTML tidy 工具进行预处理。 |

## 结论

您现在已经掌握了 **how to convert html** 为干净的 Git‑flavored Markdown、从 HTML 中提取标题以及高效处理 **convert large html** 场景的方法。通过限制资源深度、仅选择所需的 Markdown 功能并配置外部图片处理，转换过程变得快速、可靠，且适用于版本控制工作流。

### 下一步

* 探索 **html to git markdown** 选项，例如自定义项目符号样式或脚注处理。  
* 将此流水线与 CI 作业结合，在每次提交时自动转换文档页面。  
* 试验 `ResourceHandlingOptions` 标志，以过滤脚本、样式或其他不需要的资产。

祝您转换愉快，欢迎根据项目的具体需求自由改写脚本！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，每个资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [如何在 Python 中使用 GitLab‑flavored markdown 将 HTML 转换为 Markdown](/html/english/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-markdow/)
- [在将 HTML 转换为 Markdown 时如何导出链接](/html/english/python/general/how-to-export-links-while-converting-html-to-markdown/)
- [如何使用 Aspose – 将 HTML 转换为 Markdown 并提取链接](/html/english/python/general/how-to-use-aspose-convert-html-to-markdown-and-extract-links/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}