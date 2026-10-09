---
category: general
date: 2026-10-09
description: 学习如何在使用 Aspose.HTML 将 HTML 转换为 Markdown 时嵌入图像。包括将图像嵌入为 Base64 以及带有嵌入图像的
  Markdown。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed images
- convert html to markdown
- html to markdown python
- embed images as base64
- markdown with embedded images
language: zh
lastmod: 2026-10-09
og_description: 如何在 Python 中将 HTML 转换为 Markdown 时嵌入图像。本指南展示了将图像以 Base64 形式嵌入，并生成包含嵌入图像的
  Markdown。
og_image_alt: Screenshot of a Markdown file that contains embedded images generated
  by a Python HTML‑to‑Markdown conversion
og_title: 在 Python 中将 HTML 转换为 Markdown 时如何嵌入图片
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn how to embed images while converting HTML to Markdown in Python
    using Aspose.HTML. Includes embed images as Base64 and markdown with embedded
    images.
  headline: How to embed images when converting HTML to Markdown in Python
  type: TechArticle
- description: Learn how to embed images while converting HTML to Markdown in Python
    using Aspose.HTML. Includes embed images as Base64 and markdown with embedded
    images.
  name: How to embed images when converting HTML to Markdown in Python
  steps:
  - name: '**Resize images before conversion** – Use Pillow (`pip install pillow`)
      to shrink images to a reasonable resolution (e.g., 800 px width) before embedding.'
    text: '**Resize images before conversion** – Use Pillow (`pip install pillow`)
      to shrink images to a reasonable resolution (e.g., 800 px width) before embedding.'
  - name: '**Limit embedding to specific formats** – If you only need PNGs embedded,
      adjust `resource_opts` to filter by MIME type:'
    text: '**Limit embedding to specific formats** – If you only need PNGs embedded,
      adjust `resource_opts` to filter by MIME type:'
  - name: Import Aspose.HTML classes and create `MarkdownSaveOptions`.
    text: Import Aspose.HTML classes and create `MarkdownSaveOptions`.
  - name: Set `ResourceHandlingOptions.embed_resources` and `embed_images_as_base64`
      to `True`.
    text: Set `ResourceHandlingOptions.embed_resources` and `embed_images_as_base64`
      to `True`.
  - name: Attach those options to the markdown save settings.
    text: Attach those options to the markdown save settings.
  - name: Call `Converter.convert` with the source HTML and destination Markdown paths.
    text: Call `Converter.convert` with the source HTML and destination Markdown paths.
  type: HowTo
tags:
- Python
- Aspose.HTML
- Markdown conversion
- Image embedding
title: 在 Python 中将 HTML 转换为 Markdown 时如何嵌入图片
url: /zh/python/general/how-to-embed-images-when-converting-html-to-markdown-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中将 HTML 转换为 Markdown 时如何嵌入图片

如果您在进行 HTML‑to‑Markdown 转换时需要 **嵌入图片**，本指南提供了完整、可直接运行的解决方案。使用 Aspose.HTML for Python，您可以将图片以 Base‑64 字符串的形式嵌入，从而使生成的 Markdown 文件内联包含图片。这消除了链接失效的问题，使文档更加可移植。

除了嵌入图片，本教程还展示了如何 **将 HTML 转换为 Markdown**，涵盖 *html to markdown python* 工作流、配置 **embed images as Base64**，以及生成 **markdown with embedded images**，在任何 Markdown 查看器中均可正常显示。

阅读完本文后，您将拥有一个完整的脚本，能够：

* 从磁盘读取 HTML 文件。  
* 将所有引用的图片直接嵌入到 Markdown 输出中，使用 Base‑64 数据 URI。  
* 将最终的 Markdown 文件保存，随时可用于分发或版本控制。

## 前置条件

在开始之前，请确保您具备以下条件：

* 已安装 Python 3.8 或更高版本。  
* 拥有有效的 Aspose.HTML for Python 许可证（免费试用版可用于评估）。  
* 在虚拟环境中执行了 `pip install aspose-html`。  
* 一个引用本地或远程图片的 HTML 文件（`input.html`）。

如果缺少上述任意项，请立即安装，以免运行时出现错误。

## 第一步：设置 Aspose.HTML 环境

首先，导入所需的类并创建 `MarkdownSaveOptions` 实例。`MarkdownSaveOptions` 对象保存转换设置，包括后续将要配置的资源处理选项。

```python
# Step 1: Import required Aspose.HTML classes
from aspose.html import Converter, ResourceHandlingOptions, MarkdownSaveOptions

# Initialize Markdown save options (you can customize other settings here)
markdown_opts = MarkdownSaveOptions()
```

**此步骤的重要性：**  
`Converter` 承担核心转换工作，而 `MarkdownSaveOptions` 则告诉转换器如何处理图片、脚本和样式表等资源。如果不初始化 `markdown_opts`，就无法附加启用图片嵌入的资源处理配置。

## 第二步：配置资源处理以嵌入 Base64 图片

Aspose.HTML 提供 `ResourceHandlingOptions`。将 `embed_resources = True` 设置为 `True`，即可指示转换器将外部图片引用替换为 Base‑64 数据 URI。

```python
# Step 2: Create and configure resource handling options
resource_opts = ResourceHandlingOptions()
resource_opts.embed_resources = True          # Embed images directly in the output
resource_opts.embed_images_as_base64 = True   # Explicitly request Base64 encoding for images

# Attach the resource options to the markdown save options
markdown_opts.resource_handling_options = resource_opts
```

**此步骤的重要性：**  
当 `embed_resources` 为 `True` 时，转换器会扫描 HTML 中的 `<img>` 标签，获取每张图片，进行编码，并在 Markdown 中注入形如 `data:image/...;base64,` 的 URI。这样即可生成 **markdown with embedded images**，非常适合需要随源文件一起迁移的文档（例如 Git 仓库中的文档）。

## 第三步：执行 HTML 到 Markdown 的转换

现在可以调用 `Converter.convert`，传入源 HTML 路径、目标 Markdown 路径以及已配置好的 `markdown_opts`。

```python
# Step 3: Define source and destination paths
html_path = "YOUR_DIRECTORY/input.html"
markdown_path = "YOUR_DIRECTORY/with_images.md"

# Step 4: Convert HTML to Markdown, embedding images
Converter.convert(html_path, markdown_path, markdown_opts)
```

**此步骤的重要性：**  
`Converter.convert` 读取 HTML，依据您设置的选项处理所有资源，并写入包含相同视觉内容（包括图片）的 Markdown 文件，无需外部依赖。

## 第四步：验证生成的 Markdown

在任意 Markdown 预览器（VS Code、GitHub、Typora 等）中打开 `with_images.md`。您应当看到图片与原始 HTML 中的显示完全一致。图片链接大致如下：

```markdown
![Alt text](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...)
```

如果预览器显示图片破损，请检查以下事项：

* 原始 HTML 引用了可访问的图片（本地文件存在，远程 URL 可达）。  
* `embed_images_as_base64` 标志已设置为 `True`。  

## 第五步：处理大图片及性能考虑

嵌入非常大的图片会显著膨胀 Markdown 文件体积。以下两条实用技巧可帮助您控制大小：

1. **在转换前调整图片尺寸** – 使用 Pillow（`pip install pillow`）将图片缩至合适分辨率（例如宽度 800 px）后再嵌入。  
2. **仅对特定格式进行嵌入** – 若只需嵌入 PNG，可在 `resource_opts` 中按 MIME 类型过滤：

```python
resource_opts.allowed_image_formats = ["png"]  # Only embed PNG images
```

通过这些调整，您可以在保持可移植性的同时，使 Markdown 保持轻量。

## 常见坑及解决方案

| 问题 | 原因 | 解决办法 |
|------|------|----------|
| 图片显示为破损链接 | `embed_resources` 仍为 `False` | 确保 `resource_opts.embed_resources = True`。 |
| Markdown 文件大小 > 10 MB | 高分辨率大图片 | 缩小图片或仅嵌入必要的图片。 |
| 远程图片未被嵌入 | 网络超时或 URL 被阻止 | 检查网络连通性，或先下载图片到本地再转换。 |
| Base64 字符串出现异常字符 | 二进制文件读取不正确 | 确认图片文件未损坏且拥有正确的文件权限。 |

## 扩展方案：批量转换多个 HTML 文件

如果需要处理整个文件夹中的 HTML 文件，可将转换逻辑放入循环：

```python
import os

input_dir = "YOUR_DIRECTORY/html_files"
output_dir = "YOUR_DIRECTORY/markdown_output"

for filename in os.listdir(input_dir):
    if filename.lower().endswith(".html"):
        src_path = os.path.join(input_dir, filename)
        dst_path = os.path.join(output_dir, os.path.splitext(filename)[0] + ".md")
        Converter.convert(src_path, dst_path, markdown_opts)
        print(f"Converted {filename} → {os.path.basename(dst_path)}")
```

该代码片段演示了在大规模 **convert html to markdown** 时，仍保持 **embed images as base64** 行为的实现方式。

## 小结

现在您已经掌握了在使用 Python 将 HTML **转换为 Markdown** 时 **嵌入图片** 的方法。关键步骤如下：

1. 导入 Aspose.HTML 类并创建 `MarkdownSaveOptions`。  
2. 将 `ResourceHandlingOptions.embed_resources` 与 `embed_images_as_base64` 设置为 `True`。  
3. 将这些选项附加到 Markdown 保存设置中。  
4. 使用 `Converter.convert` 指定源 HTML 与目标 Markdown 路径。  

最终得到的 **markdown with embedded images** 可在任何环境下共享，而无需担心资源缺失。

## 后续步骤

* 探索其他 `ResourceHandlingOptions`（如 `embed_stylesheets`），以实现内联 CSS。  
* 将此工作流与静态站点生成器（例如 MkDocs）结合，构建文档流水线。  
* 尝试不同的图片格式与压缩等级，以在质量与文件大小之间取得平衡。

欢迎根据项目需求自行调整脚本，祝编码愉快！


## 接下来您应该学习什么？

以下教程涵盖了与本指南技术密切相关的主题，帮助您进一步掌握 API 功能并探索替代实现方式：

- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Convert markdown to html – Java guide with PDF output](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}