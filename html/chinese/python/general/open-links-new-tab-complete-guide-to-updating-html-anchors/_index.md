---
category: general
date: 2026-07-05
description: 使用 Python 在新标签页打开链接——学习如何添加 target="_blank"，更改链接目标，使用属性包含选择器，并轻松保存修改后的
  HTML。
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: zh
og_description: 快速在新标签页打开链接。本教程展示如何添加 target="_blank"，更改链接目标，并使用 Python 保存修改后的 HTML。
og_title: 在新标签页打开链接 – 步骤详解 HTML 更新指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: 在新标签页打开链接 – HTML锚点更新完整指南
url: /zh/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在新标签页打开链接 – 更新 HTML 锚点的完整指南

是否曾经需要在静态 HTML 页面上 **open links new tab**，但不知从何入手？你并不孤单。许多开发者在清理旧站点或添加可访问性改进时都会遇到这个问题。在本教程中，我们将演示一个实用的解决方案，能够 **adds target blank**、**changes link target**，并安全地 **saves modified html**——只需几行 Python 代码。

我们还会介绍如何使用 **attribute contains selector**，只处理你真正关心的锚点（例如，所有指向 *example.com* 的链接）。完成后，你将拥有一个可复用的脚本，能够在任何项目中使用，无论规模大小。

## 你将学到

- 将 HTML 文件加载到可操作的文档对象中。  
- 选择 `href` 属性包含特定子字符串的 `<a>` 元素。  
- **Add target blank** 并设置 `rel="noopener"` 属性以提升安全性。  
- **Save modified html** 回写到磁盘而不丢失格式。  

无需除标准库和 **beautifulsoup4**（一个小型安装）之外的外部依赖。如果你已经在使用其他解析器，这些概念同样适用。

---

## 前置条件

- 在机器上安装了 Python 3.8+。  
- 具备 HTML 和 Python 的基础知识。  
- `beautifulsoup4` 包（`pip install beautifulsoup4`）。  

就是这样——无需重量级框架。

---

## 步骤 1：加载 HTML 文档

首先，我们需要读取源文件并交给 BeautifulSoup。可以把它想象成打开一块空白画布，以便绘制新的属性。

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Why this matters:** 使用 `Path` 使代码保持跨操作系统兼容，且 `html.parser` 为内置解析器，简单任务无需额外解析器。

---

## 步骤 2：使用 Attribute Contains Selector 查找目标链接

我们只想处理指向 *example.com* 的锚点。CSS 选择器 `a[href*='example.com']` 正好实现了这一点——`*=` 表示“包含”。BeautifulSoup 的 `select` 方法支持此语法。

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro tip:** 如果需要不区分大小写的匹配，可以改用小循环检查 `if 'example.com' in a.get('href', '').lower()`。

现在 `anchor_elements` 包含了我们关心的所有链接，准备进行下一步转换。

---

## 步骤 3：更改链接目标 – 添加 Target Blank 并确保链接安全

在新标签页打开链接只需设置 `target="_blank"` 即可。不过，现代浏览器建议同时添加 `rel="noopener"`（或 `noreferrer`），以防新打开的页面通过 `window.opener` 访问原窗口。此小小的安全改动可以阻止网络钓鱼攻击。

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Why we use direct dictionary assignment:** 它会在属性缺失时自动创建，若已存在则覆盖——非常适合 **change link target** 操作。

---

## 步骤 4：将修改后的 HTML 保存回磁盘

最后一步是将更新后的标记写入新文件。保留原始文件不变，以便在出现问题时能够回滚。

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **What `prettify()` does:** 它为 HTML 添加良好的缩进，使保存的文件更易阅读和对比。如果你更喜欢原始空白，使用 `str(soup)` 替代 `prettify()`。

---

## 完整脚本 – 一键解决方案

下面是完整的、可直接运行的脚本。将其保存为 `update_links.py`，然后在终端中执行 `python update_links.py`。

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### 预期结果

假设 `links.html` 原始内容如下：

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

运行脚本后，`links-updated.html` 将如下所示：

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

只有指向 *example.com* 的链接被添加了 **add target blank** 属性，证明我们的 **attribute contains selector** 正如预期般工作。

---

## 常见问题与边缘情况

### 如果链接已经有 `rel` 属性怎么办？

我们的循环会将其覆盖为 `"noopener"`。如果需要保留已有值（例如 `"nofollow"`），请改为拼接：

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### 如何处理多个域名？

只需扩展选择器列表即可：

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### `prettify()` 会改变原始 HTML 结构吗？

它会重新缩进，但不会改变标签顺序或属性值。如果必须保持完全相同的原始空白，请如前所述用 `str(soup)` 替代 `prettify()`。

---

## 生产级脚本的专业提示

- **Backup before overwriting:** 添加复制步骤（`shutil.copy`）以保留原始文件。  
- **Logging instead of print:** 使用 `logging` 模块以适应可扩展项目。  
- **Batch processing:** 使用 `Path.rglob("*.html")` 循环遍历目录，一次性更新多个文件。  

这些改进将一个简单的 **open links new tab** 脚本转变为任何网站维护工作流的强大工具。

---

## 结论

现在，你拥有了一套可靠且可复用的方法，可在任意静态 HTML 集合中 **open links new tab**。通过利用 **attribute contains selector**，你可以在需要的地方 **change link target**，**add target blank**，并 **save modified html** 而不丢失格式。

在测试页面上试运行一下，然后再扩展到整个站点。需要为 PDF、其他域名等调整选择器吗？只需修改 CSS 字符串——其余保持不变。

如果遇到奇怪的问题，欢迎留言，或分享你在项目中扩展脚本的经验。祝编码愉快，愿所有锚点都在你期望的位置打开！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方式。

- [如何使用 Aspose.HTML for Java 编辑 HTML](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [如何向 Aspose.HTML for Java 的 HTML 文档添加 CSS – 内联 CSS](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}