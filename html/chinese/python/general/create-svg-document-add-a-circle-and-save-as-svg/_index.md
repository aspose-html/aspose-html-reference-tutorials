---
category: general
date: 2026-07-31
description: 学习如何快速创建 SVG 文档、添加圆形并保存 SVG 文件。只需几行 Python 代码即可将图形导出为 SVG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: zh
lastmod: 2026-07-31
og_description: 创建 SVG 文档，添加圆形，并在几秒内保存 SVG 文件。本指南展示了如何使用清晰、可运行的代码将图形导出为 SVG。
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: 创建 SVG 文档 – 添加圆形并保存为 SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: 创建 SVG 文档 – 添加圆形并保存为 SVG
url: /zh/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 SVG 文档 – 添加圆形并保存为 SVG

是否曾经需要从代码 **create SVG document**（创建 SVG 文档），但不确定从何开始？你并不孤单；许多开发者在首次接触矢量图形时都会遇到这种障碍。在本教程中，我们将通过一个小型、独立的示例，向你展示如何 **add circle to SVG**（向 SVG 添加圆形），然后 **save SVG file**（保存 SVG 文件），以便 **export graphic as SVG**（将图形导出为 SVG）用于网页或设计工具。

我们保持轻量：只需几行 Python、一个流行的 SVG 辅助库，以及一点说明。完成后，你将在文件夹中得到一个可直接使用的 `circle.svg`，并且会明白每一步的意义——不再依赖模糊的“查看文档”快捷方式。

## 您需要的环境

- Python 3.8+（任何近期版本均可）
- `svgwrite` 包 – 使用 `pip install svgwrite` 安装
- 文本编辑器或 IDE（VS Code、PyCharm，甚至记事本都可以）
- 对希望保存文件的目录拥有写入权限

就这些。没有笨重的依赖，也不需要外部服务。

## 步骤 1：设置 SVG 文档

创建 SVG 文档就像实例化 `svgwrite` 中的 `Drawing` 对象一样简单。把这个对象想象成所有形状所在的空白画布。

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Why this matters:** `Drawing` 类会为你处理所有 XML 样板——命名空间、头部以及根 `<svg>` 元素。提前指定文件名后，我们已经知道文件最终会保存到哪里，这使得后续的 **save svg file** 步骤变得轻而易举。

### 专业提示
如果你计划在循环中生成大量文件，请为每个 `Drawing` 提供唯一的名称，或使用 `io.BytesIO` 将所有内容保存在内存中，直到准备写入为止。

## 步骤 2：向 SVG 添加圆形

既然文档已经存在，让我们 **add circle to SVG**。`add()` 方法接受任意形状对象；`Circle` 非常适合在中心绘制一个简单的红点。

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Why we use `center` and `radius` variables:** 硬编码数字会让代码难以阅读和维护。通过为数值命名，我们明确了意图——此圆形正好位于 200 × 200 画布的正中心，且足够大以便被注意到。

### 边缘情况 – 透明背景
如果需要透明背景（SVG 的默认设置），可以跳过在根元素上设置 `fill`。若想要白色背景，请添加：

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

在添加圆形之前放置此代码，以便矩形位于下层。

## 步骤 3：保存 SVG 文件

形状就位后，最后一步是 **save SVG file**。`save()` 方法会将 XML 写入磁盘，并且因为我们已经为 `Drawing` 指定了文件名，只需一次调用即可完成。

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **What happens under the hood?** `svgwrite` 将元素树序列化为字符串，添加 XML 声明，并使用 UTF‑8 编码写入。如果目标目录不存在，Python 会抛出 `FileNotFoundError`；请确保路径有效，或使用 `os.makedirs()` 创建目录。

### 额外：以编程方式导出 SVG 图形

如果需要将 SVG 内容作为字符串，例如嵌入 HTML 邮件中，可以调用 `dwg.tostring()` 而不是 `save()`：

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## 完整工作示例

将所有步骤组合起来，下面是一个完整、可直接运行的脚本：

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Expected output:** 运行脚本后，你会在同一文件夹中看到 `circle.svg` 文件。用浏览器或任意矢量编辑器打开，它会显示一个位于白色方块中心的红色圆形——正是我们编写的效果。

## 常见问题与陷阱

- **What if I want a different shape?** 将 `dwg.circle` 替换为 `dwg.rect`、`dwg.ellipse`，或自定义的 `<path>` 字符串即可。API 在各种形状之间保持一致。
- **Can I embed the SVG directly in HTML?** 完全可以。刚创建的文件可以通过 `<img src="circle.svg" alt="Red circle">` 引用，或直接内联为 `<svg>` 标签。
- **Why not write raw XML?** 当然可以，但像 `svgwrite` 这样的库会处理命名空间细节，使代码更易维护——尤其是在你开始添加渐变或动画时。

## 结论

你现在已经掌握了 **create SVG document**、**add circle to SVG** 和 **save SVG file** 的完整流程，能够仅用几行 Python 就 **export graphic as SVG**。这一模式易于扩展：用任意矢量形状替代圆形，循环数据生成图表，或批量处理设计系统的资源。

接下来可以尝试添加文本标签、实验渐变，或在单个脚本中生成整套图标库。如果想了解更高级的功能，请查阅 `svgwrite` 文档中关于组（`<g>`）、变换和动画支持的章节。

祝编码愉快，愿你的矢量图始终保持锐利！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步深入。每个资源都提供完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能，并在自己的项目中探索替代实现方式。

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}