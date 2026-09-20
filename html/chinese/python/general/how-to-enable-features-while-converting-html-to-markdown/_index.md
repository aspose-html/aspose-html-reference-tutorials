---
category: general
date: 2026-09-19
description: 如何在使用 Python 将 HTML 转换为 Markdown 时启用功能。学习将 HTML 文档转换并将其保存为 Markdown，精确控制功能。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable features
- convert html to markdown
- how to convert html
- convert html document
- save html as markdown
language: zh
lastmod: 2026-09-19
og_description: 如何在将 HTML 转换为 Markdown 时启用功能。本指南将逐步演示如何转换 HTML 文档并以细粒度控制将 HTML 保存为
  Markdown。
og_image_alt: Screenshot of Python code that enables features for HTML‑to‑Markdown
  conversion
og_title: 在将HTML转换为Markdown时如何启用功能
schemas:
- author: GroupDocs
  dateModified: '2026-09-19'
  description: How to enable features while converting HTML to Markdown using Python.
    Learn to convert HTML document and save HTML as Markdown with precise feature
    control.
  headline: How to enable features while converting HTML to Markdown
  type: TechArticle
tags:
- HTML conversion
- Markdown
- Python
title: 在将HTML转换为Markdown时如何启用功能
url: /zh/python/general/how-to-enable-features-while-converting-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在将 HTML 转换为 Markdown 时如何启用功能

如果您在转换过程中需要**如何启用功能**，本指南提供了完整且可运行的解决方案。您将确切看到如何将 HTML 转换为 Markdown，控制生成的 Markdown 功能，并在一次操作中将 HTML 保存为 Markdown。

示例使用流行的 **GroupDocs.Conversion** Python SDK，但这些概念同样适用于任何允许您配置功能集的库。完成本教程后，您可以转换 HTML 文档，仅保留链接和段落，避免不需要的表格、图像或代码块。

## 您将实现的目标

* **如何启用功能** 在 Markdown 保存选项中  
* 一个清晰的 **将 HTML 转换为 Markdown** 工作流  
* 能够 **如何转换 HTML** 并选择性输出  
* 一个可直接运行的脚本，**转换 HTML 文档** 并 **将 HTML 保存为 Markdown**  

### 前置条件

* 已安装 Python 3.8+  
* `groupdocs-conversion` 包（使用 `pip install groupdocs-conversion` 安装）  
* 已知目录中的示例 HTML 文件（`sample.html`）  

---

## 在 Markdown 转换中如何启用功能

第一步是创建一个 `MarkdownSaveOptions` 对象，并告诉转换器您想保留哪些元素。在本教程中，我们仅启用 **链接** 和 **段落**。

```python
# Import the required classes from the GroupDocs.Conversion SDK
from groupdocs.conversion import Converter, HTMLDocument, MarkdownSaveOptions

# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/sample.html")

# Step 2: Create Markdown save options
markdown_options = MarkdownSaveOptions()

# Step 3: Enable only the desired features (links and paragraphs)
markdown_options.features = ["Link", "Paragraph"]

# Step 4: Convert the HTML document to Markdown using the configured options
Converter.convert_html(html_doc, "YOUR_DIRECTORY/sample.md", markdown_options)
```

**为什么这样有效：**  
* `HTMLDocument` 包装源文件，以便转换器读取。  
* `MarkdownSaveOptions` 保存所有转换设置；`features` 列表是 **如何启用功能** 的关键属性。  
* 通过分配 `["Link", "Paragraph"]`，您告诉引擎仅生成 Markdown 链接（`[text](url)`）和普通段落，丢弃图像、表格和其他标记。  
* `Converter.convert_html` 执行实际的 **将 HTML 转换为 Markdown** 操作，并将结果写入 `sample.md`。

---

## 使用自定义选项转换 HTML 文档

如果您稍后需要添加更多功能标志——例如 `"Header"` 或 `"Bold"`——只需扩展列表：

```python
# Enable links, paragraphs, headers, and bold text
markdown_options.features = ["Link", "Paragraph", "Header", "Bold"]
```

对 `Converter.convert_html` 的相同调用现在将包含这些额外元素。这种模式让您 **如何转换 HTML** 以高度可配置的方式进行，而无需编写自定义解析器。

---

## 在特定文件夹中将 HTML 保存为 Markdown

`convert_html` 方法接受绝对或相对的输出路径。要在名为 `output` 的子文件夹中 **将 HTML 保存为 Markdown**，请调整第三个参数：

```python
output_path = "YOUR_DIRECTORY/output/sample.md"
Converter.convert_html(html_doc, output_path, markdown_options)
```

运行脚本会创建 `output` 目录（如果不存在），并将 Markdown 文件写入其中。这种做法可让您的源 HTML 与生成的 Markdown 整齐地组织在一起。

---

## 完整脚本，复制粘贴即可

下面是完整的程序，已准备好运行。将 `YOUR_DIRECTORY` 替换为包含 `sample.html` 的路径。

```python
# -*- coding: utf-8 -*-
"""
How to enable features while converting HTML to Markdown

This script demonstrates:
* loading an HTML document,
* configuring MarkdownSaveOptions to keep only links and paragraphs,
* converting the HTML to Markdown,
* and saving the result to a .md file.
"""

from pathlib import Path
from groupdocs.conversion import Converter, HTMLDocument, MarkdownSaveOptions

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = Path("YOUR_DIRECTORY")                # <— change this
HTML_FILE = BASE_DIR / "sample.html"
OUTPUT_MD = BASE_DIR / "sample.md"               # <— change if you want a different name

# ----------------------------------------------------------------------
# Step 1: Load the source HTML document
# ----------------------------------------------------------------------
html_doc = HTMLDocument(str(HTML_FILE))

# ----------------------------------------------------------------------
# Step 2: Create and configure Markdown save options
# ----------------------------------------------------------------------
markdown_options = MarkdownSaveOptions()
# Enable only the desired features (links and paragraphs)
markdown_options.features = ["Link", "Paragraph"]

# ----------------------------------------------------------------------
# Step 3: Perform the conversion and write the Markdown file
# ----------------------------------------------------------------------
Converter.convert_html(html_doc, str(OUTPUT_MD), markdown_options)

print(f"Conversion complete. Markdown saved to: {OUTPUT_MD}")
```

**预期输出**（打印到控制台）：

```
Conversion complete. Markdown saved to: /path/to/YOUR_DIRECTORY/sample.md
```

打开 `sample.md`，您将仅看到 Markdown 链接和普通段落，例如：

```markdown
This is a paragraph with a [link](https://example.com) inside.
Another paragraph follows without any images or tables.
```

所有其他 HTML 元素已被省略，因为 **如何启用功能** 将输出限制为这两种选定类型。

---

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| *如果 HTML 文件不包含链接怎么办？* | 转换器仍会写入段落；输出将只包含没有链接语法的纯文本。 |
| *我可以禁用所有功能吗？* | 将 `markdown_options.features = []` 设置为一个空列表会生成空的 Markdown 文件。仅在测试时使用此设置。 |
| *SDK 如何处理无效的 HTML？* | 解析器会尝试在应用功能过滤器之前清理错误的标记。错误会被记录，但不会中止转换。 |
| *是否可以保留图像而删除表格？* | 可以。将 `markdown_options.features = ["Link", "Paragraph", "Image"]`。功能列表是累加的，而非排他的。 |
| *如果需要转换文件夹中的多个文件怎么办？* | 将转换逻辑包装在遍历 `Path.glob("*.html")` 的循环中。相同的 **如何启用功能** 配置可以在每个文件中重复使用。 |

**专业提示：** 在处理大批量时，只实例化一次 `MarkdownSaveOptions` 并重复使用。这可以减少对象创建开销，并保持 **将 HTML 转换为 Markdown** 流程的高速。

---

## 结论

现在您已经了解了在 **将 HTML 转换为 Markdown** 时 **如何启用功能**，以及如何使用选择性输出 **如何转换 HTML**，并使用简洁的 Python 脚本 **转换 HTML 文档** 并 **将 HTML 保存为 Markdown**。通过配置 `MarkdownSaveOptions.features`，您可以完全控制最终文件中出现的 Markdown 元素。

### 下一步

* 探索额外的功能标志，如 `"Header"`、`"Bold"` 和 `"Italic"`，以丰富您的 Markdown 输出。  
* 将此脚本与文件监视器（例如 `watchdog`）结合，以在新 HTML 文件到达时自动转换。  
* 查看 [GroupDocs.Conversion Python SDK 文档](https://github.com/groupdocs-conversion/GroupDocs.Conversion-Examples)，了解 PDF 转 Markdown 或 DOCX 转 HTML 等高级场景。

随意尝试不同的功能集，并与社区分享您的发现。祝您转换愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方式。

- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Markdown 转 HTML Java - 使用 Aspose.HTML 转换](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [如何在 Aspose HTML 中启用 JavaScript – 加载 HTML 并获取文本](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}