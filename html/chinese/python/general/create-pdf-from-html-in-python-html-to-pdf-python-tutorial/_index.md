---
category: general
date: 2026-07-15
description: 使用 Python 将 HTML 生成 PDF。了解如何通过简洁脚本和清晰步骤快速将 HTML 转换为 PDF。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: zh
lastmod: 2026-07-15
og_description: 使用 Python 将 HTML 转换为 PDF。本指南展示了如何将 HTML 转换为 PDF、将 HTML 保存为 PDF，并高效处理资源。
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: 在 Python 中从 HTML 创建 PDF – 实战教程
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: 在 Python 中从 HTML 创建 PDF – HTML 转 PDF Python 教程
url: /zh/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 将 HTML 转换为 PDF – 完整教程

是否曾经需要**从 HTML 创建 PDF**却不确定该选哪个 Python 库？你并不孤单——很多开发者在尝试将网页报告、发票或营销页面转为可打印的 PDF 时都会遇到这个难题。  

好消息是，只需几行代码就能**可靠地将 HTML 转换为 PDF**，且脚本可在 Windows、macOS 和 Linux 上运行。本指南将逐步演示一个完整、可运行的示例，解释每一步的意义，并展示如何**将 HTML 保存为 PDF**而不留下任何疏漏。

---

## 你将学到的内容

- 为 HTML‑to‑PDF 转换安装合适的 Python 包。  
- 使用自定义资源处理选项加载 HTML 文件（避免无限 CSS 导入）。  
- 在磁盘上生成干净的 PDF 文件。  
- 处理常见的边缘情况，如外部图片、相对路径和大文档。  

通过本**HTML 转 PDF 教程**，你将拥有一个可在任何项目中复用的函数。

---

## 前置条件

- Python 3.9+（代码在 3.8 也可运行，但 3.9+ 提供最新的 `pathlib` 功能）。  
- 对命令行和虚拟环境有基本了解。  
- 一个你想转换为 PDF 的 HTML 文件——任何静态页面都可以。

> **专业提示：** 如果使用虚拟环境，请在安装库之前激活它；这可以保持全局 Python 环境的整洁。

---

## 第一步 – 安装 WeasyPrint（转换引擎）

WeasyPrint 是一个纯 Python 库，能够将 HTML 和 CSS 渲染为 PDF。它支持大多数现代网页特性，并提供对资源加载的细粒度控制。

```bash
pip install weasyprint
```

运行上述命令会拉取 `cairocffi`、`tinycss2` 等依赖。如果在 Windows 上遇到 `cairo` 相关错误，请从 [WeasyPrint 网站](https://weasyprint.org/docs/install/) 获取预编译的 wheel 包。

---

## 第二步 – 为资源处理准备一个小助手

当加载引用外部样式表或图片的 HTML 文档时，库会跟随这些链接。在某些情况下，这会导致深度嵌套甚至无限循环（比如 CSS 文件自行 `@import`）。为保持整洁，我们限制资源处理的深度。

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

上面的类并非 WeasyPrint 必需，但它对应了原始代码片段中的模式，并提供了一个钩子来阻止导入失控。下一步会用到它。

---

## 第三步 – 使用自定义选项加载 HTML 文档

现在我们真正读取 HTML 文件。`HTML` 类接受 `base_url` 参数，我们将其设为源文件所在目录——这样相对链接即可在没有 Web 服务器的情况下工作。

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **为什么重要：** 如果你的 HTML 引入了一连串 CSS 文件，每个 `@import` 都会触发一次加载。深度守护可以防止脚本失控。

---

## 第四步 – 将处理后的文档保存为 PDF

手握 `HTML` 对象后，生成 PDF 只需一行代码。我们还传入了一段简单的 CSS，强制使用 A4 页面尺寸并添加细小的边距——可自行调整。

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

调用 `write_pdf` 会将 PDF 流式写入磁盘，生成可直接分享的文件。

---

## 第五步 – 综合示例

下面是一个紧凑的脚本，可直接复制到 `convert.py` 中。将占位路径替换为你的实际目录。

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**预期输出** – 运行 `python convert.py` 后你应看到：

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

使用任意 PDF 查看器打开生成的文件；你会看到原始页面布局、CSS 样式以及图片（前提是这些图片在 HTML 中可访问）。  

如果发现图片缺失，请再次确认它们的 `src` 属性是绝对 URL 或相对于 `YOUR_DIRECTORY` 存在的路径。

---

## 常见问题与边缘情况处理

| 问题 | 解答 |
|----------|--------|
| *如果我的 HTML 引用了外部字体怎么办？* | WeasyPrint 会自动下载字体文件，但你可能需要白名单域名以避免长时间的获取。 |
| *能否将 HTML 字符串而不是文件转换？* | 可以——使用 `HTML(string=my_html_string)`，并省略 `base_url` 或将其设为临时文件夹。 |
| *如何控制 PDF 元数据（标题、作者）？* | 向 `write_pdf` 传入 `metadata` 字典，例如 `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`。 |
| *在 Linux 上出现 “cairo‑cffi error”。* | 在 pip 安装 WeasyPrint 前，先安装系统包 `libcairo2-dev`（Debian/Ubuntu 上使用 `apt-get install libcairo2-dev`）。 |

---

## 总结

我们已经使用简洁的 Python 工作流**从 HTML 创建 PDF**，覆盖了**将 HTML 转换为 PDF**的机制，并展示了如何**将 HTML 保存为 PDF**并具备稳健的资源处理。该脚本足够小巧，可直接嵌入 CI 流水线，同时也足够灵活，可扩展自定义页眉、页脚或水印。

你可以进一步探索的方向：

- 使用 **html to pdf python** 库 `pdfkit`，基于 wkhtmltopdf 的方式（适合旧版 CSS）。  
- 添加 `argparse` 实现 CLI，使脚本接受输入/输出参数。  
- 在 Flask 或 FastAPI 接口中即时生成 PDF，以实现按需报告。  

欢迎实验、打破常规，然后回到本指南快速复习。如果遇到阻碍，WeasyPrint 的文档和社区论坛都是极佳的资源。

祝编码愉快，享受将网页转化为精美 PDF 的过程！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式，每篇都提供完整可运行的代码示例和逐步解释。

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}