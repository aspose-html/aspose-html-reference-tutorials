---
category: general
date: 2026-05-31
description: 使用 Aspose.HTML 在 Python 中将 HTML 转换为 Markdown。了解如何将 HTML 转换为 Markdown、导出为
  Markdown，并保持图像完整。
draft: false
keywords:
- create markdown from html
- convert html to markdown
- html to markdown conversion
- export html as markdown
- convert html with images
language: zh
og_description: 使用 Aspose.HTML 将 HTML 转换为 Markdown。本指南展示了如何将 HTML 转换为 Markdown、保留图像，并仅用几行
  Python 代码将 HTML 导出为 Markdown。
og_title: 将HTML转换为Markdown – 步骤式Python教程
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create markdown from HTML in Python using Aspose.HTML. Learn how to
    convert html to markdown, export html as markdown, and keep images intact.
  headline: Create Markdown from HTML – Full Python Guide with Images
  type: TechArticle
- description: Create markdown from HTML in Python using Aspose.HTML. Learn how to
    convert html to markdown, export html as markdown, and keep images intact.
  name: Create Markdown from HTML – Full Python Guide with Images
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer. - An active Aspose.HTML for Python license (or a
      free trial). - A folder containing the HTML you want to transform. - Basic familiarity
      with Python''s import system.'
  - name: What if the HTML contains relative image paths?
    text: Aspose resolves relative URLs against the location of the source file. Just
      make sure `input.html` and its assets are in the same directory, or provide
      a base URL via `Document` constructor overloads.
  - name: Can I exclude certain resources (e.g., large PDFs)?
    text: 'Yes. `ResourceHandlingOptions` also exposes a `filter` callback where you
      can return `False` for resources you don’t want to download. Example:'
  - name: How do I change the Markdown flavor (GitHub vs. CommonMark)?
    text: '`MarkdownSaveOptions` includes a `markdown_version` property. Set it to
      `MarkdownVersion.GitHub` for GitHub‑flavored Markdown, or `MarkdownVersion.CommonMark`
      for the standard.'
  type: HowTo
tags:
- Python
- Aspose.HTML
- Document Conversion
title: 从 HTML 创建 Markdown – 完整的 Python 指南（含图片）
url: /zh/python/general/create-markdown-from-html-full-python-guide-with-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 HTML 创建 Markdown – 完整 Python 指南（含图片）

是否曾经需要 **create markdown from html**，却不确定如何保留图片？你并不是唯一的遇到这种情况的人。无论是迁移博客、构建静态站点生成器，还是仅仅需要一份干净的复制粘贴文档，将 HTML 转换为 Markdown 并保留资源都可能像在玩火把一样困难。

好消息是？使用 Aspose.HTML for Python，你只需几行代码就能 **convert html to markdown**，库会自动处理图片提取。下面将展示完整、可运行的脚本、每一步的意义以及避免常见陷阱的技巧。

> **Pro tip:** 如果只需要纯文本而不需要图片，可以省略 `ResourceHandlingOptions` 步骤——可以节省几毫秒的时间。

---

## 本教程涵盖内容

我们将逐步演示 **html to markdown conversion** 的每个阶段：

1. 安装 Aspose.HTML 包。  
2. 加载源 HTML 文件。  
3. 配置 `MarkdownSaveOptions` 以便将图片保存到文件夹。  
4. 执行转换并检查输出。  

完成后，你将能够 **export html as markdown**，并将所有外部资源整齐组织。无需额外脚本、无需手动复制粘贴——纯粹的 Python 实现。

### 前置条件

- Python 3.8 或更高版本。  
- 有效的 Aspose.HTML for Python 许可证（或免费试用）。  
- 包含待转换 HTML 的文件夹。  
- 对 Python 的 import 机制有基本了解。

如果上述任意一点不熟悉，请先暂停，使用 PyPI 安装库 (`pip install aspose-html`) 并从 Aspose 官网获取试用密钥。准备好后，继续下面的步骤。

---

## 第 1 步：安装 Aspose.HTML 并准备项目

在能够 **convert html with images** 之前，需要确保库已在你的环境中。

```bash
pip install aspose-html
```

安装完成后，创建一个小项目文件夹：

```
my_md_converter/
├─ input.html          # your source HTML
├─ md_resources/       # will hold extracted images
└─ convert.py          # the script we’ll write
```

将资源文件夹放在输出 Markdown 同级，便于下游工具（如 MkDocs 或 Jekyll）定位图片。

---

## 第 2 步：加载要转换的源文档

任何 **html to markdown conversion** 脚本的第一行都是将 HTML 文件加载到 `Document` 对象中。该对象抽象了 DOM，让 Aspose 处理所有繁重工作。

```python
# convert.py
from aspose.html import Document, Converter, MarkdownSaveOptions, ResourceHandlingOptions

# Step 1: Load the source document you want to convert
doc = Document("input.html")
```

为什么使用 `Document` 而不是自行打开文件？`Document` 会规范化 HTML，解析相对 URL，并为 Aspose 支持的任何输出格式做好准备——即使是标记不完整的页面，也能保证后续转换 **reliable**。

---

## 第 3 步：配置 Markdown 保存选项（启用图片提取）

如果跳过此步骤，Aspose 将生成一个仅引用原始 URL 的 Markdown 文件，这在移动文件时常常会失效。要 **export html as markdown** 并在本地保存每张图片，必须启用资源处理。

```python
# Step 2: Create Markdown save options
md_options = MarkdownSaveOptions()

# Step 3: Enable saving of external resources (e.g., images) and specify the folder
md_options.resource_handling_options = ResourceHandlingOptions()
md_options.resource_handling_options.save_external_resources = True
md_options.resource_handling_options.resources_folder = "md_resources"
```

需要注意的几点：

- `save_external_resources = True` 告诉 Aspose 下载 HTML 中引用的所有外部资源（图片、CSS、字体）。  
- `resources_folder` 定义这些资源的保存位置。保持路径简短且相对于输出文件，以免后期出现路径问题。

---

## 第 4 步：执行转换 – 从 HTML 到 Markdown

现在魔法开始发挥作用。静态的 `Converter.convert` 方法接受源 `Document`、目标文件路径以及我们刚配置的选项。

```python
# Step 4: Convert the document to Markdown, preserving images
Converter.convert(doc, "with_images.md", md_options)
```

脚本执行完毕后，你的项目目录中会出现两样东西：

1. `with_images.md` – `input.html` 的 Markdown 表示。  
2. `md_resources/` – 包含图片文件的文件夹（如 `image1.png`、`logo.jpg`），Markdown 会引用这些文件。

---

## 第 5 步：验证输出并根据需要微调

在任意编辑器中打开 `with_images.md`，你应该看到类似如下内容：

```markdown
# My Sample Page

Here is an example image:

![Sample Image](md_resources/image1.png)

And a paragraph of text...
```

如果图片链接失效，请再次确认 `md_resources` 与 `.md` 文件位于同一目录，并且文件夹中包含已下载的图片。偶尔，HTML 页面会使用 data‑URI 图片；Aspose 会自动解码，但生成的文件名可能显得怪异（例如 `image_0.png`）。如需更整洁的名称，可自行重命名。

---

## 为什么选择 Aspose.HTML 进行 HTML 到 Markdown 的转换？

市面上有 dozens of open‑source converters（如 `html2text` 或 `pandoc`），但 Aspose 在 **convert html with images** 时提供了几项显著优势：

| 功能 | Aspose.HTML | 常见开源方案 |
|------|-------------|--------------|
| **完整的 CSS 支持** | 能准确渲染带样式的表格、列表和内联 CSS。 | 往往会剥离样式，导致格式丢失。 |
| **自动资源下载** | 处理远程图片、字体，甚至 base64 data URI。 | 需要手动后处理。 |
| **高保真度** | 保持标题、代码块和引用块完整。 | 可能会扁平化复杂结构。 |
| **跨平台** | 在 Windows、Linux、macOS 上均可运行，无需额外依赖。 | 某些工具需要本地库。 |

如果你在构建商业产品，商业库的可靠性和技术支持可以为你省下大量调试时间。

---

## 边缘情况处理与常见问题

### HTML 中包含相对图片路径怎么办？

Aspose 会依据源文件所在位置解析相对 URL。只需确保 `input.html` 与其资源在同一目录，或通过 `Document` 构造函数的重载提供基准 URL。

### 能否排除某些资源（例如大型 PDF）？

可以。`ResourceHandlingOptions` 还提供了 `filter` 回调，你可以对不想下载的资源返回 `False`。示例：

```python
def filter(resource):
    return not resource.uri.lower().endswith('.pdf')

md_options.resource_handling_options.resource_filter = filter
```

### 如何切换 Markdown 方言（GitHub 与 CommonMark）？

`MarkdownSaveOptions` 包含 `markdown_version` 属性。将其设为 `MarkdownVersion.GitHub` 可生成 GitHub‑flavored Markdown，设为 `MarkdownVersion.CommonMark` 则生成标准 CommonMark。

```python
md_options.markdown_version = MarkdownVersion.GitHub
```

---

## 流畅工作流的专业技巧

- **批量处理**：将转换逻辑放入循环，可一次性处理 dozens of HTML 文件。  
- **命名一致性**：使用 `os.path.splitext` 生成与输入匹配的输出文件名（`example.html` → `example.md`）。  
- **清理工作**：转换完成后，可将 `md_resources` 文件夹压缩为 zip，便于分发。  
- **测试**：使用 `markdownlint` 等 linter 检查生成的 Markdown，捕获残留的 HTML 标签。

---

## 完整可运行示例

下面是可以直接复制到 `convert.py` 的 **full script**。它包含错误处理和一个简易 CLI，方便你指向任意 HTML 文件。

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
Create markdown from html – Aspose.HTML Python example
Author: Your Name (2026)
"""

import sys
import os
from aspose.html import Document, Converter, MarkdownSaveOptions, ResourceHandlingOptions, MarkdownVersion

def convert_html_to_md(source_path: str, output_md: str, resources_dir: str):
    """
    Convert an HTML file to Markdown, preserving images.
    """
    if not os.path.isfile(source_path):
        raise FileNotFoundError(f"Source file not found: {source_path}")

    # Load HTML
    doc = Document(source_path)

    # Set up Markdown options
    md_options = MarkdownSaveOptions()
    md_options.markdown_version = MarkdownVersion.GitHub  # optional, choose flavor

    # Enable resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.save_external_resources = True
    res_opts.resources_folder = resources_dir
    md_options.resource_handling_options = res_opts

    # Ensure the resources folder exists
    os.makedirs(resources_dir, exist_ok=True)

    # Perform conversion
    Converter.convert(doc, output_md, md_options)
    print(f"✅ Conversion complete: {output_md}")
    print(f"📁 Images saved to: {resources_dir}")

if __name__ == "__main__":
    # Simple CLI: python convert.py input.html output.md
    if len(sys.argv) != 3:
        print("Usage: python convert.py <input.html> <output.md>")
        sys.exit(1)

    input_html = sys.argv[1]
    output_md = sys.argv[2]
    resources_folder = os.path.join(os.path.dirname(output_md), "md_resources")

    try:
        convert_html_to_md(input_html, output_md, resources_folder)
    except Exception as e:
        print(f"❌ Error: {e}")
        sys.exit(1)
```

**预期输出**（在项目根目录运行）：

```
✅ Conversion complete: with_images.md
📁 Images saved to: md_resources
```

打开 `with_images.md`，即可看到一份干净的 Markdown 文件，且本地图片引用完整——这正是静态站点生成器或文档门户所需要的。

---

## 结论

现在，你已经掌握了使用 Python 与 Aspose.HTML **create markdown from html** 的完整端到端解决方案。我们从安装库、配置 `MarkdownSaveOptions` 进行图片提取，到处理资源过滤和 Markdown 方言选择，全部讲解完毕。拥有这段完整脚本后，你可以自动化大规模 **html to markdown conversion**，将其集成到 CI 流水线，或仅作一次性迁移工具使用。

准备好迎接下一个挑战了吗？尝试批量转换一批 HTML 文章，然后将生成的 Markdown 导入 MkDocs 等静态站点生成器。或者实验 `resource_filter` 回调，跳过大型 PDF 但仍获取 PNG 与 JPEG。前路无限，而这全都归功于 Aspose

## 接下来该学习什么？

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}