---
category: general
date: 2026-09-19
description: 学习如何使用 Python 更改 HTML 文件中的标题。本指南涵盖读取 HTML、更新标题标签以及保存修改后的 HTML。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change title
- update html title
- read html with python
- load html file python
- save modified html
language: zh
lastmod: 2026-09-19
og_description: 如何使用 Python 更改 HTML 文件中的标题。请参考完整示例，读取 HTML，更新 title 标签，并保存修改后的文档。
og_image_alt: Diagram showing how to change title in an HTML file using Python
og_title: 如何使用 Python 更改 HTML 文件的标题 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Learn how to change title in an HTML file with Python. This guide covers
    reading HTML, updating the title tag, and saving the modified HTML.
  headline: How to change title in an HTML file using Python
  type: TechArticle
tags:
- Python
- HTML
- Web scraping
title: 如何使用 Python 更改 HTML 文件中的标题
url: /zh/python/general/how-to-change-title-in-an-html-file-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 更改 HTML 文件中的标题

如果您需要在 HTML 文档中以编程方式 **how to change title**，Python 可以轻松完成此任务。在本教程中，您将读取一个 HTML 文件，更新 `<title>` 元素，并将修改后的 HTML 保存回磁盘——全部使用清晰、可运行的代码。

更改页面标题是生成静态站点、定制抓取页面或自动化 SEO 更新时的常见步骤。阅读完本指南后，您将了解如何 **update html title**，如何 **read html with python**，以及如何安全地 **save modified html**。

## 前置条件

- 已安装 Python 3.8 或更高版本  
- `beautifulsoup4` 包（`pip install beautifulsoup4`）  
- 您想要编辑的 HTML 文件（示例使用您选择的文件夹中的 `index.html`）  

无需外部服务；所有操作均在本地运行。

## 步骤 1：使用 Python 加载 HTML 文件  

第一步是以 **load html file python**‑style 加载 HTML 文件。使用 `BeautifulSoup` 可以获得一个宽容的解析器，能够处理不完美的标记。

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Define the directory that holds the original HTML
html_dir = Path("YOUR_DIRECTORY")
original_path = html_dir / "index.html"

# Read the file contents (this is how you **read html with python**)
with original_path.open(encoding="utf-8") as f:
    html_content = f.read()

# Parse the document
soup = BeautifulSoup(html_content, "html.parser")
```

*此步骤的重要性:*  
`BeautifulSoup` 构建树形结构，使您能够在无需手动字符串处理的情况下查询和修改元素。内置的 `html.parser` 速度快且不需要额外的二进制文件。

## 步骤 2：定位 `<title>` 元素  

HTML 文档通常在 `<head>` 中包含唯一的 `<title>` 标签。我们检索第一次出现的该标签，以满足 **update html title** 的需求。

```python
# Find the first <title> element; BeautifulSoup returns None if missing
title_tag = soup.find("title")

if title_tag is None:
    # If the document lacks a <title>, create one inside <head>
    head_tag = soup.find("head")
    if head_tag is None:
        # As a safety net, add a <head> element at the top
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

# Show the current title (useful for debugging)
print("Current title:", title_tag.string)
```

*为什么要检查 `None`*：  
某些 HTML 片段可能没有标题。自动添加标题可以防止后续错误并保持脚本的健壮性。

## 步骤 3：更改标题文本  

现在我们通过为标签的 string 赋予新文本来 **update html title**。这就是 **how to change title** 操作的核心。

```python
new_title = "New Title"

# Replace the existing title text
title_tag.string = new_title

print("Updated title:", title_tag.string)
```

`string` 属性表示 `<title>` 内的文本节点。覆盖它即可在内存中更新 DOM。

## 步骤 4：保存修改后的 HTML  

最后，将修改后的文档写入新文件。这完成了 **save modified html** 步骤，并保持原文件不变。

```python
# Define the output path
modified_path = html_dir / "index_modified.html"

# Write the prettified HTML back to disk
with modified_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_path}")
```

`prettify()` 使用缩进格式化输出，使更改后的文件更易阅读。

### 预期输出

在原始包含以下内容的示例 `index.html` 上运行脚本：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Old Title</title>
</head>
<body>
    <h1>Welcome</h1>
</body>
</html>
```

将在控制台产生类似以下的输出：

```
Current title: Old Title
Updated title: New Title
Modified HTML saved to YOUR_DIRECTORY/index_modified.html
```

保存的 `index_modified.html` 将以以下内容开头：

```html
<!DOCTYPE html>
<html>
 <head>
  <title>
   New Title
  </title>
 </head>
 <body>
  <h1>
   Welcome
  </h1>
 </body>
</html>
```

## 完整脚本，快速复制‑粘贴

下面是完整的、可直接运行的程序，结合了所有四个步骤。将其保存为 `change_title.py` 并根据需要调整 `YOUR_DIRECTORY`。

```python
# change_title.py
from pathlib import Path
from bs4 import BeautifulSoup

# ----------------------------------------------------------------------
# Configuration – change these values to match your environment
# ----------------------------------------------------------------------
html_dir = Path("YOUR_DIRECTORY")          # Folder containing index.html
original_file = html_dir / "index.html"
modified_file = html_dir / "index_modified.html"
new_title = "New Title"                    # Desired title text
# ----------------------------------------------------------------------

# 1️⃣ Load the HTML file (read html with python)
with original_file.open(encoding="utf-8") as f:
    html_content = f.read()

soup = BeautifulSoup(html_content, "html.parser")

# 2️⃣ Locate or create the <title> element
title_tag = soup.find("title")
if title_tag is None:
    head_tag = soup.find("head")
    if head_tag is None:
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

print("Current title:", title_tag.string)

# 3️⃣ Update the title (how to change title)
title_tag.string = new_title
print("Updated title:", title_tag.string)

# 4️⃣ Save the modified HTML (save modified html)
with modified_file.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_file}")
```

运行脚本：

```bash
python change_title.py
```

您将看到控制台消息以及包含更新后标题的新 `index_modified.html` 文件。

## 其他提示和边缘情况

| 情况 | 处理方法 |
|-----------|------------|
| **多个 `<title>` 标签** | `soup.find_all("title")` 返回一个列表；更新第一个元素，或在需要更改全部时遍历。 |
| **编码问题** | 如果存在 BOM，请使用 `encoding="utf-8-sig"` 打开文件，或使用 `chardet` 检测编码。 |
| **大型 HTML 文件** | 使用 `lxml` 解析器（`BeautifulSoup(html_content, "lxml")`）以获得更好性能。 |
| **保留原始格式** | 如果必须保留精确的空白，请使用 `str(soup)` 而不是 `prettify()`。 |
| **跨多个文件自动化** | 将逻辑封装在函数中，并遍历 `Path.rglob("*.html")`。 |

这些变体在保持核心 **how to change title** 逻辑不变的同时，适应了实际项目的需求。

## 结论

您现在了解如何使用 Python 在任何 HTML 文档中 **how to change title**。本教程涵盖了读取 HTML、定位 `<title>` 标签、更新其文本以及安全地 **save modified html**。通过完整脚本，您可以将此模式集成到静态站点生成器、SEO 流程或任何需要动态更改标题的自动化任务中。

接下来，探索相关主题，例如用于提取 meta 标签的 **read html with python**，或用于处理错误标记的 **load html file python** 技术。尝试批量处理以在整个网站中更新标题——您新掌握的技能是众多网页自动化任务的基础。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方式。

- [如何使用 Aspose.Html 保存 HTML – 完整 C# 指南](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [如何在 C# 中保存 HTML – 使用自定义资源处理器的完整指南](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [如何将 HTML 渲染为 PNG – 完整分步指南](/html/english/net/rendering-html-documents/how-to-render-html-to-png-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}