---
category: general
date: 2026-05-25
description: 使用 Python 将 HTML 转换为 Markdown。了解如何使用简单脚本将 HTML 转换为 Markdown 并保存为 Markdown。
draft: false
keywords:
- create markdown from html
- convert html to markdown
- how to convert html
- convert html document
- html to markdown python
language: zh
og_description: 使用 Python 快速将 HTML 转换为 Markdown。本指南展示了如何仅用几行代码将 HTML 转换为 Markdown。
og_title: 在 Python 中从 HTML 创建 Markdown – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Create markdown from html using Python. Learn how to convert html to
    markdown with a simple script and markdown save options.
  headline: Create Markdown from HTML in Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create markdown from html using Python. Learn how to convert html to
    markdown with a simple script and markdown save options.
  name: Create Markdown from HTML in Python – Step‑by‑Step Guide
  steps:
  - name: 1. What about tables and images?
    text: By default, tables are rendered using pipe (`|`) syntax, and images become
      Markdown image links that point to the same `src` attribute found in the HTML.
      If the image files aren’t in the same folder as the Markdown, you’ll need to
      adjust the paths manually or use the `image_folder` option in `Markdo
  - name: 2. How does the converter treat custom CSS classes?
    text: It strips them out unless you enable the `export_css` flag. This keeps the
      Markdown clean, but if you rely on class‑based styling later, you might want
      to keep the HTML fragments by setting `md_options.keep_html = True`.
  - name: 3. Is there a way to preserve code blocks with syntax highlighting?
    text: Yes—wrap your code in `<pre><code class="language-python">…</code></pre>`
      in the source HTML. The converter will translate that into fenced code blocks
      with the appropriate language identifier, which most static‑site generators
      understand.
  - name: 4. What if I need to **convert html to markdown** in a Jupyter notebook?
    text: Just paste the same code cells into a notebook cell. The only caveat is
      that the output path should be a location the notebook kernel can write to,
      like `"./quick.md"`.
  type: HowTo
tags:
- Python
- Markdown
- HTML
title: 使用Python将HTML转换为Markdown – 步骤指南
url: /zh/python/general/create-markdown-from-html-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中从 HTML 创建 Markdown – 步骤指南

是否曾经需要 **create markdown from html**，却不知从何入手？你并不孤单——许多开发者在尝试将网页内容迁移到静态站点生成器或文档仓库时都会遇到这个难题。好消息是，只需几行 Python 代码，你就可以 **convert html to markdown**，每次都得到干净、可读的 Markdown。

在本指南中，我们将覆盖你需要了解的全部内容：从安装合适的库，到完成核心功能的三步代码片段，再到排查最棘手的边缘案例。阅读完毕后，你将能够 **convert html document** 为 Markdown 文件，效果堪比手工编写。顺带我们还会分享一些在处理大型项目或自定义 HTML 结构时的 **convert html** 小技巧。

---

## 你需要的准备

在深入代码之前，先确认以下基础已就绪：

| 前置条件 | 为什么重要 |
|--------------|----------------|
| Python 3.8+  | 我们使用的库要求较新的解释器。 |
| `aspose-words` 包 | 这是能够同时理解 HTML 与 Markdown 的引擎。 |
| 可写入的目录 | 转换器会将 `.md` 文件写入磁盘。 |
| 基本的 Python 知识 | 方便你运行脚本并在以后进行调整。 |

如果其中任何一项有问题，请先暂停并先行安装缺失的部分。安装该包非常简单，只需运行 `pip install aspose-words`。无需额外的系统依赖——纯 Python 即可。

---

## 第一步：安装并导入所需库

首先，将 Aspose.Words for Python 库拉入你的环境。它是商业库，但提供免费评估模式，完全满足学习需求。

```bash
pip install aspose-words
```

接下来，导入我们需要的类。请注意，导入名称与前文示例中使用的对象名称保持一致。

```python
# Import the core conversion classes
from aspose.words import Document as HTMLDocument
from aspose.words import MarkdownSaveOptions, Converter
```

> **专业提示：** 如果你计划多次运行此脚本，建议创建虚拟环境（`python -m venv venv`），以保持依赖整洁。

---

## 第二步：从字符串创建 HTML 文档

转换器可以接受原始 HTML 字符串、文件路径，甚至是 URL。为了演示清晰，这里先使用一个包含段落和强调词的简单字符串。

```python
# Step 2: Build an in‑memory HTML document
html_content = "<p>Hello <em>world</em></p>"
html_doc = HTMLDocument(html_content)
```

此时 `html_doc` 已是 Aspose 视为完整文档的对象，尽管它只包含一小段 HTML。该抽象层使同一 API 能同时处理简单字符串和复杂 HTML 文件。

---

## 第三步：准备 Markdown 保存选项

`MarkdownSaveOptions` 类允许你微调输出——比如标题样式、代码块围栏，或是否保留 HTML 注释。默认设置已能满足大多数场景，但我们将演示如何切换几个实用标志。

```python
# Step 3: Configure how the Markdown will be generated
md_options = MarkdownSaveOptions()
# Example: force a Unix line ending style
md_options.line_break_type = MarkdownSaveOptions.LineBreakType.UNIX
```

完整的选项列表可在官方 Aspose 文档中查阅，默认情况下通常会生成干净、兼容 Git 的 Markdown。

---

## 第四步：将 HTML 文档转换为 Markdown 并保存

重头戏来了：`Converter.convert_html` 方法。它接受 HTML 文档、保存选项以及目标路径。请将 `"YOUR_DIRECTORY/quick.md"` 替换为你机器上的实际文件夹。

```python
# Step 4: Perform the conversion and write the file
output_path = "output/quick.md"   # make sure the folder exists
Converter.convert_html(html_doc, md_options, output_path)

print(f"✅ Markdown file created at: {output_path}")
```

运行脚本后会生成如下文件：

```markdown
Hello *world*
```

就这么简单——在不到一分钟的时间内 **create markdown from html**。输出会保留原始的强调标签，将 `<em>` 转换为 Markdown 中的 `*`。

---

## 处理文件时的 HTML 转换方式

上面的代码片段适用于字符串，但如果你手头有完整的 HTML 文件怎么办？同一 API 可以直接读取文件路径：

```python
# Load an HTML file from disk
html_file_path = "samples/example.html"
html_doc = HTMLDocument(html_file_path)

# Convert and save
Converter.convert_html(html_doc, md_options, "output/example.md")
```

这种模式易于扩展：你可以遍历一个 HTML 文件目录，逐个转换，并将结果导出到平行的文件夹结构中。

```python
import os

source_dir = "site/html"
target_dir = "site/markdown"

for filename in os.listdir(source_dir):
    if filename.endswith(".html"):
        src_path = os.path.join(source_dir, filename)
        dst_path = os.path.join(target_dir, filename.replace(".html", ".md"))
        doc = HTMLDocument(src_path)
        Converter.convert_html(doc, md_options, dst_path)
        print(f"Converted {filename} → {os.path.basename(dst_path)}")
```

现在，你拥有了一个 **convert html document** 工作流，能够轻松嵌入 CI 流水线或构建脚本。

---

## 常见问题与边缘案例

### 1. 表格和图片怎么办？

默认情况下，表格会使用管道（`|`）语法渲染，图片会转换为指向原始 HTML 中 `src` 属性的 Markdown 图片链接。如果图片文件不在 Markdown 同一文件夹，需要手动调整路径，或使用 `MarkdownSaveOptions` 中的 `image_folder` 选项。

### 2. 转换器如何处理自定义 CSS 类？

除非启用 `export_css` 标志，否则会剥离这些类。这保持了 Markdown 的简洁，但如果后续仍需基于类进行样式处理，可通过设置 `md_options.keep_html = True` 来保留 HTML 片段。

### 3. 能否保留带语法高亮的代码块？

可以——在源 HTML 中使用 `<pre><code class="language-python">…</code></pre>` 包裹代码。转换器会将其翻译为带相应语言标识的围栏代码块，大多数静态站点生成器都能识别。

### 4. 在 Jupyter Notebook 中 **convert html to markdown** 怎么做？

只需将相同的代码单元粘贴到 Notebook 的单元格中。唯一需要注意的是输出路径必须是 Notebook 内核可写入的位置，例如 `"./quick.md"`。

---

## 完整可运行示例（复制粘贴即用）

下面是一段自包含脚本，可保存为 `python convert_html_to_md.py` 并直接运行。它包含错误处理，并在输出文件夹不存在时自动创建。

```python
#!/usr/bin/env python3
"""
Create markdown from html – a complete, runnable example.
"""

import os
from aspose.words import Document as HTMLDocument
from aspose.words import MarkdownSaveOptions, Converter

def ensure_dir(path: str) -> None:
    """Create the directory if it doesn't exist."""
    os.makedirs(path, exist_ok=True)

def convert_string_to_md(html_string: str, output_file: str) -> None:
    """Convert a raw HTML string into a Markdown file."""
    html_doc = HTMLDocument(html_string)
    md_options = MarkdownSaveOptions()
    md_options.line_break_type = MarkdownSaveOptions.LineBreakType.UNIX
    Converter.convert_html(html_doc, md_options, output_file)

def main() -> None:
    # -------------------------------------------------
    # 1️⃣  Prepare input and output locations
    # -------------------------------------------------
    output_dir = "output"
    ensure_dir(output_dir)
    output_path = os.path.join(output_dir, "quick.md")

    # -------------------------------------------------
    # 2️⃣  The HTML we want to turn into Markdown
    # -------------------------------------------------
    html_source = "<p>Hello <em>world</em></p>"

    # -------------------------------------------------
    # 3️⃣  Perform the conversion
    # -------------------------------------------------
    try:
        convert_string_to_md(html_source, output_path)
        print(f"✅ Markdown created at: {output_path}")
    except Exception as e:
        print(f"❌ Conversion failed: {e}")

if __name__ == "__main__":
    main()
```

**预期输出（`output/quick.md`）：**

```
Hello *world*
```

运行脚本，打开生成的文件，即可看到上文展示的完整结果。

---

## 总结

我们已经演示了一种简洁、可投入生产的方式，使用 Python **create markdown from html**。关键要点如下：

* 安装 `aspose-words` 并导入相应类。  
* 将 HTML（字符串或文件）包装为 `HTMLDocument`。  
* 如有需要，使用 `MarkdownSaveOptions` 调整行结束符或其他偏好。  
* 调用 `Converter.convert_html` 并指定目标文件。  

这就是 **how to convert html** 的核心流程，干净且可重复。从这里你可以扩展为批量处理，集成到静态站点生成器，甚至嵌入到 Web 服务中。

---

## Where to


## 相关教程

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}