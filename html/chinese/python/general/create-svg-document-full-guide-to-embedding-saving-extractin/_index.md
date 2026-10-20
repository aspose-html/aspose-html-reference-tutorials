---
category: general
date: 2026-06-29
description: 一步一步创建 SVG 文档，学习如何在 HTML 中嵌入 SVG，保存 SVG 文件并高效提取 SVG——完整教程。
draft: false
keywords:
- create svg document
- embed svg in html
- save svg file
- how to embed svg
- how to extract svg
language: zh
og_description: 使用 Python 创建 SVG 文档，将 SVG 嵌入 HTML，保存 SVG 文件，并学习如何提取 SVG——一篇完整的综合教程。
og_title: 创建 SVG 文档 – 嵌入、保存与提取指南
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Create SVG document step‑by‑step and learn how to embed SVG in HTML,
    save SVG file and extract SVG efficiently – a complete tutorial.
  headline: Create SVG Document – Full Guide to Embedding, Saving & Extracting SVG
  type: TechArticle
- description: Create SVG document step‑by‑step and learn how to embed SVG in HTML,
    save SVG file and extract SVG efficiently – a complete tutorial.
  name: Create SVG Document – Full Guide to Embedding, Saving & Extracting SVG
  steps:
  - name: Load the HTML page we just saved.
    text: Load the HTML page we just saved.
  - name: Locate the `<svg>` element via `get_element_by_tag_name`.
    text: Locate the `<svg>` element via `get_element_by_tag_name`.
  - name: Pull its `outer_html`, which includes the opening and closing `<svg>` tags
      plus all child nodes.
    text: Pull its `outer_html`, which includes the opening and closing `<svg>` tags
      plus all child nodes.
  - name: Feed that string back into `SVGDocument.from_string` to get a proper SVGDocument
      object.
    text: Feed that string back into `SVGDocument.from_string` to get a proper SVGDocument
      object.
  - name: Finally, **save SVG file** (`extracted.svg`) using the same `SVGSaveOptions`.
    text: Finally, **save SVG file** (`extracted.svg`) using the same `SVGSaveOptions`.
  type: HowTo
tags:
- SVG
- Python
- Aspose.HTML
title: 创建 SVG 文档 – 完整指南：嵌入、保存与提取 SVG
url: /zh/python/general/create-svg-document-full-guide-to-embedding-saving-extractin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 SVG 文档 – 完整指南：嵌入、保存与提取 SVG

是否曾想过在不打开图形编辑器的情况下**以编程方式创建 SVG 文档**？你并不孤单。无论是为 Web 应用需要一个动态徽标，还是为报告快速生成图表，实时生成 SVG 都能为你节省大量手工工作时间。在本教程中，我们将一步步演示如何创建 SVG 文档、将该 SVG 嵌入 HTML 页面、保存 SVG 文件，最后再将 SVG 提取出来——全部使用 Aspose.HTML for Python。

我们还会简要说明每一步背后的*原因*，帮助你将该模式迁移到自己的项目中。完成后，你将拥有一个可在 Windows、macOS 或 Linux 上运行的可复用代码片段，并了解如何为更复杂的图形进行定制。

## 前置条件

- 已安装 Python 3.8+  
- 已安装 `aspose.html` 包（`pip install aspose-html`）  
- 对 SVG 标记有基本了解（只需一个矩形即可开始）  
- 一个用于存放生成文件的空文件夹（代码中请将 `YOUR_DIRECTORY` 替换为实际路径）

没有繁重的依赖，也不需要外部 CLI 工具——纯 Python 即可。

## 第一步：创建 SVG 文档 – 基础

我们首先需要一个干净的 SVG 画布。可以把 SVG 文档看作一个基于矢量的空白页，能够在其上绘制形状、文字，甚至嵌入图像。使用 Aspose.HTML 的 `SVGDocument` 类可以让 XML 处理保持整洁。

```python
from aspose.html import SVGDocument, SVGSaveOptions

# Step 1: Create an SVG document containing a blue rectangle
svg_doc = SVGDocument()
svg_doc.root.append_child(
    svg_doc.create_element(
        "rect",
        {
            "x": "10",
            "y": "10",
            "width": "100",
            "height": "50",
            "fill": "blue",
        },
    )
)

# Save the raw SVG so you can inspect it later
svg_doc.save("YOUR_DIRECTORY/logo.svg", SVGSaveOptions())
```

**为什么这样做很重要：**  
- `svg_doc.root` 直接提供对 `<svg>` 根元素的访问。  
- `create_element` 用于构建带属性的 `<rect>` 节点——无需手动拼接字符串，避免生成错误的 XML。  
- 使用 `SVGSaveOptions()` 保存时会生成干净的 `logo.svg` 文件，任何浏览器都能立即渲染。

**预期输出：** 在浏览器中打开 `logo.svg`，你会看到一个蓝色矩形，距离左上角 10 px。

![Diagram showing SVG embedded in HTML](/images/svg-embed-diagram.png "Diagram showing SVG embedded in HTML")

*图片替代文字：* 在 HTML 中嵌入 SVG 的示意图

## 第二步：如何嵌入 SVG – 将矢量图形放入 HTML

现在我们已有 SVG 文件，接下来自然会问*如何将 SVG 直接嵌入 HTML 页面*。嵌入可以避免额外的 HTTP 请求，并且可以像对待其他 DOM 元素一样使用 CSS 对 SVG 进行样式设置。

```python
from aspose.html import HTMLDocument

# Step 2: Embed the SVG markup into an HTML document
html_doc = HTMLDocument()
svg_element = html_doc.create_element("svg")
# Copy raw SVG markup from the previously created document
svg_element.inner_html = svg_doc.root.inner_html
html_doc.body.append_child(svg_element)

# Save the HTML page that now contains the SVG
html_doc.save("YOUR_DIRECTORY/page_with_svg.html")
```

**为什么选择嵌入而不是链接？**  
- **性能提升：** 只加载一个文件，而不是两个独立请求。  
- **样式能力：** CSS 可以直接定位内部的 SVG 元素（`svg rect { … }`）。  
- **可移植性：** HTML 页面成为一个自包含的示例，分享时无需额外资源。

在浏览器中打开 `page_with_svg.html`，你会看到同样的蓝色矩形，只是它现在位于 HTML DOM 中。检查页面时会看到一个包含该矩形的 `<svg>` 元素。

## 第三步：保存 SVG 文件 – 持久化嵌入的图形

你可能会认为在第 1 步已经保存了 SVG，但有时我们是即时生成 SVG 并仅临时嵌入。如果之后需要一个永久的 `.svg` 文件，可以**直接从 HTML 文档中保存 SVG 文件**，而无需再次引用原始文件。

```python
# Step 3 (alternative): Save the embedded SVG as a separate file
embedded_svg_html = HTMLDocument("YOUR_DIRECTORY/page_with_svg.html") \
    .get_element_by_tag_name("svg") \
    .outer_html

# Re‑create an SVGDocument from the extracted markup and save it
SVGDocument.from_string(embedded_svg_html).save("YOUR_DIRECTORY/extracted.svg", SVGSaveOptions())
```

**这里发生了什么？**  
1. 加载我们刚才保存的 HTML 页面。  
2. 通过 `get_element_by_tag_name` 定位 `<svg>` 元素。  
3. 获取其 `outer_html`，其中包括开闭 `<svg>` 标签以及所有子节点。  
4. 将该字符串重新传入 `SVGDocument.from_string`，得到正式的 `SVGDocument` 对象。  
5. 最后，使用相同的 `SVGSaveOptions` **保存 SVG 文件**（`extracted.svg`）。

打开 `extracted.svg`，你会看到完全相同的矩形——这表明提取过程完美保留了矢量数据。

## 第四步：如何提取 SVG – 从 HTML 中抽取矢量数据

有时你会从第三方获取 HTML 内容，需要原始的 SVG 进行后续处理（例如转换为 PNG、在 Illustrator 中编辑）。上面的代码已经演示了*如何提取 SVG*，下面我们把它封装成一个可复用的函数。

```python
def extract_svg_from_html(html_path: str, output_svg_path: str) -> None:
    """
    Reads an HTML file, finds the first <svg> element,
    and writes it to a separate .svg file.
    """
    html_doc = HTMLDocument(html_path)
    svg_element = html_doc.get_element_by_tag_name("svg")
    if svg_element is None:
        raise ValueError("No <svg> element found in the provided HTML.")
    
    svg_markup = svg_element.outer_html
    SVGDocument.from_string(svg_markup).save(output_svg_path, SVGSaveOptions())
```

**为什么要封装成函数？**  
- **可复用性：** 对任意 HTML 输入调用，无需重复编写代码。  
- **错误处理：** 当 HTML 中缺少 SVG 时，`ValueError` 会给出明确提示，这是常见的边界情况。  
- **可维护性：** 将来若需要提取多个 SVG，只需在此处统一修改。

### 使用辅助函数

```python
extract_svg_from_html(
    "YOUR_DIRECTORY/page_with_svg.html",
    "YOUR_DIRECTORY/final_extracted.svg"
)
```

运行脚本后，`final_extracted.svg` 将出现在你的文件夹中，准备好用于后续任务，如光栅化或动画制作。

## 常见坑点与专业技巧

| 坑点 | 产生原因 | 解决方案 |
|--------|----------------|-----|
| **缺少命名空间** | 某些 SVG 需要 `xmlns` 属性，否则浏览器会把它当作普通 XML 处理。 | 手动创建根节点时，确保 `svg_doc.root.set_attribute("xmlns", "http://www.w3.org/2000/svg")`。 |
| **多个 `<svg>` 标签** | HTML 中若包含多个 SVG，`get_element_by_tag_name` 只返回第一个。 | 使用 `get_elements_by_tag_name("svg")` 进行遍历，并根据需要处理每个索引。 |
| **SVG 字符串过大** | 复杂的 SVG 标记在作为字符串加载时可能触及内存限制。 | 若源文件非常大，使用流式 API（`SVGDocument.load`）读取。 |
| **文件路径问题** | 使用相对路径时，脚本在不同工作目录下运行会导致 `FileNotFoundError`。 | 推荐使用 `os.path.join(os.path.abspath(os.path.dirname(__file__)), "YOUR_DIRECTORY", "file.svg")`。 |

## 完整端到端示例

将所有内容整合在一起，下面是一段可以直接放入项目并立即运行的脚本：

```python
import os
from aspose.html import SVGDocument, HTMLDocument, SVGSaveOptions

BASE_DIR = os.path.abspath("YOUR_DIRECTORY")

def ensure_dir(path: str) -> None:
    os.makedirs(path, exist_ok=True)

def create_svg() -> str:
    svg_doc = SVGDocument()
    svg_doc.root.append_child(
        svg_doc.create_element(
            "rect",
            {
                "x": "10",
                "y": "10",
                "width": "100",
                "height": "50",
                "fill": "blue",
            },
        )
    )
    svg_path = os.path.join(BASE_DIR, "logo.svg")
    svg_doc.save(svg_path, SVGSaveOptions())
    return svg_path

def embed_svg(svg_path: str) -> str:
    # Load the freshly saved SVG to reuse its markup
    svg_doc = SVGDocument(svg_path)
    html_doc = HTMLDocument()
    svg_element = html_doc.create_element("svg")
    svg_element.inner_html = svg_doc.root.inner_html
    html_path = os.path.join(BASE_DIR, "page_with_svg.html")
    html_doc.save(html_path)
    return html_path

def extract_svg(html_path: str) -> str:
    html_doc = HTMLDocument(html_path)
    svg_element = html_doc.get_element_by_tag_name("svg")
    if not svg_element:
        raise RuntimeError("No SVG found in HTML.")
    extracted_path = os.path.join(BASE_DIR, "extracted.svg")
    SVGDocument.from_string(svg_element.outer_html).save(
        extracted_path, SVGSaveOptions()
    )
    return extracted_path

if __name__ == "__main__":
    ensure_dir(BASE_DIR)
    svg_file = create_svg()
    html_file = embed_svg(svg_file)
    extracted_svg = extract_svg(html_file)
    print(f"SVG created: {svg_file}")
    print(f"HTML with embedded SVG: {html_file}")
    print(f"Extracted SVG saved as: {extracted_svg}")
```

运行该脚本后会打印出三个文件的位置，确认我们成功实现了**创建 SVG 文档**、**在 HTML 中嵌入 SVG**、**保存 SVG 文件**以及**提取 SVG**——全部一步完成。

## 小结

我们首先学习了如何使用一个简单的矩形**创建 SVG 文档**，随后探讨了*如何在 HTML 页面中嵌入 SVG*以提升加载速度并简化样式设置。接着介绍了**保存 SVG 文件**的两种方式：直接保存以及从嵌入源保存，最后演示了*如何从 HTML 中提取 SVG*的清晰辅助函数。完整可运行的示例将所有步骤串联起来，为任何矢量图形自动化任务提供了即用的工具箱。

## 接下来可以做什么？

- **使用 CSS 样式化：** 在 `<svg>` 内部添加 `<style>` 块，实现悬停变色等交互。  
- **动态内容：** 通过程序化创建 `<path>` 元素，根据数据生成图表或图标。  
- **转换流水线：** 将提取的 SVG 输入 `cairosvg` 或 `svglib`，生成 PNG 或 PDF 资源。  
- **多 SVG 处理：** 扩展提取函数，遍历所有 `<svg>` 标签并为每个生成唯一文件名。

尽情实验吧——SVG 本质是 XML，可能性无限。如果遇到奇怪的问题，记得参考上表中的坑点并相应调整。

祝你玩转矢量编码！

## 接下来该学习什么？

以下教程与本指南紧密相关，能够帮助你进一步掌握 API 功能并探索在项目中的其他实现方式。每篇资源都包含完整可运行的代码示例和逐步解释。

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}