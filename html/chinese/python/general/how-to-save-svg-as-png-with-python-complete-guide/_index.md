---
category: general
date: 2026-09-29
description: 如何使用 Python 保存 SVG 并将 SVG 导出为 PNG。学习在几分钟内使用精细调节的选项将 SVG 转换为 PNG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: zh
lastmod: 2026-09-29
og_description: 如何使用 Python 保存 SVG 并将 SVG 导出为 PNG。遵循本指南，将 SVG 转换为 PNG，并全面控制选项。
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: 如何使用 Python 将 SVG 保存为 PNG – 步骤详解
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  headline: How to save SVG as PNG with Python – complete guide
  type: TechArticle
- description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  name: How to save SVG as PNG with Python – complete guide
  steps:
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: (Optional) Create image‑save options
    text: '```python from aspose.svg import ImageSaveOptions'
  - name: Save the SVG as PNG
    text: '```python # Export the SVG to a PNG file using the options defined above
      svg_doc.save("YOUR_DIRECTORY/vector.png", options) ```'
  - name: Full script
    text: 'Putting the pieces together yields a complete, runnable program:'
  - name: Missing file or invalid path
    text: 'If `src_path` does not exist, `SVGDocument` raises a `FileNotFoundError`.
      Wrap the call in a `try/except` block to provide a friendly error message:'
  - name: Preserving aspect ratio
    text: When only one dimension (width **or** height) is set, the library automatically
      scales the other dimension to maintain the original aspect ratio. If you set
      both dimensions, the image may stretch. Choose the approach that matches your
      UI requirements.
  - name: Transparent backgrounds
    text: 'If the original SVG relies on transparency (e.g., icons), you can keep
      the PNG transparent by omitting `background_color`:'
  type: HowTo
tags:
- Python
- SVG
- Image conversion
title: 使用 Python 将 SVG 保存为 PNG 的完整指南
url: /zh/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 将 SVG 保存为 PNG – 完整指南

如果您需要 **如何保存 SVG** 为光栅图像，本教程将向您展示一个可直接运行的解决方案。您将学习如何加载矢量 SVG 文件，可选地调整图像保存设置，并仅用三行代码将结果导出为 PNG。

将 SVG 文件保存为 PNG 在您想要在网页中嵌入图形、生成缩略图或向机器学习流水线提供光栅图像时很常见。这里描述的方法可在 Windows、macOS 和 Linux 上运行，无需额外的本机依赖。

## 前提条件

在开始之前，请确保您拥有：

* 已安装 Python 3.9 或更高版本
* `aspose.svg` 包（官方的 Aspose SVG for Python via .NET）。使用以下方式安装：

```bash
pip install aspose-svg
```

* 磁盘上有效的 SVG 文件（例如 `vector.svg`）

这些要求使示例保持自包含，并避免使用诸如 CairoSVG 等外部工具。

## 如何使用 Python 保存 SVG

该过程的核心包括三个步骤：加载、配置和保存。以下章节将逐步拆解每个步骤。

### 步骤 1：加载 SVG 文档

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

`SVGDocument` 解析 SVG XML 并构建内存中的表示。必须先加载文件；否则保存操作将没有源数据。

### 步骤 2：（可选）创建图像保存选项

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

`ImageSaveOptions` 让您对 PNG 输出进行精细调节。调整宽度和高度可以在未显式同时设置两者时保持纵横比。设置背景颜色在原始 SVG 包含透明度但您需要不透明 PNG 时非常有用。

### 步骤 3：将 SVG 保存为 PNG

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

`save` 方法将 PNG 文件写入目标路径。如果省略 `options` 参数，库会使用从 SVG 的 viewBox 派生的默认尺寸。

### 完整脚本

将各部分组合在一起即可得到一个完整且可运行的程序：

```python
# -*- coding: utf-8 -*-
"""
How to save SVG as PNG with Python.
This script loads an SVG file, applies optional image‑save settings,
and exports the result to PNG.
"""

from aspose.svg import SVGDocument, ImageSaveOptions

def convert_svg_to_png(
    src_path: str,
    dst_path: str,
    width: int = 800,
    height: int = 600,
    background: str = "#FFFFFF"
) -> None:
    """Convert an SVG file to PNG with custom dimensions and background."""
    # Load the SVG document
    svg_doc = SVGDocument(src_path)

    # Prepare save options
    options = ImageSaveOptions()
    options.width = width
    options.height = height
    options.background_color = background

    # Save as PNG
    svg_doc.save(dst_path, options)


if __name__ == "__main__":
    # Example usage
    convert_svg_to_png(
        src_path="YOUR_DIRECTORY/vector.svg",
        dst_path="YOUR_DIRECTORY/vector.png",
        width=1024,
        height=768,
        background="#FFFFFF"
    )
    print("SVG successfully saved as PNG.")
```

运行脚本后会打印 **“SVG successfully saved as PNG.”** 并在同一文件夹中生成 `vector.png`。

## 将 SVG 转换为 PNG – 处理常见陷阱

### 文件缺失或路径无效

如果 `src_path` 不存在，`SVGDocument` 会抛出 `FileNotFoundError`。将调用包装在 `try/except` 块中，以提供友好的错误信息：

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### 保持纵横比

当仅设置一个维度（宽度 **或** 高度）时，库会自动缩放另一个维度以保持原始纵横比。如果同时设置两者，图像可能会被拉伸。请选择符合您 UI 需求的方法。

### 透明背景

如果原始 SVG 依赖透明度（例如图标），可以通过省略 `background_color` 来保持 PNG 的透明性：

```python
options.background_color = None   # PNG will retain transparency
```

当 PNG 将叠加在其他图形上时，此变体非常有用。

## 导出 SVG 为 PNG – 性能技巧

* **在批量转换多个文件时复用 `ImageSaveOptions`**。为每个文件创建新的选项对象开销极小，但复用可以避免重复的内存分配。
* **批处理**：遍历 SVG 文件目录，对每个文件调用 `convert_svg_to_png`。库会独立处理每个文件，因此您可以使用 `concurrent.futures.ThreadPoolExecutor` 并行循环，以在多核机器上加快转换速度。

```python
import os
from concurrent.futures import ThreadPoolExecutor

svg_folder = "YOUR_DIRECTORY"
png_folder = "YOUR_DIRECTORY/pngs"
os.makedirs(png_folder, exist_ok=True)

def batch_convert(file_name):
    src = os.path.join(svg_folder, file_name)
    dst = os.path.join(png_folder, file_name.replace('.svg', '.png'))
    convert_svg_to_png(src, dst)

with ThreadPoolExecutor(max_workers=8) as executor:
    executor.map(batch_convert, [f for f in os.listdir(svg_folder) if f.endswith('.svg')])
```

## 保存 SVG 为 PNG – 验证

转换后，您可以通过编程方式验证输出：

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

典型输出：

```
PNG size: (1024, 768), mode: RGBA
```

`mode` 为 `RGBA` 表明图像包含 alpha 通道（透明度）。如果设置了背景颜色，模式将为 `RGB`。

## 结论

现在您已经了解如何使用 Python **将 SVG 保存为 PNG**，如何 **将 SVG 转换为 PNG**，以及如何 **导出 SVG 为 PNG**，并可自定义尺寸和背景处理。完整脚本演示了从加载矢量 SVG 文件到生成光栅 PNG 图像的完整工作流。

接下来，您可以探索相关主题，例如批量模式下的 **save SVG as PNG**、使用替代库如 **CairoSVG**，或从 SVG 源生成多页 PDF。尝试不同的 `ImageSaveOptions` 设置，以针对您的具体使用场景微调质量、DPI 和压缩率。

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，构建在本教程展示的技术之上。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方法。

- [svg to png java – 使用 Aspose.HTML for Java 将 SVG 转换为图像](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [使用 Aspose.HTML 在 .NET 中将 SVG 文档呈现为 PNG](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [使用 Java 将 SVG 转换为 PNG 时如何设置 DPI](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}