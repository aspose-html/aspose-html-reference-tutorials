---
category: general
date: 2026-06-16
description: 如何在 Python 中快速调整 SVG 大小——加载 SVG 文件、编辑 SVG 文件，甚至使用一个小脚本批量调整 SVG 文件大小。
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: zh
og_description: 如何在 Python 中调整 SVG 大小？学习在 Python 中加载 SVG 文件、编辑 SVG 文件，并使用清晰、可运行的示例批量调整
  SVG 文件大小。
og_title: 如何在 Python 中调整 SVG 大小 – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  headline: How to Resize SVG in Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  name: How to Resize SVG in Python – Step‑by‑Step Guide
  steps:
  - name: '**Collects** every `.svg` file in the source folder.'
    text: '**Collects** every `.svg` file in the source folder.'
  - name: '**Loads** each file using the same routine we used for a single SVG.'
    text: '**Loads** each file using the same routine we used for a single SVG.'
  - name: '**Resizes** to the desired width while keeping the aspect ratio.'
    text: '**Resizes** to the desired width while keeping the aspect ratio.'
  - name: '**Writes** the result to a new folder, leaving originals untouched.'
    text: '**Writes** the result to a new folder, leaving originals untouched.'
  type: HowTo
tags:
- Python
- SVG
- Automation
title: 如何在 Python 中调整 SVG 大小 – 步骤指南
url: /zh/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中调整 SVG 大小 – 完整教程

是否曾想过 **如何在不打开图形编辑器的情况下调整 SVG 大小**？也许你有一个徽标需要在网页横幅中宽度为 200 px，或者你正在为移动应用准备数十个图标。好消息是？你完全可以在 Python 中完成——无需 Photoshop、无需 Inkscape UI，只需几行代码。

在本指南中，我们将逐步演示如何在 Python 中加载 SVG 文件、编辑其尺寸，甚至一次性批量缩放整个文件夹的 SVG。完成后，你将能够 **load SVG file Python**、**edit SVG file Python**，并自信地 **batch resize SVG files**。

## 前置条件

- 已安装 Python 3.8+（使用标准 `python` 命令即可）
- `svgwrite` 或 `lxml` 库 —— 我们将使用 `lxml`，因为它提供直接的 DOM 访问。
- 一个存放待调整大小的 SVG 的文件夹（例如 `assets/icons/`）

无需任何 GUI 工具；所有操作均在终端完成。

---

## 步骤 1：安装所需库

首先，从 PyPI 获取 `lxml`。它体积小、速度快，并且可以直接操作 XML 属性。

```bash
pip install lxml
```

> **小技巧：** 如果你在虚拟环境中工作，请在运行命令前激活它。这可以保持项目依赖的整洁。

## 步骤 2：在 Python 中加载 SVG 文件

现在我们将以 **load SVG file Python** 的方式——读取 XML，获取根 `<svg>` 元素，并打印其当前尺寸。

```python
from lxml import etree

def load_svg(path: str) -> etree._ElementTree:
    """
    Load an SVG document and return the parsed XML tree.
    """
    parser = etree.XMLParser(remove_blank_text=True)
    tree = etree.parse(path, parser)
    return tree

# Example usage
svg_path = "assets/logo.svg"
svg_tree = load_svg(svg_path)
root = svg_tree.getroot()
print(f"Original width: {root.get('width')}, height: {root.get('height')}")
```

**为什么重要：** `lxml` 为我们提供了真实的 DOM，因而可以查询或更改任意属性——这正是 **edit SVG file Python** 任务的理想选择。

## 步骤 3：更改宽度（以及高度） – 如何调整 SVG 大小

SVG 是矢量图形，你可以只设置宽度、只设置高度，或两者同时设置。如果只更改宽度，viewBox 会保持纵横比，但许多工具也会遵循匹配的 height 属性。下面是一个在保持原始纵横比的情况下进行调整的辅助函数：

```python
def resize_svg(tree: etree._ElementTree, new_width: int) -> None:
    """
    Resize the root <svg> element to `new_width` while preserving aspect ratio.
    """
    root = tree.getroot()
    # Grab original dimensions (they may be in px, pt, or just numbers)
    orig_width = float(root.get("width").replace("px", ""))
    orig_height = float(root.get("height").replace("px", ""))

    # Compute scale factor and new height
    scale = new_width / orig_width
    new_height = round(orig_height * scale, 2)

    # Update attributes
    root.set("width", f"{new_width}px")
    root.set("height", f"{new_height}px")

    # Optional: ensure viewBox exists for better scaling in browsers
    if "viewBox" not in root.attrib:
        viewbox = f"0 0 {orig_width} {orig_height}"
        root.set("viewBox", viewbox)

# Resize to 200 px wide
resize_svg(svg_tree, 200)
```

上述函数正是 **how to resize SVG** 的核心。它读取当前尺寸，计算等比例的高度，并将新属性写回文件。

## 步骤 4：保存修改后的 SVG

编辑完成后，需要将更改写回磁盘。这就完成了 **edit SVG file Python** 的整个循环。

```python
def save_svg(tree: etree._ElementTree, destination: str) -> None:
    """
    Write the modified SVG tree to `destination`.
    """
    tree.write(
        destination,
        pretty_print=True,
        xml_declaration=True,
        encoding="UTF-8"
    )
    print(f"Saved resized SVG to {destination}")

# Save as a new file so the original stays untouched
output_path = "assets/logo_resized.svg"
save_svg(svg_tree, output_path)
```

运行完整脚本后，你会看到一个全新的 `logo_resized.svg`，宽度正好为 200 px。

## 步骤 5：批量调整 SVG 文件大小 – 对整个文件夹进行缩放

既然我们已经能够 **load SVG file Python**、**edit SVG file Python** 并保存它们，现在让我们遍历目录，对每个文件执行相同的转换。这就是 **batch resize SVG files** 的答案。

```python
import pathlib

def batch_resize(source_dir: str, target_dir: str, width: int) -> None:
    """
    Resize every .svg file in `source_dir` to `width` pixels and store
    the results in `target_dir`.
    """
    src = pathlib.Path(source_dir)
    tgt = pathlib.Path(target_dir)
    tgt.mkdir(parents=True, exist_ok=True)

    svg_files = list(src.glob("*.svg"))
    if not svg_files:
        print("No SVG files found.")
        return

    for svg_path in svg_files:
        try:
            tree = load_svg(str(svg_path))
            resize_svg(tree, width)
            out_path = tgt / svg_path.name
            save_svg(tree, str(out_path))
        except Exception as e:
            print(f"Failed on {svg_path.name}: {e}")

# Example: resize everything in 'assets/icons' to 64 px wide
batch_resize("assets/icons", "assets/icons_resized", 64)
```

### 这段代码的作用：

1. **收集** 源文件夹中所有 `.svg` 文件。
2. **加载** 每个文件，使用单个 SVG 时相同的例程。
3. **调整大小** 到目标宽度，同时保持纵横比。
4. **写入** 结果到新文件夹，保持原文件不变。

现在你拥有一个可直接使用的 **batch resize SVG files** 流程。

## 步骤 6：边缘情况与常见陷阱

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| 缺少 `width`/`height` 属性 | 有些 SVG 仅依赖 `viewBox`。 | 若属性缺失，回退到 `viewBox` 的尺寸（`viewBox="0 0 w h"`）。 |
| 单位不是 `px`（如 `pt`、`%`） | 脚本仅剥离 `px`。 | 扩展 `replace` 调用或使用正则捕获任意单位。 |
| 复杂的 `<symbol>` 或 `<use>` 元素 | 调整根节点可能不影响嵌套符号。 | 对每个 `<symbol>` 标签同样修改属性，或使用 CSS `transform: scale()`。 |
| 文件名包含 Unicode 或特殊字符 | `pathlib` 能处理大多数情况，但 Windows 可能对某些字符报错。 | 确保文件名为 UTF‑8 安全，或在处理前重命名。 |

提前处理这些问题，可避免后期出现意外破损的图标。

## 步骤 7：验证结果

可以使用一个简短的 HTML 片段快速检查：

```html
<!DOCTYPE html>
<html>
<head><title>SVG Test</title></head>
<body>
  <h3>Original</h3>
  <img src="assets/logo.svg" alt="original logo">
  <h3>Resized</h3>
  <img src="assets/logo_resized.svg" alt="resized logo">
</body>
</html>
```

在浏览器中打开该文件——两张图片应看起来相同，但在开发者工具中，调整后的图像宽度会显示为 **200 px**。

---

## 结论

现在你已经掌握了使用纯 Python **how to resize SVG** 的方法，从单个文件到整个目录。整个工作流涵盖了 **load SVG file Python**、**edit SVG file Python**，以及 **batch resize SVG files**——仅需少量函数即可实现。

动手试一试：尝试不同的宽度，仅调整高度，或使用 `argparse` 添加命令行界面。可能性无限，这段脚本足够轻量，可嵌入构建流水线、CI 作业或桌面工具中。

对处理渐变、嵌入字体，或将其集成到 Flask 应用有疑问？留下评论，我们一起探索这些细节。祝编码愉快！


## 接下来你应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方案。每个资源都提供完整的可运行代码示例和逐步解释。

- [使用 Aspose.HTML 将 SVG 转换为图像（.NET）](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [使用 Aspose.HTML 将 SVG 转换为 PDF（.NET）](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [使用 Aspose.HTML 将 SVG 文档呈现为 PNG（.NET）](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}