---
category: general
date: 2026-10-28
description: 学习如何在 Python 中光栅化 SVG，并使用 CairoSVG 的简单脚本将 SVG 转换为 PNG。几秒钟即可将 SVG 保存为
  PNG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rasterize svg
- convert svg to png
- save svg as png
- svg to png python
- export svg as png
language: zh
lastmod: 2026-10-28
og_description: 如何在 Python 中光栅化 SVG：本指南展示如何使用 CairoSVG 将 SVG 转换为 PNG，涵盖安装、代码和故障排除。
og_image_alt: Screenshot of Python code that rasterizes SVG to PNG
og_title: 如何在 Python 中栅格化 SVG – 快速 SVG 转 PNG 指南
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  headline: How to rasterize SVG in Python – convert SVG to PNG easily
  type: TechArticle
- description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  name: How to rasterize SVG in Python – convert SVG to PNG easily
  steps:
  - name: Why CairoSVG?
    text: '- **Pure Python**: No need for external command‑line tools once the package
      is installed. - **SVG‑compliant**: Supports most SVG 1.1 features, including
      gradients, masks, and text. - **Flexible output**: Besides PNG, you can export
      to PDF, PS, or even raw bytes.'
  - name: Step‑by‑step breakdown
    text: 1. **Install the library** – `pip install cairosvg` pulls in the compiled
      Cairo bindings. 2. **Import the module** – `import cairosvg` gives you access
      to the `svg2png` helper. 3. **Call `svg2png`** – Pass the SVG file path (or
      a URL) and the destination PNG path. Optional `output_width`, `output_he
  - name: Edge cases you might encounter
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | **Large SVG (megapixel dimensions)** | Increase `dpi` or set explicit `output_width`/`output_height`
      to avoid memory spikes. | | **Missing fonts** | Install the required fonts on
      the system or em'
  type: HowTo
tags:
- svg
- python
- image processing
- cairosvg
title: 如何在 Python 中光栅化 SVG – 轻松将 SVG 转换为 PNG
url: /zh/python/general/how-to-rasterize-svg-in-python-convert-svg-to-png-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中光栅化 SVG – 轻松将 SVG 转换为 PNG

如果您需要为网页应用、报告或自动化构建 **how to rasterize svg**，本指南提供了一个即开即用的解决方案。您只需几行 Python 代码即可 **convert svg to png**，并得到一张清晰的 PNG，您可以立即存储或提供。

本教程涵盖了从安装所需库到处理大型文件或自定义 DPI 设置等边缘情况的全部内容。完成后，您将能够 **save svg as png**、**export svg as png**，并将此过程集成到任何 Python 工作流中。

## 您需要的条件

- Python 3.8+（代码在 3.9、3.10 及更高版本上均可运行）
- `pip` 用于安装包
- 本地 SVG 文件（例如 `logo.svg`），您希望对其进行光栅化
- 可选：用于干净依赖管理的虚拟环境

> **专业提示：** 使用虚拟环境（`python -m venv .venv`）可以将 CairoSVG 依赖与全局 Python 包隔离。

## 如何在 Python 中光栅化 SVG

最直接的 **how to rasterize svg** 方法是使用 **CairoSVG** 库。CairoSVG 读取 SVG XML，使用 Cairo 图形引擎渲染，并将光栅图像写入 PNG、PDF 或其他位图格式。

```bash
# Install CairoSVG and its binary dependencies
pip install cairosvg
```

```python
# rasterize_svg.py
import sys
from pathlib import Path
import cairosvg

def rasterize_svg(input_path: str, output_path: str,
                  width: int | None = None,
                  height: int | None = None,
                  dpi: int = 96) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the PNG file.
    width : int | None
        Desired output width in pixels (maintains aspect ratio if height is None).
    height : int | None
        Desired output height in pixels (maintains aspect ratio if width is None).
    dpi : int
        Dots per inch for the rasterization. Higher DPI yields larger files but more detail.
    """
    try:
        # CairoSVG can read from a file path directly
        cairosvg.svg2png(url=Path(input_path).as_uri(),
                         write_to=output_path,
                         output_width=width,
                         output_height=height,
                         dpi=dpi)
        print(f"✅ Successfully saved PNG to {output_path}")
    except Exception as e:
        print(f"❌ Failed to rasterize {input_path}: {e}", file=sys.stderr)
        raise

if __name__ == "__main__":
    # Example usage:
    # python rasterize_svg.py ./assets/logo.svg ./output/logo.png 300 300
    if len(sys.argv) < 3:
        print("Usage: python rasterize_svg.py <input_svg> <output_png> [width] [height] [dpi]")
        sys.exit(1)

    input_svg = sys.argv[1]
    output_png = sys.argv[2]
    w = int(sys.argv[3]) if len(sys.argv) > 3 else None
    h = int(sys.argv[4]) if len(sys.argv) > 4 else None
    d = int(sys.argv[5]) if len(sys.argv) > 5 else 96

    rasterize_svg(input_svg, output_png, width=w, height=h, dpi=d)
```

### 为什么选择 CairoSVG？

- **Pure Python**：安装包后无需外部命令行工具。
- **SVG‑compliant**：支持大多数 SVG 1.1 特性，包括渐变、遮罩和文本。
- **Flexible output**：除了 PNG，还可以导出为 PDF、PS，甚至原始字节。

### 步骤分解

1. **安装库** – `pip install cairosvg` 会拉取已编译的 Cairo 绑定。  
2. **导入模块** – `import cairosvg` 让您可以使用 `svg2png` 辅助函数。  
3. **调用 `svg2png`** – 传入 SVG 文件路径（或 URL）和目标 PNG 路径。可选的 `output_width`、`output_height` 和 `dpi` 参数可控制尺寸和分辨率。  
4. **处理错误** – `try/except` 块会在 SVG 损坏或输出目录不可写时打印清晰的错误信息。

## 使用 CairoSVG 将 SVG 转换为 PNG

如果您只需要一行代码快速转换，下面的代码片段即可完成，无需包装函数：

```python
import cairosvg

cairosvg.svg2png(url="logo.svg", write_to="logo.png")
```

这是 **convert svg to png** 最简洁的示例。它从当前目录读取 `logo.svg` 并在同目录下生成 `logo.png`。

## 将 SVG 保存为 PNG – 验证结果

运行脚本后，您应该在目标路径看到 PNG 文件。使用任意图像查看器打开以确认：

```bash
# Linux/macOS
xdg-open ./output/logo.png   # or open on macOS
# Windows
start ./output/logo.png
```

如果 PNG 看起来模糊，请增大 `dpi` 参数（例如 `dpi=300`），以生成更高分辨率的光栅图。

## 以不同格式导出 SVG 为 PNG

CairoSVG 还可以输出 **PDF**、**PostScript** 或原始 **PNG bytes**。下面示例演示在需要将图像保存在内存中（例如用于 Flask 响应）时导出到 `BytesIO` 对象：

```python
import io
import cairosvg

svg_path = "logo.svg"
png_bytes = io.BytesIO()
cairosvg.svg2png(url=Path(svg_path).as_uri(), write_to=png_bytes)
png_bytes.seek(0)  # Ready for sending over HTTP
```

### 可能遇到的边缘情况

| 情况                               | 推荐处理方式 |
|------------------------------------|--------------|
| **大型 SVG（百万像素尺寸）**       | 增加 `dpi` 或显式设置 `output_width`/`output_height`，以避免内存激增。 |
| **缺失字体**                       | 在系统上安装所需字体，或使用 `<style>` 标签将其嵌入 SVG 中。 |
| **透明度问题**                     | PNG 默认保留 alpha 通道；如果需要实色背景，可向 `svg2png` 传入 `background_color="#FFFFFF"`。 |
| **批量处理**                       | 遍历 SVG 目录，对每个文件调用 `rasterize_svg`。 |

## 完整可运行示例

下面是一个最小的、独立的脚本，您可以复制粘贴到名为 `svg_to_png.py` 的文件中并立即运行。

```python
# svg_to_png.py
import cairosvg
from pathlib import Path

def main():
    src = Path("example.svg")
    dst = Path("example.png")
    if not src.is_file():
        raise FileNotFoundError(f"Source SVG not found: {src}")

    # Convert with default DPI (96) and keep original dimensions
    cairosvg.svg2png(url=src.as_uri(), write_to=dst)
    print(f"✅ {src.name} → {dst.name} created successfully.")

if __name__ == "__main__":
    main()
```

Running `python svg_to_png


## 接下来应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [如何在 Python 中光栅化 SVG – 完整指南](/html/english/python/general/how-to-rasterize-svg-in-python-complete-guide/)
- [在 Python 中将 SVG 转换为 PNG – 高分辨率导出指南](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [在 Python 中创建 SVG 文档 – 将 SVG 转换为 PNG 指南](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}