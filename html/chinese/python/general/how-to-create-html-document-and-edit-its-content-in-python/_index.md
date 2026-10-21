---
category: general
date: 2026-08-25
description: 学习如何使用简单的 Python 脚本创建 HTML 文档、选择元素 CSS、修改 HTML 文本并保存 HTML 文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: zh
lastmod: 2026-08-25
og_description: 使用几行 Python 创建 HTML 文档，选择元素的 CSS，修改 HTML 文本并保存 HTML 文件。请遵循本完整教程。
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: 使用 Python 创建 HTML 文档并编辑其内容 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: 如何在 Python 中创建 HTML 文档并编辑其内容
url: /zh/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中创建 HTML 文档并编辑其内容

如果您需要从头**create html document**并以编程方式更改其元素，本指南将准确展示操作方法。您将看到一个简短且可运行的脚本，它会创建文件、使用 CSS 选择器选择段落、更新文本，并将结果写回磁盘。

在 Python 中处理 HTML 在生成报告、电子邮件模板或静态站点内容时很常见。完成本教程后，您将能够**select element css**、**modify html text**和**save html file**，而无需离开 IDE 的舒适环境。

## 前置条件

* 已安装 Python 3.9 或更高版本。
* `beautifulsoup4` 和 `lxml` 包（使用 `pip install beautifulsoup4 lxml` 安装）。
* 对计划存放输出文件的目录具有写入权限。

无需额外工具；标准库已处理文件 I/O。

## 步骤 1：安装所需库

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` 提供了便捷的 API 用于解析和操作 HTML，而 `lxml` 则提供了能够理解 CSS 选择器的高速解析器。

## 步骤 2：创建初始 HTML 文档

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

`BeautifulSoup` 构造函数在内存中构建一个**create html document**对象。使用 `"lxml"` 解析器可确保完整的 CSS 选择器支持。

## 步骤 3：使用 CSS 选择器选择段落元素

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

`select_one` 方法实现了**select element css**逻辑，返回第一个匹配的标签。如果选择器未匹配到任何内容，`para` 将为 `None`，因此在生产代码中建议进行防御性检查。

## 步骤 4：修改段落的文本内容

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

给 `para.string` 赋值会执行**modify html text**操作。BeautifulSoup 会更新底层 DOM 树，因此在文档序列化时会体现出该更改。

## 步骤 5：将更新后的 HTML 保存到文件

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

`open` 调用配合 `write` 实现了**save html file**功能。使用 `prettify()` 可以生成良好缩进的输出，这在调试时非常有帮助。

### 完整脚本，快速复制‑粘贴

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

运行 `python edit_html.py` 会生成包含以下内容的 `updated.html`：

```html
<p>
 New
</p>
```

## 常见变体和边缘情况

### 选择多个元素

如果您需要**select element css**选择器匹配多个标签（例如 `"div.note"`），请使用 `doc.select("div.note")`，它会返回一个列表。遍历该列表即可对每个元素应用更改。

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### 保持已有属性

当您替换文本时，BeautifulSoup 会保留标签上的所有属性。例如：

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### 优雅地处理缺失元素

在生产脚本中，您经常会遇到结构不完整的 HTML。像步骤 4 中展示的那样，将选择操作包装在条件判断或 try‑except 块中，以避免崩溃。

### 写入特定目录

将 `output_path` 替换为绝对路径或相对路径：

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

确保目录已存在；否则，Python 将抛出 `FileNotFoundError`。

## 专业提示

* **Performance** – 对于大型 HTML 文件，建议直接使用 `lxml.etree`；BeautifulSoup 虽然方便，但会增加一层轻量抽象，速度略慢。
* **Encoding** – 始终使用 `encoding="utf-8"` 打开文件，以保留非 ASCII 字符。
* **Testing** – 修改后，您可以在单元测试中使用 `assert "New" in open(output_path).read()` 来验证输出。

## 结论

现在您已经掌握了如何使用 Python **create html document**、使用 **select element css** 查询定位节点、**modify html text**，以及最终 **save html file**。该模式可扩展到更复杂的转换，如批量更新、属性修改或模板生成。

接下来，您可以探索相关主题，例如使用 XPath 表达式**how to edit html**、使用 Jinja2 生成完整 HTML 页面，或自动化批量处理多个文件。所有这些都基于本教程展示的核心步骤，进一步扩展您对程序化 HTML 操作的工具箱。

## 接下来应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [使用 Aspose.HTML 创建 HTML 文档 – 步骤指南](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [如何在 Aspose.HTML for Java 中编辑 HTML 文档树](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [在 Aspose.HTML for Java 中保存 HTML 文档](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}