---
category: general
date: 2026-11-27
description: 使用 Python 创建 SVG 文档并保存 SVG 文件。学习将矢量导出为 SVG 并快速生成 SVG 图像。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: zh
lastmod: 2026-11-27
og_description: 使用 Python 创建 SVG 文档并保存 SVG 文件。本指南将向您展示如何将矢量图导出为 SVG，并在几分钟内生成 SVG 图像。
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: 使用 Python 创建 SVG 文档并保存 SVG 文件
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: 使用 Python 创建 SVG 文档并保存 SVG 文件
url: /zh/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 创建 SVG 文档并保存 SVG 文件

如果你需要**从头创建 SVG 文档**，本指南将手把手带你完成整个过程。你将看到如何**将 SVG 文件保存**到磁盘、导出向量为 SVG，并仅用几行代码得到一个可直接使用的 SVG 图像。

以编程方式生成可伸缩的图形对于报告、UI 图标或任何需要分辨率无关图像的场景都非常有用。完成本教程后，你将能够回答“**如何创建 SVG**？”这一问题，先从简单形状入手，再将模式扩展到复杂的矢量艺术。

## 你需要的环境

- Python 3.8 或更高版本  
- `svgwrite` 包（可通过 `pip` 安装）  
- 用于输出文件的可写目录  

无需外部图形编辑器；所有操作均在命令行完成。

## 第一步：安装 `svgwrite` 库

`svgwrite` 提供了简洁、符合 Python 风格的 API 来构建 SVG 标记。使用以下命令一次性安装：

```bash
pip install svgwrite
```

> **小技巧：** 使用虚拟环境（`python -m venv .venv`）可以让依赖保持隔离。

## 第二步：创建 SVG 文档

现在我们实际**创建 SVG 文档**对象。`Drawing` 类对应根 `<svg>` 元素，并自动处理命名空间。

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

`Drawing` 实例是后续所有 SVG 操作的入口。通过指定 `size` 可以设定画布尺寸，这会影响浏览器渲染图像的方式。

## 第三步：添加一个红色圆形元素

添加形状非常直接。`circle` 方法会创建一个 `<circle>` 元素；随后我们将其附加到根节点。

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

之所以选择圆形：圆形是展示可伸缩性的矢量基元，能够在不失真情况下放大，非常适合作为**导出向量为 SVG**工作流的测试对象。

## 第四步：保存 SVG 文件

最后，将标记写入磁盘。此步骤实现了**保存 SVG 文件**的需求，并生成一个可以在任意浏览器或矢量编辑器中打开的文件。

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

运行脚本后，你会在控制台看到一条确认生成文件位置的消息。

### 预期输出

生成的 `circle.svg` 包含以下内容：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

在浏览器中打开该文件会显示一个清晰的红色圆形，并且由于它是基于矢量的，你可以无限放大而不会出现像素化。

## 第五步：常见变体和边缘情况

### 导出更复杂的矢量

如果需要为多形状插图**导出向量为 SVG**，只需使用 `dwg.add()` 方式重复添加其他基元（`rect`、`line`、`path` 等）。例如：

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### 处理 Unicode 与文本

SVG 支持完整的 Unicode 文本元素。使用 `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` 可以嵌入多语言标签。

### 保存到其他位置

当**保存 SVG 图像**到用户指定的文件夹时，需要验证路径以避免权限错误：

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### 压缩输出

在生产流水线中，你可能希望文件更小。向 `dwg.tostring()` 传入 `pretty=False`，然后手动写入结果：

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## 使用其他库创建 SVG（可选）

虽然 `svgwrite` 轻量且纯 Python，仍有其他生态可供选择：

- **cairosvg** – 将 PNG、PDF 或 HTML 转换为 SVG。  
- **lxml** – 使用 XML API 手动构建 SVG 标记。  

选择哪种库取决于项目的复杂度和已有依赖。

## 结论

现在你已经掌握了如何**创建 SVG 文档**、添加矢量形状，并使用 Python **保存 SVG 文件**。完整的示例展示了实现**导出向量为 SVG**、生成**SVG 图像**以及回答常见的**如何创建 SVG**编程问题的步骤。

接下来你可以：

- 使用循环扩展脚本，自动生成图表或图标。  
- 将 SVG 输出集成到 Web 应用或邮件模板中。  
- 通过添加 `<animate>` 元素并使用 `svgwrite` 探索动画效果。

尝试不同的形状、颜色和渐变，充分利用 Python 项目中可伸缩矢量图形的强大力量。祝编码愉快！


## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步提升。每个资源都提供完整可运行的代码示例以及逐步解释，助你掌握更多 API 功能并探索替代实现方式。

- [Create SVG Document – Add a Circle and Save as SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Load SVG File Python – Complete Guide to Export, Embed & Convert](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}