---
category: general
date: 2026-11-17
description: 使用 Python 将 HTML 转换为 Markdown（保留图像）——学习如何快速转换 HTML 并完整导出图像。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to convert html
- export html with images
- markdown conversion with images
language: zh
lastmod: 2026-11-17
og_description: 在 Python 中将 HTML 转换为带图片的 Markdown。本教程展示了如何在转换 HTML 的同时导出图片，为您提供完整的可直接运行的解决方案。
og_image_alt: Diagram showing convert html to markdown workflow with image extraction
og_title: 使用 Python 将 HTML 转换为带图片的 Markdown – 快速指南
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Convert HTML to markdown with images in Python – learn how to convert
    HTML quickly while exporting images intact.
  headline: Convert HTML to markdown with images in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Image extraction
title: 在 Python 中将 HTML 转换为带图片的 Markdown
url: /zh/python/general/convert-html-to-markdown-with-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 HTML 转换为带图像的 Markdown（Python）

如果您需要在 **将 HTML 转换为 markdown** 的同时保持图像为单独的文件，本指南将准确展示如何操作。您将获得一个完整、可运行的示例，能够处理外部资源，从而使生成的 markdown 正确引用原始图像。

导出带图像的 HTML 往往会让简单的转换器出错，因为它们要么丢失图像，要么将其嵌入为 base64 字符串。通过配置资源处理选项，您可以保留原始图像文件，并生成干净的 markdown，便于后续版本控制或编辑。

在本教程中，您将：

* 从磁盘加载 HTML 文档。  
* 配置转换器以 **导出带图像的 HTML** 为单独的文件。  
* 使用 **带图像的 markdown 转换** 选项将结果保存为 markdown。  

唯一的前提是使用最新版本的 Aspose.HTML for Python 库（或任何提供 `HTMLDocument`、`ResourceHandlingOptions`、`MarkdownSaveOptions` 和 `Converter` 的兼容 API）。您还需要 Python 3.8+ 并对输出文件夹拥有写入权限。

---

## 前置条件和安装

1. 安装 Aspose.HTML 包：

   ```bash
   pip install aspose-html
   ```

2. 验证安装：

   ```python
   import aspose.html as ah
   print(ah.__version__)   # should print the installed version, e.g., 22.9
   ```

> **专业提示：** 使用虚拟环境可以避免与其他项目的版本冲突。

---

## 第 1 步：加载源 HTML 文档

第一步是创建一个表示源文件的 `HTMLDocument` 对象。该对象会解析标记并构建 DOM 树，供转换器遍历。

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*为何重要* – 加载文档让库能够完全控制标记，进而解析相对 URL 并在后续应用资源处理。

---

## 第 2 步：配置外部资源处理

当您 **导出带图像的 HTML** 时，通常希望图像保存在 markdown 文件旁边，而不是嵌入其中。`ResourceHandlingOptions` 类允许您指定此行为。

```python
from aspose.html import ResourceHandlingOptions

resource_options = ResourceHandlingOptions()
resource_options.save_external_resources = True   # keep images as separate files
```

将 `save_external_resources` 设置为 `True` 会指示转换器将每个外部资源（图像、CSS、字体）复制到 markdown 输出旁边的文件夹。markdown 文件将包含指向这些副本的相对链接。

---

## 第 3 步：将资源处理配置附加到 markdown 选项

`MarkdownSaveOptions` 控制 markdown 转换的方式。通过为其分配 `resource_handling_options` 属性，您即可启用 **带图像的 markdown 转换** 功能。

```python
from aspose.html import MarkdownSaveOptions

markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

如果省略此步骤，转换器将会剥离图像引用或将其嵌入为 data URI，这会违背导出图像的初衷。

---

## 第 4 步：执行转换

最后，使用 `Converter.convert` 调用源文档、目标路径以及您准备好的选项。

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/sample.md"
Converter.convert(html_doc, output_path, markdown_options)
```

调用完成后，您将看到：

* `sample.md` – 原始 HTML 的 markdown 版本。  
* 一个名为 `sample_files`（或类似）的子文件夹，包含 HTML 中引用的所有图像。

---

## 完整可运行脚本

将所有部分组合在一起，即可得到一个可直接在命令行运行的脚本：

```python
# convert_html_to_markdown.py
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, MarkdownSaveOptions, Converter

def convert_html_to_markdown(html_file: str, markdown_file: str):
    """
    Convert an HTML file to markdown while exporting images as separate files.
    """
    # 1. Load the HTML document
    html_doc = HTMLDocument(html_file)

    # 2. Set up resource handling to keep images external
    res_opts = ResourceHandlingOptions()
    res_opts.save_external_resources = True

    # 3. Attach resource handling to markdown options
    md_opts = MarkdownSaveOptions()
    md_opts.resource_handling_options = res_opts

    # 4. Convert and save
    Converter.convert(html_doc, markdown_file, md_opts)
    print(f"Conversion complete: {markdown_file}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    src_html = os.path.abspath("YOUR_DIRECTORY/sample.html")
    dst_md   = os.path.abspath("YOUR_DIRECTORY/sample.md")

    convert_html_to_markdown(src_html, dst_md)
```

**预期输出**

```
Conversion complete: /absolute/path/YOUR_DIRECTORY/sample.md
```

执行后，在任意 markdown 编辑器中打开 `sample.md`。图像链接将显示为：

```markdown
![Alt text](sample_files/image1.png)
```

图像本身位于 `sample_files` 文件夹中，便于版本控制或进一步处理。

---

## 处理常见边缘情况

| 情况                              | 推荐做法 |
|-----------------------------------|----------|
| **缺少图像文件**                  | 转换器会记录警告并留下断开的链接。请在转换前确认所有 `<img src>` 属性指向可访问的资源。 |
| **指向项目文件夹之外的相对 URL**   | 使用 `ResourceHandlingOptions.base_url` 提供基准 URL，以便转换器正确解析路径。 |
| **包含大量图像的大型 HTML 文件**   | 如有 `resource_options.max_resource_size`（可用时），可将其设置为限制复制资源的大小。 |
| **非 PNG/JPEG 图像格式**          | 库会自动复制原始格式。请确保目标 markdown 查看器支持该格式（例如 SVG）。 |
| **写入权限错误**                  | 以适当的权限运行脚本，或选择您拥有写入权限的输出目录。 |

---

## 顺畅进行 **带图像的 markdown 转换** 的技巧

* 保持输出文件夹整洁：每次运行前删除 `*_files` 目录，以获得全新的图像集合。  
* 在原始 HTML 中使用有意义的 `alt` 属性；它们会自动成为 markdown 图像的说明文字。  
* 如果需要将图像嵌入为 base64（用于单文件 markdown），将 `resource_options.save_external_resources = False`。这与 **导出带图像的 HTML** 相反，但在邮件或文档嵌入时很有用。  
* 批量转换文件时，可将脚本包装在循环中，并调整 `resource_options.resource_folder` 以避免名称冲突。

---

## 常见问题

**问：这是否适用于缺少完整 `<html>` 包装的 HTML 片段？**  
答：是的。`HTMLDocument` 能够解析片段；转换器会将其视为

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整的可运行代码示例和逐步说明。

- [如何在 Python 中将 HTML 转换为 Markdown 并嵌入图像](/html/english/python/general/how-to-embed-images-in-html-to-markdown-conversion-using-pyt/)
- [将 HTML 转换为 Markdown – 完整指南（含 CSS 与图像）](/html/english/python/general/convert-html-to-markdown-complete-guide-with-css-images/)
- [使用 Aspose 将 HTML 转换为 Markdown – 完整 Python 指南](/html/english/python/general/convert-html-to-markdown-with-aspose-complete-python-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}