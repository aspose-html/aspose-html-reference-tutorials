---
category: general
date: 2026-09-19
description: 学习在 Python 中将 HTML 转换为 Markdown。本教程展示如何快速将 HTML 保存为 Markdown，以及如何从 HTML
  生成 Markdown。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- save html as markdown
- generate markdown from html
- how to convert html
- html to markdown file
language: zh
lastmod: 2026-09-19
og_description: 使用 Python 将 HTML 转换为 Markdown。请按照本指南将 HTML 保存为 Markdown、从 HTML 生成
  Markdown，并创建 HTML 到 Markdown 的文件。
og_image_alt: Screenshot showing convert html to markdown script output
og_title: 在 Python 中将 HTML 转换为 Markdown – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Learn to convert HTML to Markdown in Python. This tutorial shows how
    to save HTML as Markdown and generate Markdown from HTML quickly.
  headline: How to convert HTML to Markdown with Python – step‑by‑step guide
  type: TechArticle
tags:
- Python
- HTML
- Markdown
- File conversion
title: 如何使用 Python 将 HTML 转换为 Markdown——一步步指南
url: /zh/python/general/how-to-convert-html-to-markdown-with-python-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 将 HTML 转换为 Markdown – 步骤指南

如果您需要 **将 HTML 转换为 Markdown**，本指南将带您完整了解整个过程。您将看到如何 **将 HTML 保存为 Markdown**、从 HTML 生成 Markdown，以及生成可用于静态站点生成器、文档流水线或任何偏好纯文本标记的工作流的 *html to markdown file*。

本教程涵盖了从安装所需库到处理嵌入图像和自定义格式等边缘情况的所有内容。完成后，您将拥有一个可直接运行的脚本，并清晰了解每一步的意义。

## 前置条件

在开始之前，请确保您具备：

- 已在机器上安装 Python 3.8 或更高版本。
- 对 Python 脚本有基本了解。
- 能够使用终端或命令提示符。
- 已安装 `aspose.html` 库（或任何兼容的 HTML‑to‑Markdown 包）。本教程使用 **Aspose.HTML for Python via .NET**，其中提供了代码示例中使用的 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 类。

> **专业提示：** 如果您更倾向于纯 Python 方案，可以将 `aspose.html` 替换为 `html2text` 包。整体流程保持不变。

## 第 1 步：安装转换库

首先，安装提供 `HTMLDocument`、`MarkdownSaveOptions` 和 `Converter` 的库。运行以下命令：

```bash
pip install aspose-html
```

该包捆绑了生成 **markdown from html** 所需的本地引擎，能够快速且高保真地完成转换。通常在标准宽带连接下，安装时间不超过一分钟。

## 第 2 步：加载源 HTML 文档

加载 HTML 文件是转换流水线中的第一个具体操作。`HTMLDocument` 类会解析文件并在内存中构建 DOM，随后转换器会遍历该 DOM 生成 Markdown。

```python
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

# Step 2: Load the source HTML document
html_path = "YOUR_DIRECTORY/input.html"
html_doc = HTMLDocument(html_path)
```

> **为何重要：** 通过创建 `HTMLDocument` 对象，您确保表格、列表和内联样式等复杂结构在转换前被正确解释。跳过此步骤会导致转换器直接读取原始文本，从而丢失格式。

## 第 3 步：配置 Markdown 保存选项

`MarkdownSaveOptions` 对象允许您微调输出格式。要生成 **Git‑flavored Markdown**，将 `formatter` 属性设为 `"GIT"`。这与 GitHub、GitLab、Bitbucket 等平台使用的语法相匹配。

```python
# Step 3: Create Markdown save options and select Git‑flavored Markdown
md_options = MarkdownSaveOptions()
md_options.formatter = "GIT"   # Equivalent to md_options.git = True
```

您还可以根据下游工具中 **save html as markdown** 的需求，调整 `preserve_links`、`code_block_style` 等其他设置。

## 第 4 步：将 HTML 转换为 Markdown 并保存结果

在文档已加载且选项已配置的情况下，调用静态 `convert_html` 方法。该方法读取 DOM、应用选定的格式化器，并写入输出文件。

```python
# Step 4: Convert the HTML to Markdown and save the result
output_path = "YOUR_DIRECTORY/output.md"
Converter.convert_html(html_doc, output_path, md_options)
print(f"Conversion complete – Markdown saved to {output_path}")
```

运行脚本后，您将在指定目录中看到一个名为 `output.md` 的新文件。打开它即可看到干净、兼容 Git 的 Markdown，准备好进行版本控制或发布。

## 第 5 步：验证生成的 markdown 文件

快速的完整性检查可以帮助您确认转换成功，并且 **html to markdown file** 包含预期内容。

```python
# Step 5: Load and print the first 10 lines of the generated Markdown
with open(output_path, "r", encoding="utf-8") as md_file:
    for i, line in enumerate(md_file):
        if i >= 10:
            break
        print(line.rstrip())
```

一个简单 HTML 页面典型的输出如下：

```
# Sample Document

This is a **bold** paragraph with a [link](https://example.com).

- Item 1
- Item 2
- Item 3
```

如果发现标题缺失或列表格式错误，请返回 **第 3 步**，尝试不同的 `formatter` 值（如 `"COMMONMARK"`、`"MARKDOWN_EXTRA"`）。

## 高级：处理图像和相对路径

当源 HTML 包含图像时，转换器可以将其嵌入为 data URI，或保留原始 `src` 属性。为保持 **generate markdown from html** 过程的轻量化，您可能希望将图像文件复制到平行文件夹并相应调整路径。

```python
md_options.image_handling = "COPY"  # Options: "EMBED", "COPY", "IGNORE"
md_options.images_folder = "YOUR_DIRECTORY/images"
```

转换完成后，Markdown 将以 `![Alt text](images/picture.png)` 的形式引用图像。此做法在后续 **save html as markdown** 于需要将资源放在专用文件夹的静态站点生成器中时表现良好。

## 完整脚本（可直接复制粘贴）

下面是完整、可运行的脚本，已整合所有讨论的步骤。将其保存为 `convert_html_to_md.py`，并使用 `python convert_html_to_md.py` 执行。

```python
# convert_html_to_md.py
# Complete script to convert an HTML file to a Git‑flavored Markdown file.

from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter
import os

def main():
    # Define input and output locations
    input_html = os.path.join("YOUR_DIRECTORY", "input.html")
    output_md = os.path.join("YOUR_DIRECTORY", "output.md")

    # 1️⃣ Load the HTML document
    html_doc = HTMLDocument(input_html)

    # 2️⃣ Set up Markdown options (Git‑flavored)
    md_options = MarkdownSaveOptions()
    md_options.formatter = "GIT"          # Git‑flavored Markdown
    md_options.image_handling = "COPY"    # Copy images to a folder
    md_options.images_folder = os.path.join("YOUR_DIRECTORY", "images")

    # 3️⃣ Perform the conversion
    Converter.convert_html(html_doc, output_md, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {output_md}")

    # 4️⃣ Quick verification – show first few lines
    print("\n--- First 10 lines of the generated Markdown ---")
    with open(output_md, "r", encoding="utf-8") as md_file:
        for i, line in enumerate(md_file):
            if i >= 10:
                break
            print(line.rstrip())

if __name__ == "__main__":
    main()
```

### 预期输出

运行脚本后会打印确认信息，并显示 Markdown 文件的前十行，如前文所示。生成的 `output.md` 可在任意文本编辑器中打开，在 VS Code 中预览，或提交到 Git 仓库。

## 常见问题与边缘情况处理

| Question | Answer |
|----------|--------|
| **如果 HTML 文件很大（> 10 MB）怎么办？** | `HTMLDocument` 类会流式读取输入，保持内存使用在适度范围。但如果出现 `MemoryError`，请考虑提升 Python 进程的内存限制。 |
| **能否转换 HTML 字符串而不是文件？** | 可以。使用 `HTMLDocument.from_string(html_string)`（或等价构造函数）在调用 `Converter.convert_html` 之前加载字符串。 |
| **如何保留原始 HTML 注释？** | 设置 `md_options.preserve_comments = True`。注释会以 HTML 注释形式（`<!-- … -->`）出现在 Markdown 文件中。 |
| **能否针对不同的 Markdown 方言？** | 将 `md_options.formatter` 改为 `"COMMONMARK"` 或 `"MARKDOWN_EXTRA"`，具体取决于目标平台。 |
| **需要单独安装 .NET 运行时吗？** | `aspose-html` 包已为大多数平台捆绑所需运行时。在 Linux 上，请确保已安装 `libgdiplus`（`sudo apt-get install libgdiplus`）。 |

## 结论

现在，您已经掌握了使用 Python **convert HTML to Markdown** 的方法，了解了如何 **save html as markdown**，以及如何通过细粒度的选项 **generate markdown from html**，并对格式和资源进行控制。该脚本展示了完整工作流——从加载源文件到生成干净的 *html to markdown file*，可用于版本控制或发布。

接下来，您可以探索诸如 **批量转换多个 HTML 文件**、将转换步骤集成到 CI/CD 流水线，或为 Hugo、Jekyll 等特定静态站点生成器自定义 Markdown 输出等相关主题。尝试不同的 `MarkdownSaveOptions` 设置，以使结果符合项目的风格指南。

祝您转换愉快！


## 接下来您可以学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方案。每个资源都提供完整的可运行代码示例和逐步解释。

- [在 .NET 中使用 Aspose.HTML 将 HTML 转换为 Markdown](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [在 Aspose.HTML for Java 中将 HTML 转换为 Markdown](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Markdown 转 HTML（Java） – 使用 Aspose.HTML 转换](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}