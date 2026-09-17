---
category: general
date: 2026-09-16
description: 学习快速将 HTML 转换为 Markdown，使用简易的 Python 脚本导出 HTML 为 Markdown 并保持图片完整。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- export html as markdown
- save html page as markdown
- how to convert html to markdown
- markdown conversion with images
language: zh
lastmod: 2026-09-16
og_description: 将 HTML 转换为 Markdown 并保留图像。本教程展示如何使用简洁的 Python 脚本将 HTML 导出为 Markdown。
og_image_alt: convert html to markdown script output showing markdown file with images
og_title: 将 HTML 转换为带图片的 Markdown – 步骤详解 Python 指南
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn to convert HTML to markdown quickly, export HTML as markdown
    and keep images intact with a simple Python script.
  headline: How to convert HTML to markdown with images using Python
  type: TechArticle
- description: Learn to convert HTML to markdown quickly, export HTML as markdown
    and keep images intact with a simple Python script.
  name: How to convert HTML to markdown with images using Python
  steps:
  - name: '**Validate the source HTML** – malformed markup can cause missing elements
      in the markdown output. Use tools like `html5lib` or browser dev tools to clean
      up the HTML first.'
    text: '**Validate the source HTML** – malformed markup can cause missing elements
      in the markdown output. Use tools like `html5lib` or browser dev tools to clean
      up the HTML first.'
  - name: '**Keep the output folder writable** – the script needs permission to create
      the resource sub‑folder.'
    text: '**Keep the output folder writable** – the script needs permission to create
      the resource sub‑folder.'
  - name: '**Version‑control the markdown** – once generated, commit the `.md` files
      to your repository; the accompanying resource folder should be added to `.gitignore`
      if you don’t need version history for binary assets.'
    text: '**Version‑control the markdown** – once generated, commit the `.md` files
      to your repository; the accompanying resource folder should be added to `.gitignore`
      if you don’t need version history for binary assets.'
  - name: '**Test the markdown rendering** – open the resulting file in a markdown
      viewer (e.g., VS Code, Typora) to ensure images display as expected.'
    text: '**Test the markdown rendering** – open the resulting file in a markdown
      viewer (e.g., VS Code, Typora) to ensure images display as expected.'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Document conversion
title: 如何使用 Python 将 HTML 转换为带图片的 Markdown
url: /zh/python/general/how-to-convert-html-to-markdown-with-images-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 将 HTML 转换为带图片的 Markdown

如果您需要 **convert HTML to markdown** 并保留所有链接的图片，本指南提供了一个完整、可直接运行的解决方案。无论是迁移博客、提取文档，还是构建静态站点生成器，下面的步骤都能让您在几秒钟内 **export HTML as markdown**。

您将学习如何 **save HTML page as markdown**，自动处理资源复制，并避免常见的图片链接断裂等陷阱。教程假设您具备基本的 Python 知识，并已安装最新版本的转换库。

## 前置条件

开始之前，请确保您拥有：

* 已安装 Python 3.8+（代码在 Windows、macOS 和 Linux 上均可运行）
* 提供 `HTMLDocument`、`MarkdownSaveOptions`、`ResourceHandlingOptions` 和 `Converter` 的 `groupdocs-conversion`（或兼容）包。使用以下方式安装：

```bash
pip install groupdocs-conversion
```

* 您想要转换的 HTML 文件，例如 `page.html`，位于可引用为 `YOUR_DIRECTORY` 的文件夹中。

> **Pro tip:** 将 HTML 与目标 markdown 文件夹放在一起；脚本会将图片复制到 markdown 文件旁的子文件夹中。

## 步骤 1：加载要转换的 HTML 文档

第一步创建一个代表源文件的 `HTMLDocument` 对象。该对象让转换器能够访问 DOM、样式和链接的资源。

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you wish to convert
doc = HTMLDocument("YOUR_DIRECTORY/page.html")
```

*Why this matters*: 加载文档后，它会从文件系统中隔离出来，使转换器能够使用干净的内存表示。如果文件路径不正确，构造函数会抛出明确的 `FileNotFoundError`，您可以捕获它以实现更好的错误处理。

## 步骤 2：创建 Markdown 保存选项

`MarkdownSaveOptions` 让您微调输出 markdown 的生成方式。大多数情况下默认设置已足够，但必须启用资源处理才能保留图片。

```python
from groupdocs.conversion import MarkdownSaveOptions

# Prepare options for the markdown output
opt = MarkdownSaveOptions()
```

*Why this matters*: 选项对象用于控制换行符、标题级别和图片处理等。如果不创建它，您将依赖库的默认行为，可能会遗漏图片。

## 步骤 3：配置资源处理以复制所有链接的资源

HTML 中引用的图片、CSS 文件和其他资产需要与 markdown 文件一起保存。将 `copy_resources` 设置为 `True` 可指示转换器将这些文件复制到 markdown 输出旁的文件夹中。

```python
from groupdocs.conversion import ResourceHandlingOptions

# Enable copying of linked resources (images, CSS, etc.)
opt.resource_handling_options = ResourceHandlingOptions()
opt.resource_handling_options.copy_resources = True
```

*Why this matters*: 如果跳过此步骤，生成的 markdown 将包含指向原始位置的图片 URL，移动 markdown 时常会失效。启用资源复制可确保 **markdown conversion with images** 离线可用。

## 步骤 4：使用配置好的选项将 HTML 文档转换为 Markdown

最后，调用 `Converter.convert` 方法，传入源文档、目标路径以及您准备好的选项。

```python
from groupdocs.conversion import Converter

# Perform the conversion
Converter.convert(doc, "YOUR_DIRECTORY/page.md", opt)
```

脚本完成后，您将在同一目录下看到 `page.md`，以及一个名为 `page_files`（或类似）的子文件夹，里面包含原始 HTML 中引用的所有图片和样式表。

### 预期输出

在任意文本编辑器中打开 `page.md`。您应该会看到类似以下的 markdown 语法，包含标题、段落、列表和图片链接：

```markdown
# Sample Title

Here is a paragraph from the original HTML.

![Alt text](page_files/image1.png)
```

所有图片现已本地存储，使 markdown 文件可移植。

## 完整、可运行的脚本

下面是将上述四个步骤组合在一起的完整脚本。将其保存为 `convert_html_to_md.py` 并使用 `python convert_html_to_md.py` 运行。

```python
# convert_html_to_md.py
# This script converts an HTML file to markdown and copies all linked resources.
# It demonstrates a reliable "convert html to markdown" workflow with images.

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, ResourceHandlingOptions, Converter

# ------------------------------------------------------------
# Configuration – adjust these paths for your environment
# ------------------------------------------------------------
INPUT_HTML = "YOUR_DIRECTORY/page.html"   # Path to the source HTML file
OUTPUT_MD = "YOUR_DIRECTORY/page.md"      # Desired markdown output path

def main():
    # Step 1: Load the HTML document
    doc = HTMLDocument(INPUT_HTML)

    # Step 2: Create markdown save options
    opt = MarkdownSaveOptions()

    # Step 3: Enable resource copying so images stay linked
    opt.resource_handling_options = ResourceHandlingOptions()
    opt.resource_handling_options.copy_resources = True

    # Step 4: Execute the conversion
    Converter.convert(doc, OUTPUT_MD, opt)

    print(f"Conversion complete! Markdown saved to: {OUTPUT_MD}")

if __name__ == "__main__":
    main()
```

运行脚本后，控制台会确认转换已完成：

```
Conversion complete! Markdown saved to: YOUR_DIRECTORY/page.md
```

## 处理边缘情况和常见问题

| Question | Answer |
|----------|--------|
| **如果 HTML 包含外部图片（例如 `https://example.com/img.png`）怎么办？** | 转换器会将这些图片下载到资源文件夹，只要 URL 可访问。如果服务器阻止请求，图片链接将保持不变；您可以手动下载并放入资源文件夹。 |
| **我可以自定义图片文件夹的名称吗？** | 可以。在转换前设置 `opt.resource_handling_options.resource_folder_name = "my_images"`。 |
| **如何批量转换多个 HTML 文件？** | 将转换逻辑放入循环，遍历文件路径列表。为提升效率，可复用同一个 `MarkdownSaveOptions` 实例。 |
| **有没有办法去除 CSS 样式？** | 设置 `opt.resource_handling_options.copy_css = False`。这会删除链接的 CSS 文件，同时保留 markdown 内容。 |
| **表格会被正确转换吗？** | 库会将 HTML 表格转换为 markdown 表格语法。复杂的嵌套表格可能需要手动调整。 |

## 可靠的 **export html as markdown** 最佳实践

1. **Validate the source HTML** – 结构不良的标记可能导致 markdown 输出缺失元素。请先使用 `html5lib` 或浏览器开发者工具清理 HTML。  
2. **Keep the output folder writable** – 脚本需要权限来创建资源子文件夹。  
3. **Version‑control the markdown** – 生成后，将 `.md` 文件提交到代码库；如果不需要二进制资产的版本历史，可将相应资源文件夹加入 `.gitignore`。  
4. **Test the markdown rendering** – 在 markdown 查看器（如 VS Code、Typora）中打开生成的文件，确保图片正常显示。

## 结论

您现在拥有一套稳健、可投入生产的 **convert HTML to markdown** 方法，能够在保留图片的同时完成 **save HTML page as markdown** 与 **export HTML as markdown** 的一键自动化。通过配置 `ResourceHandlingOptions`，脚本保证了跨平台可用的 **markdown conversion with images**。

接下来，您可以探索诸如 **how to convert HTML to markdown** 的大规模文档转换、将脚本集成到 CI 流水线，或扩展支持 PDF、DOCX 等其他输出格式。祝您转换愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 的其他功能，并在项目中尝试不同的实现方式。每个资源都提供完整的可运行代码示例和逐步解释。

- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [在 .NET 中使用 Aspose.HTML 将 HTML 转换为 Markdown](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown 转 HTML（Java）- 使用 Aspose.HTML 转换](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}