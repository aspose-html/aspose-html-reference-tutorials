---
category: general
date: 2026-11-27
description: 学习如何使用 Aspose.HTML 在 Python 中将 HTML 转换为 Markdown。按照本分步指南，将 HTML 转换为 Markdown，启用
  GitLab 预设，并将 HTML 保存为 Markdown。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create markdown from html
- convert html to markdown
- html to markdown conversion
- save html as markdown
- how to convert html
language: zh
lastmod: 2026-11-27
og_description: 在 Python 中将 HTML 转换为 Markdown。本教程展示如何将 HTML 转换为 Markdown，生成兼容 GitLab
  的输出，并将 HTML 保存为 Markdown。
og_image_alt: Diagram illustrating how to create markdown from HTML using Python
og_title: 使用 Python 将 HTML 转换为 Markdown – 完整转换指南
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Learn how to create markdown from HTML in Python using Aspose.HTML.
    Follow this step‑by‑step guide to convert HTML to markdown, enable GitLab preset,
    and save HTML as markdown.
  headline: How to create markdown from HTML with Python
  type: TechArticle
- description: Learn how to create markdown from HTML in Python using Aspose.HTML.
    Follow this step‑by‑step guide to convert HTML to markdown, enable GitLab preset,
    and save HTML as markdown.
  name: How to create markdown from HTML with Python
  steps:
  - name: Load the source HTML document.
    text: Load the source HTML document.
  - name: Configure markdown save options (including the GitLab preset).
    text: Configure markdown save options (including the GitLab preset).
  - name: Run the conversion and write the markdown file.
    text: Run the conversion and write the markdown file.
  type: HowTo
- questions:
  - answer: Yes. Use `HTMLDocument.from_string(html_string)` instead of passing a
      file path.
    question: Can I convert a string of HTML without writing a file first?
  - answer: It forces images to use the `![]()` syntax with an escaped URL, which
      GitLab renders correctly.
    question: Does the GitLab preset affect image syntax?
  - answer: 'Wrap the conversion logic in a loop that iterates over a directory, changing
      `html_path` and `md_path` for each file. ## Full example – batch conversion
      script ```python import os from aspose.html import HTMLDocument, Converter,
      MarkdownSaveOptions def convert_folder(source_dir: str, dest_dir: str):'
    question: How do I batch‑process multiple HTML files?
  type: FAQPage
tags:
- markdown
- html
- python
- document‑conversion
title: 如何使用 Python 将 HTML 转换为 Markdown
url: /zh/python/general/how-to-create-markdown-from-html-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 将 HTML 转换为 Markdown

如果您需要在 Python 项目中 **create markdown from HTML**，本指南将向您展示具体步骤。您将看到如何将 HTML 转换为 markdown，配置输出以兼容 GitLab，并将结果保存为 `.md` 文件——只需几行代码。

将 HTML 转换为 markdown 是在迁移文档、生成 README 文件或将网页内容集成到静态站点生成器时的常见任务。在本教程中，我们使用 **Aspose.HTML for Python via .NET** 库，因为它提供可靠的 `html to markdown conversion` 和细粒度的保存选项。

阅读完本文后，您将能够运行一个脚本，将任意 HTML 文件转换为适用于 GitLab 等版本控制平台的 markdown 文件。

## 前提条件

* 已安装 Python 3.8+  
* 虚拟环境（可选，但推荐）  
* Aspose.HTML 包 – 使用以下方式安装：

```bash
pip install aspose-html
```

* 要转换的 HTML 文件（例如位于 `YOUR_DIRECTORY` 文件夹中的 `sample.html`）

这些前提条件使教程保持自包含，并避免外部依赖。

## 在 Python 中将 HTML 创建为 markdown

**create markdown from html** 工作流的核心包括三个步骤：

1. 加载源 HTML 文档。  
2. 配置 markdown 保存选项（包括 GitLab 预设）。  
3. 运行转换并写入 markdown 文件。

下面是完整的可运行脚本。每行代码都有注释，帮助您了解 **why**（原因），而不仅是 **what**（做了什么）。

```python
# ------------------------------------------------------------
# Step 1: Load the source HTML document
# ------------------------------------------------------------
from aspose.html import HTMLDocument, Converter, MarkdownSaveOptions

# Replace the path with the location of your HTML file
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)

# ------------------------------------------------------------
# Step 2: Create Markdown save options and enable the GitLab preset
# ------------------------------------------------------------
markdown_options = MarkdownSaveOptions()
# Setting `git` to True produces GitLab‑compatible markdown (e.g., fenced code blocks)
markdown_options.git = True

# ------------------------------------------------------------
# Step 3: Convert the HTML document to Markdown using the configured options
# ------------------------------------------------------------
# Destination markdown file
md_path = "YOUR_DIRECTORY/sample_git.md"

# Perform the conversion
Converter.convert(html_doc, markdown_options, md_path)

print(f"Conversion complete! Markdown saved to: {md_path}")
```

### 为什么这样有效

* **`HTMLDocument`** 解析输入文件并创建 DOM 的内存表示，转换器随后读取该表示。  
* **`MarkdownSaveOptions`** 允许您控制输出格式。启用 `git` 标志可使 markdown 与 GitLab 的渲染引擎保持一致，确保表格、代码块和任务列表正确显示。  
* **`Converter.convert`** 是一个一次性调用的方法，它应用选项并写入结果，使 **html to markdown conversion** 过程原子且线程安全。

## 附加配置选项（可选）

如果您需要对转换进行更细致的控制，Aspose.HTML 提供了多个属性：

| Option | Description | Typical use case |
|--------|-------------|------------------|
| `markdown_options.indent_spaces` | 缩进使用的空格数 | 使列表符合项目的风格指南 |
| `markdown_options.encode_url` | 对链接中的 URL 进行编码 | 防止特殊字符导致的链接破裂 |
| `markdown_options.escape_html` | 转义原始 HTML 标签 | 防止 HTML 片段被解释为 markdown |

Example:

```python
markdown_options.indent_spaces = 4
markdown_options.encode_url = True
```

### 需要注意的边缘情况

| Situation | What can happen | How to handle it |
|-----------|----------------|-----------------|
| **Large HTML files** ( > 10 MB ) | 因为整个文档被加载到内存，导致内存使用激增 | 如果环境支持，使用流式 API（`HTMLDocument.from_stream`） |
| **Unsupported HTML5 tags** | 这些标签可能被丢弃或作为纯文本渲染 | 验证输出并在需要时添加自定义后处理 |
| **Relative image paths** | 图像可能在 markdown 预览中不显示 | 将其转换为绝对 URL 或嵌入为 base64 数据 URI |

## 验证输出

在任意 markdown 查看器（VS Code、GitLab、GitHub）中打开 `sample_git.md`。您应该看到原始 HTML 的干净呈现，标题、列表、表格和代码块均被保留。快速的合理性检查：

```markdown
# Sample Title

This is a paragraph from the original HTML.

- List item 1
- List item 2

```python
print("Hello, markdown!")
```
```

如果 markdown 如预期显示，则 **save html as markdown** 步骤成功。

## 常见问题

**Q: 我可以在不先写入文件的情况下转换 HTML 字符串吗？**  
A: 可以。使用 `HTMLDocument.from_string(html_string)` 而不是传入文件路径。

**Q: GitLab 预设会影响图片语法吗？**  
A: 它强制图片使用 `![]()` 语法并对 URL 进行转义，GitLab 能正确渲染。

**Q: 如何批量处理多个 HTML 文件？**  
A: 将转换逻辑放入遍历目录的循环中，对每个文件更改 `html_path` 和 `md_path`。

## 完整示例 – 批量转换脚本

```python
import os
from aspose.html import HTMLDocument, Converter, MarkdownSaveOptions

def convert_folder(source_dir: str, dest_dir: str):
    # Ensure destination exists
    os.makedirs(dest_dir, exist_ok=True)

    # Prepare markdown options once
    md_opts = MarkdownSaveOptions()
    md_opts.git = True

    for filename in os.listdir(source_dir):
        if not filename.lower().endswith('.html'):
            continue  # skip non‑HTML files

        html_path = os.path.join(source_dir, filename)
        md_name = os.path.splitext(filename)[0] + ".md"
        md_path = os.path.join(dest_dir, md_name)

        doc = HTMLDocument(html_path)
        Converter.convert(doc, md_opts, md_path)
        print(f"Converted {filename} → {md_name}")

# Example usage
convert_folder("YOUR_DIRECTORY", "YOUR_DIRECTORY/markdown_output")
```

运行此脚本会将 `YOUR_DIRECTORY` 中的每个 `.html` 文件转换为放在 `markdown_output` 目录下的 markdown 文件。这展示了 **how to convert html** 的大规模用法。

## 结论

您现在已经了解如何使用 Python 和 Aspose.HTML **create markdown from HTML**。本教程覆盖了关键的 **convert html to markdown** 步骤，解释了每个配置选项，并展示了如何处理常见的边缘情况。  

接下来，您可以探索相关主题，例如针对其他平台（GitHub、Bitbucket）的 **html to markdown conversion**，或将转换嵌入 CI/CD 流水线以自动更新文档。尝试可选设置，以微调输出以符合项目的风格指南。  

祝转换愉快！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，构建在本教程演示的技术之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方式。

- [How to Use Aspose to Convert HTML to Markdown in Python – Complete Guide](/html/english/python/general/how-to-use-aspose-to-convert-html-to-markdown-in-python-comp/)
- [How to convert HTML to Markdown with GitLab‑flavored markdown in Python](/html/english/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-markdow/)
- [How to convert HTML to markdown with images using Python](/html/english/python/general/how-to-convert-html-to-markdown-with-images-using-python/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}