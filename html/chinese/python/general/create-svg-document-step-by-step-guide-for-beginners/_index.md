---
category: general
date: 2026-07-02
description: 使用 Python 快速创建 SVG 文档。学习保存 SVG 文件、生成基本 SVG 图像，并仅用几行代码导出 SVG。
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: zh
og_description: 轻松创建 SVG 文档。本指南展示了如何生成 SVG、保存 SVG 文件，以及使用简洁的 Python 示例从代码导出 SVG。
og_title: 创建 SVG 文档 – 快速 Python 教程
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: 创建 SVG 文档——初学者分步指南
url: /zh/python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 SVG 文档 – 初学者分步指南

有没有想过在不打开图形编辑器的情况下 **create SVG document**？你并不是唯一有这种想法的人。无论你需要一个用于网页的微型图标，还是实时生成的动态图表，能够以编程方式 **create SVG document** 都能节省时间，并且让所有内容都受到版本控制。

在本教程中，我们将逐步演示一个完整且可运行的示例，向您展示如何 **create SVG document**、**save SVG file**，甚至解答在自动化图形时经常出现的 “**how to generate SVG**” 问题。完成后，您将在磁盘上得到一个红色方块，并且了解如何 **export SVG from code** 用于任何后续项目。

## 您需要的准备

* Python 3.9 或更高版本（标准库已完成所有繁重工作）
* 您喜欢的文本编辑器或 IDE——VS Code、PyCharm，甚至记事本都可以
* 对您将 **save SVG file** 的文件夹拥有写入权限（我们将使用 `output/` 目录）

无需外部包，设置只需几分钟。

## 步骤 1：设置 SVG 辅助函数（创建文档）

首先，我们需要一个小型助手来构建 SVG 背后的 XML 结构。可以把它看作我们稍后将 **create basic SVG image** 元素绘制在其上的画布。

```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**此步骤的重要性：** `SVGDocument` 类抽象了低层的 XML 操作。将其封装在类中可以保持其余代码的整洁，这在更大的应用中 **export SVG from code** 时是最佳实践。

## 步骤 2：添加矩形 – **Create Basic SVG Image** 示例的核心

现在我们已有文档对象，让我们加入一个红色方块。这是本教程中 **create basic SVG image** 部分的核心。

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**解释：**  
* 矩形的 `x` 和 `y` 坐标设为 10 像素的边距，使其不紧贴边缘。  
* 使用字典来存放属性使代码更易读，并且与在任何基于 XML 的格式中 **save SVG file** 属性的方式相吻合。  
* 如果您需要 **how to generate SVG** 除矩形之外的形状，只需将标签改为 `"circle"` 或 `"path"` 并相应地调整属性字典。

## 步骤 3：持久化 SVG – 最终 **Save SVG File** 到磁盘

我们已经在内存中构建了文档；现在将其写入磁盘。这就是抽象的 **create SVG document** 变成可在浏览器中打开的实际文件的时刻。

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**您将看到的内容：** 在 Chrome、Firefox 或任何支持 SVG 的查看器中打开 `output/square.svg`，会显示一个带有细白色边框的简单红色方块（SVG 画布的背景）。这证明我们已经成功 **exported SVG from code**。

## 完整脚本 – 单文件解决方案

下面是完整脚本，可直接复制粘贴到 `create_svg.py`。运行 `python create_svg.py` 将生成上述文件。

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### 预期输出

运行脚本后会打印：

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

生成的 `square.svg` 如下所示（简化视图）：

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

打开文件会渲染出清晰的红色方块——正是我们想要 **create basic SVG image** 的效果。

## 扩展示例 – 常见问题解答

### 如何添加文本或其他形状？

只需调用 `svg.create_element("text", {...})` 或 `svg.create_element("circle", {...})`，并像矩形一样将其追加。相同的 **how to generate SVG** 逻辑适用。

### 如果需要 **export SVG from code** 并使用透明背景怎么办？

从根 `<svg>` 元素中移除任何 `fill` 属性，或对需要透明的形状设置 `fill="none"`。XML 仍然有效，浏览器会自动渲染透明效果。

### 我可以使用美化格式 **save SVG file** 吗？

`ElementTree` writes compact XML by default. For a human‑readable version, you can use `xml.dom.minidom` to re‑format:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

将 `svg.save(output_path)` 替换为 `pretty_save(svg, output_path)`。

### 大型 SVG 的性能如何？

在生成成千上万的元素时，建议先构建 `ET.Element` 对象的列表，然后一次性扩展根节点。这样可以减少树的变更次数，加快 **save SVG file** 操作的速度。

## 专业技巧与常见陷阱

* **专业提示：** 在 **saving SVG file** 时始终使用绝对路径（或 `pathlib.Path`）；相对路径在脚本从不同工作目录运行时可能会失效。  
* **注意：** 忘记注册 SVG 命名空间。若未调用 `ET.register_namespace("", SVGDocument.SVG_NS)`，输出会包含冗余的 `ns0` 前缀，某些浏览器会误解。  
* **常见错误：** 在属性值中混用整数和字符串。XML 需要字符串，因此我们使用 `str()` 将所有内容转换——辅助类已经为您完成此操作，但如果绕过它，可能会出现 `TypeError`。  

## 结论

我们刚刚完整地演示了一个端到端的示例，展示了如何 **create SVG document**、**save SVG file**，以及回答

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本教程展示的技术进行扩展。每个资源都包含完整的可运行代码示例和分步说明，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [在 Aspose.HTML for Java 中保存 SVG 文档](/html/english/java/saving-html-documents/save-svg-document/)
- [在 Aspose.HTML for Java 中创建和管理 SVG 文档](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg 转 png java – 使用 Aspose.HTML for Java 将 SVG 转换为图像](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}