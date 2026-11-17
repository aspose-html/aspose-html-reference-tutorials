---
category: general
date: 2026-11-17
description: 使用 Python 几行代码将 SVG 转换为 PNG。了解如何在可选的转换设置下将 SVG 保存为 PNG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert svg to png
- save svg as png
- export svg as png
- svg to raster image
- how to convert svg to png
language: zh
lastmod: 2026-11-17
og_description: 在 Python 中将 SVG 转换为 PNG，示例简洁。按照步骤高效导出 SVG 为 PNG。
og_image_alt: Diagram illustrating convert svg to png workflow in Python
og_title: 在 Python 中将 SVG 转换为 PNG – 快速指南
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: convert svg to png using Python in a few lines. Learn to save SVG as
    PNG with optional conversion settings.
  headline: How to convert SVG to PNG in Python – step‑by‑step guide
  type: TechArticle
tags:
- svg
- png
- python
- image conversion
title: 如何在 Python 中将 SVG 转换为 PNG——一步一步的指南
url: /zh/python/general/how-to-convert-svg-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中将 SVG 转换为 PNG – 步骤指南

如果你需要 **convert svg to png**，本指南提供了一个可以立即运行的完整解决方案。你还将看到如何 **save svg as png**，并可选地设置尺寸和背景颜色。

从矢量 SVG 文件生成光栅图像在向浏览器提供图形、创建缩略图或在 PDF 中嵌入图像时非常常见。本教程涵盖了从安装所需库到处理缺失文件或超大 SVG 等边缘情况的全部内容。

## 前置条件

在开始之前，请确保你具备以下条件：

* 已安装 Python 3.8 或更高版本。
* 能够使用终端或命令提示符。
* 已安装 `cairosvg` 包，该包负责 **svg to raster image** 转换的核心工作。

你可以使用一条 pip 命令安装该包：

```bash
pip install cairosvg
```

> **专业提示：** 使用虚拟环境可以将依赖与其他项目隔离。

## 如何在 Python 中将 SVG 转换为 PNG

整个过程的核心包括三个操作：加载 SVG、可选地调整转换参数、写入 PNG 文件。下面的代码在可复用函数中实现了这三步。

```python
import cairosvg
from pathlib import Path

def convert_svg_to_png(svg_path: str, png_path: str) -> None:
    """
    Convert an SVG file to a PNG raster image.

    Parameters
    ----------
    svg_path : str
        Path to the source SVG file.
    png_path : str
        Destination path for the generated PNG file.
    """
    # Verify that the SVG file exists
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    # Perform the conversion using default settings
    cairosvg.svg2png(url=svg_path, write_to=png_path)

# Example usage
if __name__ == "__main__":
    svg_file = "YOUR_DIRECTORY/image.svg"
    png_file = "YOUR_DIRECTORY/image.png"
    convert_svg_to_png(svg_file, png_file)
    print(f"Converted {svg_file} to {png_file}")
```

### 为什么这样可行

* `cairosvg.svg2png` 读取 SVG 文件（`url=svg_path`）并写入 PNG 文件（`write_to=png_path`）。  
* 如果找不到源 SVG，函数会抛出明确的错误，帮助你提前调试文件路径问题。  
* 将转换逻辑封装在函数中，使其易于在多个脚本之间复用，或集成到更大的应用程序中。

## 可选：微调转换参数

如果你需要特定的输出尺寸或不同的背景，`cairosvg.svg2png` 接受额外的参数。下面的变体将宽度设置为 300 px 并使用白色背景。

```python
def convert_svg_to_png_custom(svg_path: str, png_path: str,
                              width: int = 300,
                              background_color: str = "white") -> None:
    """
    Convert an SVG to PNG with custom dimensions and background.

    Parameters
    ----------
    width : int
        Desired width of the PNG in pixels; height scales proportionally.
    background_color : str
        Hex or named color for the PNG background.
    """
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    cairosvg.svg2png(
        url=svg_path,
        write_to=png_path,
        output_width=width,
        background_color=background_color
    )
```

你可以像调用基础版本一样调用此函数，只需传入任意宽度或颜色即可。

## 常见问题与边缘情况

**如果 SVG 包含外部字体怎么办？**  
`cairosvg` 会自动嵌入引用的字体，但字体文件必须能够从 SVG 所在位置访问到。请将字体文件放在 SVG 同目录下或使用绝对 URL。

**如何处理超大 SVG？**  
大文件可能会消耗大量内存。你可以在不从磁盘一次性加载的情况下流式读取 SVG 内容：

```python
with open(svg_path, "rb") as svg_stream:
    cairosvg.svg2png(file_obj=svg_stream, write_to=png_path)
```

**能批量转换多个文件吗？**  
在循环中包装转换调用，并使用 `Path.glob("*.svg")` 来发现目录中的所有 SVG 文件。

## 预期输出

运行示例脚本后会在终端打印一行，确认转换已完成：

```
Converted YOUR_DIRECTORY/image.svg to YOUR_DIRECTORY/image.png
```

生成的 `image.png` 文件位于同一目录，可使用任意图像查看器打开。

## 结论

现在你已经掌握了如何在 Python 中 **convert svg to png**、如何 **save svg as png**，以及如何使用自定义尺寸 **export svg as png**。相同的方法适用于任何 SVG 文件，将矢量图形转换为适用于网页、报告或缩略图的 **svg to raster image** 格式。

接下来的可能方向包括：

* 探索 `export svg as png` 参数以控制 DPI。
* 将转换函数集成到 Flask 或 Django 接口中，实现即时图像生成。
* 使用次要关键词 **how to convert svg to png** 搜索更高级的用例，如批处理或 CI/CD 流水线。

欢迎尝试不同设置，并将你的成果分享给社区！

## 接下来你应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方案，每个资源都提供了完整可运行的代码示例和逐步解释。

- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)
- [Convert SVG to PNG in Python – Complete Step‑by‑Step Guide](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}