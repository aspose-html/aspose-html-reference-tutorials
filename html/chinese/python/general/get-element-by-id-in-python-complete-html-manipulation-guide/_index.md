---
category: general
date: 2026-05-31
description: 学习如何使用 Python 通过 ID 获取元素、修改 HTML 背景颜色、读取 HTML 文本以及设置 HTML 属性。一步一步的教程。
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: zh
og_description: 使用 Python 获取元素 ID、读取 HTML 文本、设置 HTML 属性并更改背景颜色的简明指南。
og_title: 在Python中通过ID获取元素 – 完整HTML操作教程
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: 在 Python 中通过 ID 获取元素 – 完整的 HTML 操作指南
url: /zh/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中通过 id 获取元素 – 完整的 HTML 操作指南

是否曾在编写快速 Python 脚本时需要 **get element by id** 从 HTML 页面中获取元素？你并不孤单——大多数开发者在开始爬取站点或调整本地报告时都会遇到这个难题。好消息是，只需几行代码，你就可以读取元素的文本、改变其背景颜色，甚至设置新属性，全部在编辑器中完成。

在本教程中，我们将演示一个真实案例：加载本地 `sample.html`，获取 ID 为 `main‑content` 的元素，打印其内部文本，最后将背景颜色更改为浅灰色。完成后，你还将了解 **how to read HTML text**、**how to set HTML attribute**，以及为何 **manipulate HTML with Python** 是任何自动化工具箱中实用的技能。

## 你需要的环境

- **Python 3.9+**（任何近期版本均可）
- **`lxml`** 库（如果你更喜欢也可以使用 **BeautifulSoup**）——我们将使用 `lxml.html`，因为它提供了类似 `get_element_by_id` 的简洁 API。
- 一个名为 `sample.html` 的小型 HTML 文件，放在名为 `YOUR_DIRECTORY` 的文件夹中。可以随意将下面的代码片段复制到该文件中：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

就这么简单——无需任何花哨的框架，只需纯 Python 和一个静态 HTML 文件。

## 第一步：安装所需库

如果尚未安装 `lxml`，打开终端并运行：

```bash
pip install lxml
```

*小技巧：* 使用虚拟环境可以保持全局 Python 环境整洁，尤其是在处理多个项目时。

## 第二步：加载 HTML 文档

现在我们将把文件读取为 `lxml.html` 文档对象。可以把它看作是将原始文本转换为可遍历的树结构。

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

运行后会打印 “Document loaded successfully.” 如果文件未找到，Python 将抛出 `FileNotFoundError`——建议尽早捕获，以免追踪不存在的元素。

## 第三步：通过 id 获取元素

这就是关键所在。`lxml` 提供了方便的 `get_element_by_id` 方法，类似于在 JavaScript 中使用的 DOM API。

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

当元素存在时，控制台会打印 “Element found!”。这就是 **get element by id** 步骤，为我们后续的大多数操作提供支持。

## 第四步：如何读取 HTML 文本

获得元素后，提取其可见文本轻而易举。`text_content()` 方法返回内部的所有内容，去除标签。

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Expected output:

```
Inner text: Hello, world! This is the original text.
```

你可能会想，*如果元素包含嵌套标签怎么办？* `text_content()` 仍然有效——它会连接所有子孙文本节点，给你一个干净的字符串，便于记录、存储或用于其他算法。

## 第五步：如何设置 HTML 属性

更改或添加属性同样简单。`set` 方法允许你为任意属性名赋值。

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Output:

```
New attribute value: true
```

该行演示了 **how to set HTML attribute** 的即时操作。你可以将 `"data-modified"` 替换为 `"class"`、`"title"` 或元素支持的其他属性。

## 第六步：更改 HTML 背景颜色

接下来进行视觉微调。要更改背景颜色，我们注入一个覆盖默认值的 `style` 属性。

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

运行脚本后，打开浏览器查看 `sample.html` 中的 `div` 将呈现如下：

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

这就是可复用的 **change background colour html** 技巧，适用于任何元素——只需更换颜色代码即可。

## 第七步：使用 Python 操作 HTML – 综合示例

下面是完整的可运行脚本，整合了所有步骤。将其保存为 `modify_html.py`，并在与你的 `YOUR_DIRECTORY` 文件夹相同的目录下执行。

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### 脚本逐行说明

1. **Imports** `lxml.html` 用于解析，`pathlib` 用于跨平台路径。  
2. **Loads** `sample.html`，如果文件缺失则以明确错误中止。  
3. **Retrieves** 元素，使用 **get element by id**。  
4. **Prints** 元素的文本——展示 **how to read HTML text**。  
5. **Adds** 自定义属性，说明 **how to set HTML attribute**。  
6. **Changes** 背景颜色，满足 **change background colour html** 的需求。  
7. **Writes** 更新后的标记到 `sample_modified.html`，以便在浏览器中打开查看更改。

运行脚本后，控制台输出类似于：

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

打开 `sample_modified.html`，你会看到文字后面的灰色背景——这证明 **manipulate HTML with python** 确实有效。

## 常见陷阱及规避方法

- **Missing ID** – 如果目标元素不存在，`get_element_by_id` 会返回 `None`。在访问属性前务必检查是否为 `None`，否则会触发 `AttributeError`。  
- **Encoding issues** – 读取非 ASCII 页面时，向 `html.parse` 传入 `encoding='utf-8'`，或确保文件以 UTF‑8 保存。  
- **Overwriting existing styles** – 设置 `style` 属性会覆盖之前的内联样式。如果需要保留已有规则，先读取当前的 `style` 值，追加新规则后再写回。  
- **File permissions** – 在只读系统中写回同一文件夹可能失败。请选择可写的输出路径，如我们使用的 `sample_modified.html`。

## 扩展示例

既然你已经掌握了基础，考虑以下进阶步骤：

- **Loop over multiple IDs** – 使用 ID 列表并通过 `for` 循环遍历，以批量处理页面的各个部分。  
- **Replace text content** – 调用 `elem.text = "New text"` 来修改可见字符串。  
- **Add child elements** – 使用 `

## 接下来该学习什么？

- [如何使用 Aspose.HTML for Java 编辑 HTML](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [如何在 Java 中查询 HTML – 完整教程](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [如何将 HTML 转换为 PDF（Java） – 使用 Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}