---
category: general
date: 2026-10-02
description: 学习如何在 Python 中创建 SVG 文档，将 SVG 保存到文件，并使用简短完整的脚本导出 SVG 图像。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: zh
lastmod: 2026-10-02
og_description: 使用 Python 创建 SVG 文档，并通过本实用教程导出 SVG 图像。按照脚本操作，将 SVG 保存到文件，立即重复使用矢量图形。
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: 使用 Python 创建 SVG 文档 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: 如何在 Python 中创建 SVG 文档并将其导出为图像
url: /zh/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中创建 SVG 文档并导出为图像

如果你需要 **创建 SVG 文档**（programmatically），本教程将手把手教你使用 Python 完成。你将看到一个完整的脚本，构建一个简单的圆形，将 SVG 保存到文件，并生成可在任何地方嵌入的可导出 SVG 图像。

通过代码生成可伸缩矢量图形（SVG），可以省去在 GUI 编辑器中手动绘制形状的工作。阅读完本指南后，你可以将 SVG 创建集成到数据可视化管道、自动化报告生成器或任何需要清晰、分辨率无关图形的项目中。

## 前置条件

在开始之前，请确保你具备以下条件：

- 已安装 Python 3.8 或更高版本
- 已安装 `svgwrite` 库（使用 `pip install svgwrite` 安装）
- 对将保存 SVG 的目录拥有写入权限

这些要求保持示例轻量且兼容大多数环境。

## 第一步：安装并导入 SVG 库

第一步是添加提供便捷 API 用于 SVG 创建的第三方库。

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` 抽象了 SVG 文件的 XML 结构，让你专注于几何形状，而不是原始标记。

## 第二步：创建 SVG 文档对象

现在可以通过实例化 `svgwrite.Drawing` **创建 SVG 文档**。该对象代表根 `<svg>` 元素，并保存所有后续的形状。

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

`size` 参数定义渲染后的像素尺寸，而 `viewBox` 建立与后续几何定义相匹配的坐标系。

## 第三步：添加圆形元素

圆形由中心点 (`cx`, `cy`) 和半径 (`r`) 定义。使用 `circle` 辅助方法来设置这些属性。

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

该圆位于 100 × 100 画布的中心，两侧各留有 10 像素的边距。根据你的设计语言调整 `fill` 和 `stroke`。

## 第四步：将 SVG 保存到文件

图形组装完成后，你可以使用 `save` 方法 **将 SVG 保存到文件**。这会写入符合规范的 XML，浏览器和矢量编辑器都能识别。

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

文件 `circle.svg` 现在位于当前工作目录。你可以在网页浏览器、Inkscape 或任何支持 SVG 格式的工具中打开它。

## 第五步：验证导出的 SVG 图像

在浏览器中打开已保存的文件以确认输出。你应该会看到一个居中的圆形，颜色与指定的一致。原始 XML 如下所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

由于 SVG 基于矢量，你可以在不损失质量的情况下缩放图像，这使其非常适合响应式网页设计或高分辨率打印。

## 小技巧：将 SVG 导出为 PNG 或 JPEG

如果需要栅格版本，可以结合 **CairoSVG** 等转换工具：

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

此步骤演示了 **导出 SVG 图像** 为位图格式，当下游系统无法直接渲染 SVG 时非常有用。

## 常见变体和边缘情况

| 变体 | 处理方式 |
|-----------|---------------|
| 多个形状 | 对每个新元素（矩形、直线、路径）调用 `dwg.add()`。 |
| 动态尺寸 | 在创建 `Drawing` 前根据数据计算 `size` 和 `viewBox`。 |
| 文本标签 | 使用 `dwg.text("Label", insert=("10", "20"))` 并通过 `font_size` 与 `fill` 设置样式。 |
| 重复使用文档 | 将 `Drawing` 对象保存在内存中，需要更新文件时调用 `save()`。 |
| 大文件 | 使用 `dwg.tostring()` 流式输出并手动写入文件对象，以避免内存峰值。 |

处理这些场景可确保你的 **如何生成 SVG** 脚本能够从简单图标扩展到复杂图表。

## 完整脚本回顾

下面是包含所有步骤及可选转换的完整可运行示例：

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

运行此脚本会生成 `circle.svg`，如果已安装 `cairosvg`，还会生成 `circle.png`。这两个文件均可直接用于网页、报告或后续处理。

## 结论

现在你已经掌握了在 Python 中 **创建 SVG 文档**、**将 SVG 保存到文件**，以及 **导出 SVG 图像** 以供更广泛使用的完整流程。示例涵盖了关键 API 调用，解释了每一步的意义，并提供了面向更复杂图形的扩展思路。

接下来，探索更多 **SVG Python 教程** 主题，如绘制路径、应用渐变以及为元素添加动画。将这些技术融入你的 Python 应用，即可直接生成动态、数据驱动的矢量图形。祝编码愉快！


## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步提升。每个资源都提供完整的可运行代码示例，并配有逐步解释，帮助你掌握更多 API 功能并在项目中尝试不同实现方式。

- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}