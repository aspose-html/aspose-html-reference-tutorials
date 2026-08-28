---
category: general
date: 2026-06-29
description: 使用 Python 快速将 HTML 转换为 Markdown。了解资源处理选项，保持图片为外部链接，生成干净的 .md 文件。
draft: false
keywords:
- convert html to markdown
- HTML to Markdown conversion
- resource handling options
- external image assets
- Python HTML conversion
language: zh
og_description: 使用 Python 在几分钟内将 HTML 转换为 Markdown。本指南涵盖资源处理、外部资产以及完整代码示例。
og_title: 将 HTML 转换为 Markdown – 完整的 Python 教程
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Convert HTML to Markdown quickly using Python. Learn resource handling
    options, keep images external, and generate clean .md files.
  headline: Convert HTML to Markdown – Step‑by‑Step Python Guide
  type: TechArticle
- description: Convert HTML to Markdown quickly using Python. Learn resource handling
    options, keep images external, and generate clean .md files.
  name: Convert HTML to Markdown – Step‑by‑Step Python Guide
  steps:
  - name: What the Settings Do
    text: '| Setting | Effect | |---------|--------| | `save_external_resources` |
      Saves each referenced image as a separate file instead of embedding it. | |
      `external_resources_folder` | Relative path (from the output markdown) where
      images will be written. |'
  - name: Expected Output
    text: '- `complex.md` – a markdown file containing clean headings, lists, and
      image references like `![Alt text](assets/image1.png)`. - `assets/` – a folder
      next to the markdown file containing every image that was referenced in the
      original HTML.'
  - name: 1️⃣ Images with Query Strings
    text: Some legacy sites append timestamps to image URLs (`pic.png?v=123`). Aspose
      strips the query part automatically, but if you notice missing images, double‑check
      the `external_resources_folder` permissions and ensure the source path is reachable.
  - name: 2️⃣ Inline Styles That Don't Translate
    text: 'Markdown doesn’t have a native concept for CSS. If your HTML relies heavily
      on `<style>` blocks, the converter will drop them. You can preserve critical
      styling by converting those sections to HTML blocks inside markdown:'
  - name: 3️⃣ Tables with Merged Cells
    text: Aspose does its best to flatten merged cells into markdown tables, but complex
      `rowspan`/`colspan` layouts may lose alignment. In those cases, consider exporting
      the table as an HTML snippet within the markdown, or manually edit the generated
      markdown.
  - name: 4️⃣ Large Documents and Memory Usage
    text: 'For massive HTML files (hundreds of megabytes), load the document in streaming
      mode:'
  type: HowTo
tags:
- Python
- HTML
- Markdown
- File conversion
title: 将HTML转换为Markdown – 步骤详解Python指南
url: /zh/python/general/convert-html-to-markdown-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为 Markdown – 完整 Python 教程

是否曾经需要 **convert HTML to Markdown**，却一直遇到图片链接失效或格式混乱的问题？你并不孤单。许多开发者在将遗留的网页内容迁移到干净、受版本控制的 markdown 仓库时，都会碰到这道墙。

在本教程中，我们将通过一个 **完整、可运行的示例**，一步步演示如何在保持图片为独立文件的前提下，将 HTML 转换为 Markdown。完成后，你将拥有可复用的脚本，了解每个设置背后的原因，并掌握如何针对内联 CSS 或嵌入式 SVG 等边缘情况进行微调。

---

## 本指南涵盖内容

- 安装合适的 Python 库（Aspose.HTML for Python）  
- 从磁盘加载 HTML 文档  
- 配置 **资源处理选项**，使图片保持为外部资源  
- 设置 **MarkdownSaveOptions** 并关联资源配置  
- 执行转换并验证输出  

无需任何 Aspose 经验；只需基本的 Python 环境和一文件夹的 HTML 文件。让我们开始吧。

---

## 前置条件

在编写代码之前，请确保你已经：

1. 安装了 **Python 3.9+**（推荐使用最新稳定版）。  
2. 具备 **pip** 可用于安装包。  
3. 拥有 **Aspose.HTML for Python via .NET** 包 (`aspose-html`) —— 它负责解析 HTML 并生成 Markdown。  
4. 准备好一个示例 HTML 文件（`complex.html`），其中包含图片、表格和少量自定义样式。  

如果缺少上述任意项，请在终端运行以下命令：

```bash
python -m pip install aspose-html
```

> **小技巧：** 使用虚拟环境（`python -m venv venv`）来保持依赖隔离。

---

## 第一步 – 加载源 HTML 文档

首先，我们告诉 Aspose 源文件所在的位置。`HTMLDocument` 类会将文件读取为类似 DOM 的结构，供转换器使用。

```python
from aspose.html import HTMLDocument

# Replace the path with the location of your HTML file
html_path = "YOUR_DIRECTORY/complex.html"
html_doc = HTMLDocument(html_path)
print(f"Loaded document: {html_doc.url}")
```

> **为什么重要：** 预先加载文档可以让库根据文件所在位置解析相对链接（如 `<img src="images/pic.png">`），这在后续 **convert HTML to markdown** 并保持图片外部化时至关重要。

---

## 第二步 – 配置资源处理以保持图片分离

如果直接调用转换器，Aspose 会将每张图片以 Base64 字符串嵌入到 markdown 中。这在干净的仓库里几乎从未是我们想要的。相反，我们启用 **外部图片资源**，并指定一个文件夹来保存这些图片。

```python
from aspose.html import ResourceHandlingOptions

resource_options = ResourceHandlingOptions()
resource_options.save_external_resources = True          # Keep images external
resource_options.external_resources_folder = "assets"    # Sub‑folder for assets

print("Resource handling configured:")
print(f"  Save external: {resource_options.save_external_resources}")
print(f"  Assets folder: {resource_options.external_resources_folder}")
```

### 设置的作用

| 设置 | 效果 |
|---------|--------|
| `save_external_resources` | 将每个引用的图片保存为单独的文件，而不是嵌入。 |
| `external_resources_folder` | 相对于输出 markdown 的路径，图片将写入此文件夹。 |

> **边缘情况：** 如果你的 HTML 包含 CSS `url()` 引用，这些也会被视为外部资源。若计划共享 markdown，请确保将 `assets` 文件夹加入版本控制。

---

## 第三步 – 将资源选项附加到 Markdown 保存设置

现在我们创建 `MarkdownSaveOptions` 实例，并把刚才定义的资源处理配置注入进去。该对象告诉转换器如何序列化文档。

```python
from aspose.html import MarkdownSaveOptions

markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options

print("Markdown save options ready.")
```

> **为何需要此步骤：** 若不附加 `resource_handling_options`，转换器会忽略我们的外部资源偏好，回退到默认的内联 Base64。这一步是实现 **HTML to Markdown conversion** 整洁化的关键链接。

---

## 第四步 – 执行转换

最后，调用静态方法 `Converter.convert_html`，提供源文档、markdown 选项以及目标路径。

```python
from aspose.html import Converter

output_md = "YOUR_DIRECTORY/complex.md"
Converter.convert_html(html_doc, markdown_options, output_md)

print(f"Conversion complete! Markdown saved to: {output_md}")
```

### 预期输出

- `complex.md` – 包含干净标题、列表以及类似 `![Alt text](assets/image1.png)` 的图片引用的 markdown 文件。  
- `assets/` – 与 markdown 文件同级的文件夹，存放原始 HTML 中引用的所有图片。

在任意 markdown 查看器（VS Code、Typora、GitHub）中打开 `complex.md`，你应当看到与原始 HTML 相同的视觉结构，只是以轻量的文本格式呈现。

---

## 常见问题处理

### 1️⃣ 带查询字符串的图片

一些旧站点会在图片 URL 后附加时间戳（`pic.png?v=123`）。Aspose 会自动去除查询部分，但若发现图片缺失，请检查 `external_resources_folder` 的权限，并确保源路径可访问。

### 2️⃣ 不会被转换的内联样式

Markdown 本身没有 CSS 概念。如果你的 HTML 大量依赖 `<style>` 块，转换器会将其丢弃。你可以通过在 markdown 中嵌入 HTML 块的方式保留关键样式：

```markdown
<div>
  <style>
    .highlight { background:#ff0; }
  </style>
  <p class="highlight">Important text</p>
</div>
```

### 3️⃣ 含合并单元格的表格

Aspose 会尽力将合并单元格展平成 markdown 表格，但复杂的 `rowspan`/`colspan` 布局可能会失去对齐。在这种情况下，考虑将表格导出为 markdown 中的 HTML 片段，或手动编辑生成的 markdown。

### 4️⃣ 大文档与内存使用

对于体积巨大的 HTML 文件（数百 MB），可以采用流式模式加载文档：

```python
html_doc = HTMLDocument(html_path, load_options=LoadOptions(streaming=True))
```

这会在稍微降低处理速度的前提下，显著降低 RAM 消耗。

---

## 完整脚本（可直接复制粘贴）

下面是整合了上述所有步骤和技巧的完整可运行脚本。将其保存为 `convert_html_to_md.py`，并相应调整路径。

```python
# convert_html_to_md.py
# -------------------------------------------------
# Python script to convert an HTML file to Markdown
# while keeping images as external assets.
# -------------------------------------------------

from aspose.html import (
    HTMLDocument,
    ResourceHandlingOptions,
    MarkdownSaveOptions,
    Converter,
)

def convert_html_to_markdown(
    html_path: str,
    markdown_path: str,
    assets_folder: str = "assets",
) -> None:
    """
    Convert HTML to Markdown with external image handling.

    Parameters
    ----------
    html_path : str
        Path to the source HTML file.
    markdown_path : str
        Destination path for the generated .md file.
    assets_folder : str, optional
        Sub‑folder (relative to markdown_path) where images will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(html_path)

    # Configure resource handling
    resource_opts = ResourceHandlingOptions()
    resource_opts.save_external_resources = True
    resource_opts.external_resources_folder = assets_folder

    # Set up markdown options and attach resource handling
    md_opts = MarkdownSaveOptions()
    md_opts.resource_handling_options = resource_opts

    # Perform the conversion
    Converter.convert_html(html_doc, md_opts, markdown_path)

    print(f"✅ Conversion finished! 🎉")
    print(f"   Markdown: {markdown_path}")
    print(f"   Images  : {assets_folder}/ (if any)")

if __name__ == "__main__":
    # -----------------------------------------------------------------
    # Update these paths before running the script
    # -----------------------------------------------------------------
    SOURCE_HTML = "YOUR_DIRECTORY/complex.html"
    DEST_MD    = "YOUR_DIRECTORY/complex.md"
    ASSETS_DIR = "assets"

    convert_html_to_markdown(SOURCE_HTML, DEST_MD, ASSETS_DIR)
```

使用以下命令运行：

```bash
python convert_html_to_md.py
```

你将看到与分步章节相同的确认信息，`assets` 文件夹也会出现在 `complex.md` 旁边。

---

## 额外：可视化概览

![convert html to markdown workflow diagram](/images/convert-html-to-markdown-diagram.png "Diagram showing the convert html to markdown process with resource handling")

*Alt text:* 展示从加载 HTML、配置资源处理到保存带外部资源的 Markdown 过程的流程图。

*(如果没有该图片，请自行想象一个简易流程图——alt 文本已满足 SEO 要求。)*

---

## 结论

现在，你已经掌握了一套 **完整、可投入生产的 HTML 转 Markdown 方法**，并通过显式配置 **资源处理选项**，实现图片的独立存放，这对于受版本控制的文档或静态站点生成器尤为理想。

接下来，你可以：

- 为整个 HTML 文件夹实现批量转换。  
- 扩展脚本，将失效链接替换为绝对 URL。  
- 将其集成到 CI 流水线，在每次提交时自动构建文档。  

欢迎随意实验——如果需要逆向操作，只需将 `MarkdownSaveOptions` 替换为 `HtmlSaveOptions`，或使用 `LoadOptions` 微调解析行为。

祝转换愉快，保持 markdown 整洁！ 🚀


## 接下来该学习什么？

以下教程与本指南紧密相关，能够帮助你进一步掌握 API 功能并探索在项目中的替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}