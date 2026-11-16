---
category: general
date: 2026-08-03
description: 如何在使用 Python 将 HTML 转换为 Markdown 时嵌入图像。学习在单个脚本中将 HTML 保存为 Markdown 并将图像以
  Base64 形式嵌入。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed images
- convert html to markdown
- how to convert html
- save html as markdown
- embed images as base64
language: zh
lastmod: 2026-08-03
og_description: 如何在使用 Python 将 HTML 转换为 Markdown 时嵌入图像。本指南展示了如何高效地将 HTML 保存为 Markdown
  并将图像以 Base64 形式嵌入。
og_image_alt: Screenshot showing how to embed images in HTML to Markdown conversion
  using Python
og_title: 如何在 HTML 到 Markdown 的转换中嵌入图片（Python）
schemas:
- author: Aspose
  dateModified: '2026-08-03'
  description: How to embed images while converting HTML to Markdown with Python.
    Learn to save HTML as Markdown and embed images as Base64 in a single script.
  headline: How to embed images in HTML to Markdown conversion using Python
  type: TechArticle
- description: How to embed images while converting HTML to Markdown with Python.
    Learn to save HTML as Markdown and embed images as Base64 in a single script.
  name: How to embed images in HTML to Markdown conversion using Python
  steps:
  - name: Load the source HTML document
    text: '```python from aspose.html import HTMLDocument'
  - name: Configure resource handling to embed images as Base64
    text: '```python from aspose.html import ResourceHandlingOptions'
  - name: Attach the resource options to the Markdown save options
    text: '```python from aspose.html import MarkdownSaveOptions'
  - name: Convert the HTML to Markdown and save the file
    text: '```python from aspose.html import Converter'
  - name: Expected output
    text: 'Open `embedded_images.md` in any Markdown viewer. You should see something
      like:'
  - name: Tips for reliable conversion
    text: '* **Validate the source HTML** – malformed tags can lead to unexpected
      Markdown. Use `HTMLDocument.validate()` if you suspect issues. * **Set `markdown_opts.escape_uri
      = False`** if you want to keep original URLs for images that are not embedded.
      * **Control line breaks** with `markdown_opts.force_n'
  type: HowTo
tags:
- Python
- Aspose.HTML
- Markdown
- Base64
- HTML conversion
title: 如何在使用 Python 将 HTML 转换为 Markdown 时嵌入图片
url: /zh/python/general/how-to-embed-images-in-html-to-markdown-conversion-using-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 HTML 转 Markdown 的过程中嵌入图片（使用 Python）

如果您需要在将 HTML 文件转换为 Markdown 时 **嵌入图片**，本教程提供了完整、可直接运行的解决方案。使用 Aspose.HTML for Python，您可以将 HTML 转换为 Markdown，将每张图片嵌入为 Base64 字符串，并通过一次调用保存结果。

将图片以 Base64 形式嵌入可消除外部文件依赖，这在您希望发布一个自包含的 Markdown 文档或将其存储在数据库中时尤为有用。下面的步骤同样涵盖了 **convert html to markdown**、**save html as markdown** 和 **embed images as base64**——全部在 Python 环境内完成。

> **先决条件**  
> • 已安装 Python 3.8+  
> • `aspose.html` 包（`pip install aspose-html`）  
> • 本地 HTML 文件（`sample.html`），其中至少包含一个 `<img>` 标签  

完成本指南后，您将能够运行脚本生成 `embedded_images.md`，该 Markdown 文件中的每张图片都已嵌入为 Base64 数据 URI。

![如何在 HTML 转 Markdown 的过程中嵌入图片（使用 Python）](https://example.com/placeholder-image.png){.align-center width=600 alt="展示如何在 HTML 转 Markdown 的过程中嵌入图片的截图"}

## 如何在 HTML 转 Markdown 的过程中嵌入图片

整个过程的核心是配置 **ResourceHandlingOptions**，让 Aspose.HTML 知道必须将图片嵌入，而不是复制为单独的文件。以下章节将工作流拆解为清晰、合乎逻辑的步骤。

### 步骤 1：加载源 HTML 文档

```python
from aspose.html import HTMLDocument

# Replace YOUR_DIRECTORY with the folder that holds your HTML file
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*此步骤的重要性：* `HTMLDocument` 解析 HTML 标记并构建 Aspose.HTML 可操作的 DOM。若不加载文档，转换器将无内容可处理。

### 步骤 2：配置资源处理以将图片嵌入为 Base64

```python
from aspose.html import ResourceHandlingOptions

resource_opts = ResourceHandlingOptions()
# Setting embed_images to True tells the converter to replace <img src="...">
# with a data URI that contains the image encoded in Base64.
resource_opts.embed_images = True
```

*此步骤的重要性：* 默认情况下，转换器会将图片文件复制到 Markdown 输出旁边。启用 `embed_images` 可确保每张图片成为自包含的 data URI，满足 **embed images as base64** 的需求。

### 步骤 3：将资源选项附加到 Markdown 保存选项

```python
from aspose.html import MarkdownSaveOptions

markdown_opts = MarkdownSaveOptions()
markdown_opts.resource_handling_options = resource_opts
```

*此步骤的重要性：* `MarkdownSaveOptions` 汇总所有转换设置。将 `resource_handling_options` 关联进去，可在 **convert html** 步骤中应用嵌入图片规则。

### 步骤 4：将 HTML 转换为 Markdown 并保存文件

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/embedded_images.md"
Converter.convert_html(html_doc, markdown_opts, output_path)
print(f"Markdown file created at: {output_path}")
```

*此步骤的重要性：* `Converter.convert_html` 执行核心工作——解析 DOM、将 HTML 标签翻译为 Markdown 语法并写入最终文件。由于我们已附加资源选项，每个 `<img>` 标签都会变为 `![alt text](data:image/...;base64,...)` 条目。

### 预期输出

在任意 Markdown 查看器中打开 `embedded_images.md`。您应看到类似如下内容：

```markdown
# Sample Document

Here is an image embedded directly in the file:

![Sample Image](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...)
```

`base64,` 之后的长串即为编码后的图片数据。无需外部图片文件。

## 使用 Aspose.HTML 将 HTML 转换为 Markdown

Aspose.HTML 支持广泛的 HTML 功能，包括表格、列表和代码块。当您 **convert html to markdown** 时，库会将每个 HTML 元素映射为对应的 Markdown：

| HTML 元素 | Markdown 输出 |
|-----------|----------------|
| `<h1>`    | `# Heading`    |
| `<ul>` / `<li>` | `- List item` |
| `<pre><code>` | ```` ```code``` ```` |
| `<img>`   | `![alt](url)`（当 `embed_images=True` 时为 data URI） |

由于转换在服务器端完成，您无需额外的 JavaScript 或第三方服务。该过程确定且在 Windows、macOS 和 Linux 上表现一致。

### 可靠转换的技巧

* **验证源 HTML** – 结构错误的标签可能导致意外的 Markdown。若怀疑问题，可使用 `HTMLDocument.validate()`。  
* **设置 `markdown_opts.escape_uri = False`**，如果希望保留未嵌入图片的原始 URL。  
* **使用 `markdown_opts.force_new_line = True`** 来严格控制换行行为。

## 使用自定义选项将 HTML 保存为 Markdown

如果您只想 **save html as markdown** 而不嵌入图片，只需将 `resource_opts.embed_images = False`。其余代码保持不变：

```python
resource_opts.embed_images = False  # Images will be saved as regular URLs
```

这种灵活性让您可以在不同部署场景下复用同一脚本——用于文档的自包含 Markdown，或用于网页发布的轻量 Markdown（外部资源）。

## 使用 ResourceHandlingOptions 将图片嵌入为 Base64

将图片嵌入为 Base64 会增加文件体积（约比原始二进制大 33 %），但可确保可移植性。请留意以下边缘情况：

| 场景 | 建议 |
|------|------|
| 大尺寸 PNG（>1 MB） | 在嵌入前压缩或缩放，以保持 Markdown 文件大小可控。 |
| SVG 图片 | SVG 本身已是 XML，您可以直接嵌入原始 SVG 标记或进行 Base64 编码，两者皆可。 |
| 远程图片（`http://…`） | Aspose.HTML 会下载图片、嵌入并在转换期间缓存。请确保网络可达。 |

**专业提示：** 若只需嵌入部分图片，可在设置 `embed_images = True` 前按文件扩展名或大小过滤。可通过自定义 `resource_opts.image_filter`（在新版 Aspose.HTML 中提供）实现。

## 完整脚本（可直接复制粘贴）

```python
# embed_html_to_markdown.py
# -------------------------------------------------
# Complete example: convert HTML to Markdown and embed images as Base64.
# -------------------------------------------------
from aspose.html import HTMLDocument, ResourceHandlingOptions, MarkdownSaveOptions, Converter

# 1️⃣ Load HTML
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)

# 2️⃣ Configure resource handling (embed images)
resource_opts = ResourceHandlingOptions()
resource_opts.embed_images = True  # Change to False to keep external image files

# 3️⃣ Attach options to MarkdownSaveOptions
markdown_opts = MarkdownSaveOptions()
markdown_opts.resource_handling_options = resource_opts

# 4️⃣ Convert and save
output_path = "YOUR_DIRECTORY/embedded_images.md"
Converter.convert_html(html_doc, markdown_opts, output_path)

print(f"✅ Markdown with embedded images saved to: {output_path}")
```

运行脚本：

```bash
python embed_html_to_markdown.py
```

您将看到确认信息，生成的 `embedded_images.md` 将包含所有图片的 Base64 数据 URI。

## 结论

现在，您已经掌握了在使用 Aspose.HTML for Python **convert html to markdown** 时 **如何嵌入图片** 的方法。教程涵盖了加载 HTML 文档、配置 `ResourceHandlingOptions` 以 **embed images as base64**、将这些选项附加到 `MarkdownSaveOptions`，以及最终调用 `Converter.convert_html` **save html as markdown**。

接下来您可以：

* 关闭图片嵌入以保留外部资源（`embed_images = False`）。  
* 尝试其他 `MarkdownSaveOptions`，如 `force_new_line` 或 `escape_uri`。  
* 将此脚本与批处理结合，自动转换多个 HTML 文件。

欢迎将代码迁移至 Aspose.HTML 支持的其他语言（C#、Java 等），或集成到 CI 流水线中，实现从 HTML 源生成文档的自动化。祝转换愉快！

## 接下来您可以学习什么？

以下教程与本指南紧密相关，进一步深化您在本章节展示的技术。每篇资源均提供完整可运行的代码示例和逐步解释，帮助您掌握更多 API 功能并探索在项目中的替代实现方案。

- [How to Save HTML as GIF with Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-gif/)
- [How to Convert HTML to JPEG Using Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}