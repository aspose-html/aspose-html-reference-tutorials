---
category: general
date: 2026-06-07
description: 如何使用 Python 为 HTML 标题添加前缀。学习选择多个标题、更改 HTML 标题，并高效保存修改后的 HTML。
draft: false
keywords:
- how to add prefix
- select multiple headings
- save modified html
- change html titles
- modify html with python
language: zh
og_description: 如何使用 Python 为 HTML 标题添加前缀。本教程展示了如何选择多个标题、更改 HTML 标题，并仅用几行代码保存修改后的
  HTML。
og_title: 使用 Python 为 HTML 标题添加前缀 – 快速指南
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  headline: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  name: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  steps:
  - name: Verify the changes in a diff tool.
    text: Verify the changes in a diff tool.
  - name: Roll back instantly if something looks off.
    text: Roll back instantly if something looks off.
  - name: Keep the original untouched for audit purposes.
    text: Keep the original untouched for audit purposes.
  type: HowTo
tags:
- Python
- HTML
- Automation
- Web Scraping
title: 如何使用 Python 为 HTML 标题添加前缀——一步一步指南
url: /zh/python/general/how-to-add-prefix-to-html-headings-with-python-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 为 HTML 标题添加前缀 – 完整教程

在维护经常更新的网站时，使用 Python 为 HTML 标题添加前缀是一项常见需求。在本指南中，我们将逐步演示如何选择多个标题、修改 HTML 标题，并保存修改后的 HTML——全部在编辑器中完成。  

如果你曾想过是否可以在数十个页面上自动化“标记为已更新”徽章，那么你来对地方了。我们还将介绍如何以可扩展的方式 **modify html with python**，这样你就不必手动打开每个文件。

## 你将实现的目标

* **选择多个标题** (`h1`, `h2`, `h3`) 一次性完成。  
* **为每个标题文本添加自定义前缀**（例如 `[Updated]`）。  
* **保存修改后的 html** 回磁盘，保留原始文件结构。  
* 了解不同 Python HTML 解析器之间的取舍，并选择最适合你项目的解析器。

无需外部服务，也不需要庞大的框架——只需纯 Python 和几个维护良好的库。

---

## 如何在 Python 中为标题文本添加前缀

下面是一个最小可运行的示例，演示核心思路。它使用 **`lxml`** 库结合 **`cssselect`** 提供选择器支持，类似于原始代码片段中看到的 `query_selector_all` 方法。

```python
# -------------------------------------------------
# Step 0: Install dependencies (run once)
# -------------------------------------------------
# pip install lxml cssselect

# -------------------------------------------------
# Step 1: Load the HTML document
# -------------------------------------------------
from lxml import html

# Replace with your actual file path
input_path = "YOUR_DIRECTORY/article.html"
with open(input_path, "r", encoding="utf-8") as f:
    doc = html.fromstring(f.read())

# -------------------------------------------------
# Step 2: Select multiple headings (h1, h2, h3)
# -------------------------------------------------
# The CSS selector "h1, h2, h3" grabs all three levels.
headings = doc.cssselect("h1, h2, h3")

# -------------------------------------------------
# Step 3: Add the prefix "[Updated] " to each heading
# -------------------------------------------------
prefix = "[Updated] "
for heading in headings:
    # Preserve existing whitespace but prepend our tag
    heading.text = f"{prefix}{heading.text_content().strip()}"

# -------------------------------------------------
# Step 4: Save the modified HTML
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/article_updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

print(f"✅ Finished! Modified file saved to {output_path}")
```

**预期输出**（摘自 `article_updated.html`）：

```html
<h1>[Updated] Introduction to Machine Learning</h1>
<h2>[Updated] Data Pre‑processing Steps</h2>
<h3>[Updated] Feature Engineering Techniques</h3>
```

请注意，每个标题现在都以 `[Updated]` 标签开头——这正是我们在询问 **how to add prefix** 时想要的效果。

### 为什么这种方法有效

* **`lxml` + `cssselect`** 为你提供完整的 CSS 选择器功能，使“选择多个标题”步骤可以一行代码完成。  
* `text_content()` 方法安全地提取内部文本，避免 HTML 实体或子标签。  
* 使用 `pretty_print=True` 写回时保持文件可读性，这对版本控制的差异查看非常有用。

---

## 使用 CSS 选择器选择多个标题

如果你来自 JavaScript 背景，`cssselect` 语法会让你感觉很熟悉。选择器 `"h1, h2, h3"` 是一个 **逗号分隔的列表**，表示“获取匹配这三者中任意一个的元素”。  

你可以进一步扩大范围：

```python
# Grab every heading from h1 through h6
all_headings = doc.cssselect("h1, h2, h3, h4, h5, h6")
```

或缩小到特定区域：

```python
# Only headings inside the <article> tag
article_headings = doc.cssselect("article h1, article h2, article h3")
```

这些细微的调整让你能够 **select multiple headings**，精准定位，这在拥有庞大文档站点且只想更新某个子章节时尤为有用。

## 安全地保存修改后的 HTML 文件

当你 **save modified html** 时，需要避免损坏原始文件。上面展示的模式会写入新文件（`article_updated.html`），这样你可以：

1. 在差异工具中验证更改。  
2. 如果出现问题，立即回滚。  
3. 保持原始文件未被修改，以便审计。

如果你更喜欢就地编辑，只需交换路径：

```python
import shutil
shutil.move(output_path, input_path)  # Overwrites the original
```

但请记住：在覆盖之前 **始终备份**，尤其是在生产服务器上。

## 更改 HTML 标题 与 标题（Headings） 的区别

你可能会想，“changing HTML titles” 是否等同于给标题添加前缀。按照 HTML 术语，`<title>` 标签位于 `<head>` 中，控制浏览器标签页标题，而标题（`<h1>…<h3>`）出现在页面正文中。

如果你还需要 **change html titles**，同样的 `lxml` 工作流也适用：

```python
# Change the <title> tag
title_elem = doc.find(".//title")
if title_elem is not None:
    title_elem.text = f"{prefix}{title_elem.text}"
```

现在页面标题和可见的标题都带有相同的 `[Updated]` 标记——这对于希望在元数据和页面内容之间保持一致性的 SEO 审计非常理想。

## 用于 **modify html with python** 的替代库

虽然 `lxml` 速度快且功能丰富，但你可能已经在项目中使用 **BeautifulSoup**（bs4）。下面是更“pythonic” 风格的相同逻辑：

```python
from bs4 import BeautifulSoup

with open(input_path, "r", encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")

for tag in soup.select("h1, h2, h3"):
    tag.string = f"{prefix}{tag.get_text(strip=True)}"

with open(output_path, "w", encoding="utf-8") as f:
    f.write(str(soup.prettify()))
```

这两个库都能让你 **modify html with python**，因此请选择与你现有技术栈匹配的库。`BeautifulSoup` 在需要宽容解析错误标记时表现出色，而 `lxml` 在大批量处理时速度更快。

## 专业技巧与常见陷阱

* **编码很重要**——始终使用 `encoding="utf-8"` 打开文件，以避免非 ASCII 字符的 Unicode 错误。  
* **避免双重前缀**——如果脚本运行两次，你会得到 `[Updated] [Updated] …`。通过检查 `heading.text.startswith(prefix)` 来防止这种情况。  
* **保留空白**——`strip()` 调用会去除多余空格，使输出保持整洁。  
* **批量处理**——将整个流程包装在 `for file in pathlib.Path("YOUR_DIRECTORY").glob("*.html"):` 循环中，以单个命令更新整个文件夹。  

## 完整工作示例：批量更新目录

下面是一个紧凑的脚本，它遍历目录中的每个 `.html` 文件，为标题添加前缀，更新 `<title>`，并写入一个带有 `_updated` 后缀的新文件。

```python
import pathlib
from lxml import html

prefix = "[Updated] "
source_dir = pathlib.Path("YOUR_DIRECTORY")
output_dir = source_dir / "updated"
output_dir.mkdir(exist_ok=True)

for html_path in source_dir.glob("*.html"):
    # Load
    with open(html_path, "r", encoding="utf-8") as f:
        doc = html.fromstring(f.read())

    # Headings
    for h in doc.cssselect("h1, h2, h3"):
        if not h.text_content().startswith(prefix):
            h.text = f"{prefix}{h.text_content().strip()}"

    # Title
    title_elem = doc.find(".//title")
    if title_elem is not None and not title_elem.text.startswith(prefix):
        title_elem.text = f"{prefix}{title_elem.text}"

    # Save
    out_path = output_dir / f"{html_path.stem}_updated.html"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

    print(f"✅ Processed {html_path.name} → {out_path.name}")
```

运行一次后，`YOUR_DIRECTORY` 中的每个 HTML 文件都会获得新的 `[Updated]` 徽章——无需手动编辑。

## 结论

我们已经介绍了使用 Python **how to add prefix** 到 HTML 标题的方式，演示了如何 **select multiple headings**，展示了如何安全地 **save modified html**，甚至涉及了 **change html titles** 以实现完整改造。通过使用 `lxml` 或 `BeautifulSoup`，你现在拥有了在实际项目中 **modify html with python** 的坚实工具箱。

下一步？尝试使用时间戳而不是静态标签，或生成一个列出所有已修改文件的变更日志文件。你还可以将此脚本挂接到 CI 流水线，使每次部署自动

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方式。

- [如何使用 Aspose.HTML for Java 编辑 HTML](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [如何在 Aspose.HTML for Java 中为 HTML 文档添加 CSS – 内联 CSS](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [如何在 Java 中查询 HTML – 完整教程](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}