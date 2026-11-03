---
category: general
date: 2026-05-28
description: 使用 Aspose.HTML for Python 将 HTML 转换为 Markdown，并学习如何通过简易的逐步代码在 Markdown
  中嵌入图片。
draft: false
keywords:
- convert html to markdown
- embed images in markdown
- how to embed images markdown
- Aspose.HTML Python
- HTML to Markdown conversion
language: zh
og_description: 使用 Aspose.HTML Python 将 HTML 转换为 Markdown。本教程展示了如何在 Markdown 中嵌入图片，并解答了如何在
  Markdown 中嵌入图片的问题。
og_title: 将HTML转换为Markdown – 完整指南（含图片嵌入）
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Convert HTML to markdown using Aspose.HTML for Python and learn how
    to embed images in markdown with easy step‑by‑step code.
  headline: Convert HTML to Markdown – Complete Programming Guide
  type: TechArticle
- description: Convert HTML to markdown using Aspose.HTML for Python and learn how
    to embed images in markdown with easy step‑by‑step code.
  name: Convert HTML to Markdown – Complete Programming Guide
  steps:
  - name: Expected Output
    text: 'Open `embedded_images.md` in any text editor. You should see something
      like:'
  - name: 1. Relative Image Paths
    text: If your HTML uses relative paths like `src="images/pic.png"`, make sure
      the working directory when you run the script is the same as the HTML file’s
      folder, or provide an absolute path to the HTML file. The converter resolves
      the paths relative to the HTML document’s location.
  - name: 2. Large Images
    text: 'Embedding very large images can bloat the markdown file (think megabytes
      of Base64 text). If size becomes a concern, you can selectively embed only certain
      images:'
  - name: 3. Unsupported Formats
    text: 'Aspose.HTML supports PNG, JPEG, GIF, and SVG out of the box. If you have
      WebP or other exotic formats, convert them to PNG first:'
  type: HowTo
- questions:
  - answer: Yes. Aspose.HTML is cross‑platform because it runs on .NET Core under
      the hood. Just ensure you have the appropriate runtime (`dotnet` runtime) installed.
    question: Does this work on Windows, macOS, and Linux?
  - answer: Absolutely. Wrap the `convert_html_to_markdown` call in a loop that iterates
      over `os.listdir()` and filters for `.html` extensions.
    question: Can I convert a whole folder of HTML files at once?
  - answer: 'Set `resource_opts.embed_images = False`. The converter will emit standard
      markdown image links pointing to the original files. ## Wrap‑Up We’ve just covered
      **how to convert HTML to markdown** using Aspose.HTML for Python, and we’ve
      shown the exact steps to **embed images in markdown** so your docu'
    question: What if I need to keep the original image files instead of embedding
      them?
  type: FAQPage
tags:
- Python
- Aspose
- Markdown
- HTML
title: 将HTML转换为Markdown – 完整编程指南
url: /zh/python/general/convert-html-to-markdown-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为 Markdown – 完整编程指南

有没有想过如何 **将 HTML 转换为 markdown** 而不丢失任何内嵌图片？你并不是唯一有此困惑的人。许多开发者在 markdown 文件出现破损的图片链接，甚至完全缺失图片时，都会卡住。

好消息是？只需几行 Python 代码和 Aspose.HTML，就能把任何 HTML 页面转换为干净的 markdown *并且* 将所有引用的图片直接嵌入输出文件中。本文将从安装库到处理相对路径等边缘情况，完整演示整个过程。结束时，你将准确掌握 **如何在 markdown 中嵌入图片**，让文档保持可移植性。

## 前置条件 – 您需要的东西

- **Python 3.8+** – 任意近期版本均可。  
- **pip** – 标准的包管理器。  
- 需要互联网连接以获取 Aspose.HTML 包。  
- 一个示例 HTML 文件（`sample.html`），其中至少包含一个 `<img>` 标签。  

如果你已经具备这些，太好了。如果没有，打开终端并运行：

```bash
pip install aspose-html
```

该命令会获取 **Aspose.HTML for Python via .NET** 库，负责在后台完成繁重的工作。

> **小技巧：** 使用虚拟环境（`python -m venv venv`）来保持依赖整洁。

## 步骤 1：加载源 HTML 文档

首先，需要将转换器指向我们想要转换的 HTML 文件。把 `HTMLDocument` 看作一个包装器，它读取文件并在内存中构建 DOM 树。

```python
from aspose.html import Converter, HTMLDocument, MarkdownSaveOptions, ResourceHandlingOptions

# Load the HTML file – replace the path with your actual file location
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)

print(f"Loaded HTML document from: {html_path}")
```

> **为什么重要：** 加载文档后我们才能访问所有关联资源（样式表、脚本、图片）。如果跳过这一步，转换器将无从下手。

## 步骤 2：告诉转换器嵌入图片

默认情况下，Aspose.HTML 会把图片 URL 直接复制到 markdown 中，如果图片未在线托管，就会出现破链。要 **在 markdown 中嵌入图片**，我们需要在 `ResourceHandlingOptions` 上打开一个标志。

```python
# Create resource handling options
resource_opts = ResourceHandlingOptions()
resource_opts.embed_images = True   # This makes every <img> become a base64 data URI

print("Resource handling configured: embed_images =", resource_opts.embed_images)
```

> **工作原理：** 当 `embed_images` 为 `True` 时，转换器会读取每个图片文件，将其编码为 Base64，并以 data URI 的形式注入 markdown 图片语法（`![](data:image/png;base64,…)`）。这样 markdown 文件即可自包含。

## 步骤 3：配置 Markdown 保存选项

现在把资源设置与 markdown 输出配置结合起来。`MarkdownSaveOptions` 允许我们传入刚才定义的 `resource_opts`。

```python
# Set up Markdown save options and attach the resource handling configuration
markdown_opts = MarkdownSaveOptions()
markdown_opts.resource_handling_options = resource_opts

print("Markdown save options prepared with resource handling.")
```

> **你得到的好处：** 通过附加 `resource_handling_options`，转换器在保存阶段会自动应用图片嵌入规则。

## 步骤 4：执行转换

最后，调用静态的 `convert_html` 方法。它接受三个参数：已加载的 HTML 文档、保存选项以及目标 markdown 文件路径。

```python
# Destination markdown file – change the path as needed
output_md = "YOUR_DIRECTORY/embedded_images.md"

# Run the conversion
Converter.convert_html(html_doc, markdown_opts, output_md)

print(f"Conversion complete! Markdown saved to: {output_md}")
```

### 预期输出

在任意文本编辑器中打开 `embedded_images.md`。你应该会看到类似下面的内容：

```markdown
# Sample Title

Here is a paragraph with an embedded image:

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...)
```

`sample.html` 中的每个 `<img>` 标签现在都变成了 data URI，这意味着 markdown 文件可以随意移动而不会丢失图片。

## 处理常见的边缘情况

### 1. 相对图片路径

如果你的 HTML 使用了类似 `src="images/pic.png"` 的相对路径，请确保运行脚本时的工作目录与 HTML 文件所在文件夹相同，或为 HTML 文件提供绝对路径。转换器会相对于 HTML 文档的位置解析这些路径。

```python
# Example: using an absolute path to avoid confusion
import os
base_dir = os.path.abspath("YOUR_DIRECTORY")
html_doc = HTMLDocument(os.path.join(base_dir, "sample.html"))
```

### 2. 大图片

嵌入非常大的图片会导致 markdown 文件体积膨胀（想象几兆字节的 Base64 文本）。如果文件大小成为顾虑，你可以仅选择性地嵌入特定图片：

```python
def should_embed(image_path):
    # Embed only images smaller than 200KB
    return os.path.getsize(image_path) < 200 * 1024

resource_opts.embed_images = False  # Start with no embedding
resource_opts.embed_images_filter = should_embed
```

*（注意：`embed_images_filter` 是一个假想的钩子；如果你使用的库版本未提供该功能，需要自行在前置步骤中处理图片。）*

### 3. 不受支持的格式

Aspose.HTML 原生支持 PNG、JPEG、GIF 和 SVG。如果你有 WebP 或其他冷门格式，请先将其转换为 PNG：

```python
from PIL import Image
Image.open("image.webp").save("image.png")
```

## 完整工作脚本

把所有步骤整合起来，下面是一个可直接运行的脚本，保存为 `html_to_md.py`：

```python
# html_to_md.py
import os
from aspose.html import Converter, HTMLDocument, MarkdownSaveOptions, ResourceHandlingOptions

def convert_html_to_markdown(input_html: str, output_md: str):
    # Load HTML
    html_doc = HTMLDocument(input_html)

    # Configure resource handling to embed all images
    resource_opts = ResourceHandlingOptions()
    resource_opts.embed_images = True

    # Set markdown options with the resource handling config
    markdown_opts = MarkdownSaveOptions()
    markdown_opts.resource_handling_options = resource_opts

    # Perform conversion
    Converter.convert_html(html_doc, markdown_opts, output_md)

    print(f"✅ Conversion finished. Markdown with embedded images saved to: {output_md}")

if __name__ == "__main__":
    # Adjust these paths to match your environment
    base_dir = os.path.abspath("YOUR_DIRECTORY")
    html_path = os.path.join(base_dir, "sample.html")
    md_path   = os.path.join(base_dir, "embedded_images.md")

    convert_html_to_markdown(html_path, md_path)
```

运行方式：

```bash
python html_to_md.py
```

如果一切顺利，你会看到 ✅ 提示，并生成一个自动 **在 markdown 中嵌入图片** 的文件。

## 常见问题

**Q: 这在 Windows、macOS 和 Linux 上都能工作吗？**  
A: 能。Aspose.HTML 是跨平台的，因为它底层运行在 .NET Core 上。只需确保已安装相应的运行时（`dotnet` runtime）。

**Q: 能一次性转换整个文件夹的 HTML 文件吗？**  
A: 完全可以。将 `convert_html_to_markdown` 调用包装在循环中，遍历 `os.listdir()` 并筛选出 `.html` 扩展名即可。

**Q: 如果我想保留原始图片文件而不是嵌入它们怎么办？**  
A: 将 `resource_opts.embed_images = False`。转换器将生成指向原始文件的标准 markdown 图片链接。

## 总结

我们已经完整演示了如何使用 Aspose.HTML for Python **将 HTML 转换为 markdown**，并展示了 **在 markdown 中嵌入图片** 的全部步骤，使你的文档保持可移植性。从安装包、加载 HTML、配置资源处理到执行转换——每一步都像拼图一样紧密衔接。

现在，你可以把任何网页、博客文章或生成的报告转换为单个自包含的 markdown 文件。接下来，你可能想探索：

- 添加自定义 markdown 扩展（表格、脚注）。  
- 为静态站点生成器实现批量转换自动化。  
- 使用相同方法 **将 HTML 转换为其他格式**（PDF、DOCX）。

动手试一试，调整选项以适配你的项目，让嵌入的图片在任何分享环境中都保持清晰。

--- 

![将 HTML 转换为 Markdown 示例](/images/convert-html-to-markdown.png "显示嵌入图片的转换结果的截图")


## 相关教程

- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [在 .NET 中使用 Aspose.HTML 将 HTML 转换为 Markdown](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown 转 HTML（Java）- 使用 Aspose.HTML 转换](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}