---
category: general
date: 2026-07-27
description: 如何在 Aspose.HTML（Python）中使用 SaveOptions 将大型 HTML 页面转换并高效地进行资源处理。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: zh
lastmod: 2026-07-27
og_description: 如何在 Aspose.HTML（Python）中使用 SaveOptions，在进行资源处理的同时转换大型 HTML 页面，以获得干净、快速的结果。
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: 如何在 Aspose.HTML 中使用 SaveOptions – Python 指南
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: 如何在 Aspose.HTML（Python）中使用 SaveOptions
url: /zh/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose.HTML (Python) 中使用 SaveOptions

在处理大型 HTML 文件时，许多开发者都会询问如何在 Aspose.HTML for Python 中使用 SaveOptions。如果你需要 **转换大型 HTML 页面** 并且想要对 **apply resource handling** 进行精细控制，那么你来对地方了。  

在本教程中，我们将通过一个真实场景演示：对一个体积庞大的 HTML 页面进行处理，限制嵌套资源的抓取深度，最终以清晰可控的方式保存（或转换）结果。没有模糊的引用，只有完整、可直接运行的示例，今天就可以复制粘贴到你的项目中使用。

> **技巧提示：** Aspose.HTML 的 `SaveOptions` 不仅用于保存回 HTML，还可以用于转换为 PDF、PNG，甚至 DOCX。下面展示的相同模式同样适用于所有这些格式。

---

## 你需要准备的环境

- **Python 3.8+**（代码使用类型提示，但在任何近期版本上均可运行）  
- **Aspose.HTML for Python via .NET** – 通过 `pip install aspose-html` 安装  
- 一个你想要压缩或转换的 **大型 HTML 文件**（示例使用 `big_page.html`）  
- 用于输出文件的适量磁盘空间  

就这些——无需额外库，也不需要笨重的构建工具。

---

## 如何使用带资源处理选项的 SaveOptions

这才是关键所在。我们将创建一个 `SaveOptions` 实例，附加一个 `ResourceHandlingOptions` 对象，用来告诉 Aspose.HTML 在抓取链接资源时的深度限制，然后将所有设置交给文档的 `save` 方法。

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**工作原理：**  
- `HTMLDocument` 加载原始文件，解析每个 `<img>`、`<link>`、`<script>` 等标签。  
- `ResourceHandlingOptions.max_handling_depth` 告诉引擎在嵌套三层后停止抓取资源——这对于避免在嵌入其他页面的页面上出现无限循环非常有效。  
- `SaveOptions` 是承载输出格式（默认 HTML）以及资源处理规则的容器。  
- 最后，`doc.save` 将新文件写出，应用我们刚才设定的规则。

运行脚本后，你会在 `big_page_processed.html` 看到一个新文件。用浏览器打开它，你会发现所有深度不超过三层的图片、样式和脚本仍然存在，而更深层的引用已被剔除。这大幅降低了文件体积，却不破坏页面的核心布局——正是 **转换大型 HTML 页面** 用于离线或邮件发送时所需要的。

---

## 高效转换大型 HTML 页面

如果你的目标是 *转换大型 HTML 页面* 为更小的版本，上面的代码片段已经完成了大部分工作。不过，你可能想要更改输出格式。Aspose.HTML 只需一行代码即可实现：

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

只需将 `format` 属性改为 `"PNG"`、`"JPEG"` 或 `"DOCX"`，即可得到完整的转换流水线。相同的 **apply resource handling** 规则仍然生效，因此生成的 PDF 不会嵌入原站点的所有外部 CSS 文件——仅会包含你定义的三层深度内的资源。

---

## 对嵌套资源应用资源处理

让我们更深入地探讨 **apply resource handling** 的有效使用方式。假设你的 HTML 包含一个样式表，而该样式表又导入了其他样式表，并且每个样式表都可能引用图片。如果没有深度限制，Aspose.HTML 可能会无限追踪这些链条，导致内存和 CPU 使用飙升。

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Depth 0** – 不抓取任何外部资源；得到一个极简的 HTML 骨架。  
- **Depth 1** – 只包含一级资源（直接的 `<img>` 标签、立即的 CSS 文件）。  
- **Depth 2+** – 尊重更深层的嵌套，适用于样式相互依赖的复杂站点。

根据你的 **转换大型 HTML 页面** 场景选择合适的深度。对于邮件新闻稿，Depth 1 通常已足够；对于本地归档，Depth 3（如主示例所示）则提供了良好的平衡。

---

## 完整工作示例 – 从头到尾

下面是一个自包含的脚本，保存为 `process_html.py`。它包含错误处理、日志记录以及一个小助手，用于打印出你实现的大小缩减比例。

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**预期输出（控制台）：**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

打开处理后的文件，你会看到一个仍然保持原始外观但更精简的页面。如果将 `fmt` 改为 `"PDF"`，控制台会报告 PDF 文件大小，你可以使用任意 PDF 阅读器打开它。

---

## 常见问题与边缘情况

- **如果页面引用的 HTTPS 资源需要身份验证怎么办？**  
  Aspose.HTML 会跟随重定向，但不会自动发送凭证。你可以预先下载这些资产，或使用自定义 `WebRequest` 处理器（超出本指南范围）。

- **我能保留内联 CSS 同时剔除外部文件吗？**  
  可以——将 `resource_options.max_handling_depth = 0`。这样会跳过外部文件，但保留所有 `<style>` 块。

- **对于仍然导致输出膨胀的超大图片怎么办？**  
  保存后，你可以使用 Pillow 再次处理以降低分辨率，或使用 Aspose.HTML 内置的图像压缩选项（通过 `save_options.image_quality` 设置）。

- **深度限制是针对每种资源类型单独应用的吗？**  
  限制在所有资源类型（图片、脚本、样式）之间是全局的。如果需要更细粒度的控制，需要在加载文档后手动过滤资源。

---

## 结论

现在，你已经掌握了在 Aspose.HTML 中 **如何使用 SaveOptions** 的完整方法。

## 接下来该学习什么？

以下教程涵盖了与本指南紧密相关的主题，帮助你在项目中进一步探索 API 功能并尝试替代实现方案。每个资源都提供了完整的可运行代码示例和逐步解释。

- [如何使用 Aspose.HTML for Java 将 HTML 转换为 PDF](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [如何使用 Aspose.HTML for Java 将 HTML 转换为 MHTML](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [如何使用 Aspose 将 HTML 渲染为 PNG – 步骤指南](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}