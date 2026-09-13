---
category: general
date: 2026-09-13
description: 学习如何解析HTML并加载HTML文档，同时限制深度以防止在Python中出现无限递归。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- load html document
- how to limit depth
- prevent infinite recursion
language: zh
lastmod: 2026-09-13
og_description: 如何安全地解析 HTML 并加载 HTML 文档。本指南展示了如何限制深度并防止无限递归。
og_image_alt: Diagram showing HTML parsing flow with depth‑limit control
og_title: 如何在深度限制下解析HTML – Python教程
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to parse HTML and load HTML document while limiting depth
    to prevent infinite recursion in Python.
  headline: How to parse HTML with depth limiting using Python
  type: TechArticle
- description: Learn how to parse HTML and load HTML document while limiting depth
    to prevent infinite recursion in Python.
  name: How to parse HTML with depth limiting using Python
  steps:
  - name: Create resource handling options
    text: The `ResourceHandlingOptions` object tells the parser when to stop following
      nested resources such as `<iframe>` tags or linked CSS files.
  - name: Load HTML document with the configured options
    text: Now you load the file while supplying the options you just defined. This
      is the **load html document** step that respects the depth limit.
  - name: Parse the document safely
    text: With the document loaded, you can now traverse the DOM. The example below
      extracts all headings (`<h1>`‑`<h3>`) without exceeding the depth limit.
  type: HowTo
tags:
- html parsing
- python
- recursion
- resource handling
title: 如何使用 Python 对 HTML 进行深度限制解析
url: /zh/python/general/how-to-parse-html-with-depth-limiting-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 限制深度解析 HTML

如果你需要 **如何解析 HTML** 来自大型报告，第一步是使用安全网加载 HTML 文档，以阻止深层嵌套。本文教程展示了如何加载 HTML 文档、设置最大处理深度，以及 **防止无限递归** 当资源相互引用时。

你将看到一个完整、可运行的示例，使用 `ResourceHandlingOptions` 和 `HTMLDocument`。阅读完本指南后，你可以安全地解析任何 HTML 文件，而不会耗尽内存或导致栈溢出。

## 前置条件

在开始之前，请确保你已具备：

* 已安装 Python 3.9 或更高版本。
* 提供 `ResourceHandlingOptions` 和 `HTMLDocument` 的 HTML 处理库。（本教程假设该库名为 `htmlhandler`；使用 `pip install htmlhandler` 安装。）
* 对递归和 HTML 结构有基本了解。

无需额外的系统配置。

## 如何使用深度限制解析 HTML

解决方案的核心是创建 `ResourceHandlingOptions` 实例，配置其 `max_handling_depth`，并将其传递给 `HTMLDocument`。以下步骤将带你完成整个过程。

### 步骤 1：创建资源处理选项

`ResourceHandlingOptions` 对象告诉解析器何时停止跟随嵌套资源，例如 `<iframe>` 标签或链接的 CSS 文件。

```python
# Step 1: Create resource handling options
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after 3 levels of nested resources
```

*为什么这很重要*：如果没有深度限制，恶意或格式错误的文档可能会嵌入相互引用的资源，导致无限循环。将 `max_handling_depth` 设置为 3 可确保解析器在三层后停止，这对大多数合法文档足够，同时保护运行时安全。

### 步骤 2：使用配置好的选项加载 HTML 文档

现在在加载文件时提供刚才定义的选项。这是 **加载 HTML 文档** 步骤，能够遵守深度限制。

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument(
    "YOUR_DIRECTORY/big_report.html",
    resource_handling_options=resource_options
)
```

*为什么这很重要*：将 `resource_handling_options` 传递给 `HTMLDocument` 可将深度限制直接集成到解析引擎中。解析器将在达到限制后自动停止遍历，从而 **防止无限递归**。

### 步骤 3：安全地解析文档

文档加载完成后，你可以遍历 DOM。下面的示例提取所有标题（`<h1>`‑`<h3>`），且不会超出深度限制。

```python
def extract_headings(node, current_depth=0):
    """
    Recursively collect heading text while respecting the max handling depth.
    """
    if current_depth > resource_options.max_handling_depth:
        return []  # Prevent infinite recursion by aborting deeper calls

    headings = []
    if node.tag_name in ("h1", "h2", "h3"):
        headings.append(node.text_content.strip())

    for child in node.children:
        headings.extend(extract_headings(child, current_depth + 1))
    return headings

# Start traversal from the root element
all_headings = extract_headings(html_doc.root)
print("Collected headings:", all_headings)
```

**预期输出（示例）**：

```
Collected headings: ['Executive Summary', 'Methodology', 'Results', 'Conclusion']
```

判断 `if current_depth > resource_options.max_handling_depth` 的 guard 是 **如何限制深度** 的机制，能够阻止进一步的递归。此模式适用于任何树形结构数据，而不仅限于 HTML。

## 如何使用自定义选项加载 HTML 文档

如果需要为特定文件调整深度，只需在创建 `HTMLDocument` 前更改 `max_handling_depth`。

```python
resource_options.max_handling_depth = 5   # Allow deeper nesting for this file
html_doc = HTMLDocument("another_report.html", resource_handling_options=resource_options)
```

在你知道文档包含合法的深层嵌套（例如嵌套表格）时，修改限制非常有用。相同的代码仍然 **防止无限递归**，因为限制在运行时被强制执行。

## 常见陷阱及避免方法

| 陷阱 | 产生原因 | 解决方案 |
|---------|----------------|-----|
| **缺少 `resource_handling_options`** | 解析器会跟随每个资源，导致递归无界。 | 在构造 `HTMLDocument` 时始终传入 `ResourceHandlingOptions` 实例。 |
| **`max_handling_depth` 设置过低** | 解析器过早停止，重要内容可能被跳过。 | 使用具有代表性的样本进行测试，选择兼顾安全与完整性的深度。 |
| **递归函数未进行深度检查** | 即使解析器停止，自定义遍历仍可能无限递归。 | 在每个递归辅助函数中加入相同的深度检查逻辑（`if current_depth > max_depth: return`）。 |
| **假设所有节点都有 `children`** | 文本节点可能没有 `children` 属性，导致属性错误。 | 使用 `hasattr(node, "children")` 进行判断，或使用 try/except 块。 |

解决这些问题可确保你的 **如何解析 HTML** 方案在各种输入下保持稳健。

## 完整、可运行的示例

下面是完整脚本，可复制粘贴到名为 `parse_report.py` 的文件中。它演示了从创建选项到提取标题的完整工作流。

```python
# parse_report.py
from htmlhandler import ResourceHandlingOptions, HTMLDocument

def main():
    # ---- Step 1: configure depth limit ----
    resource_options = ResourceHandlingOptions()
    resource_options.max_handling_depth = 3   # adjust as needed

    # ---- Step 2: load the HTML document ----
    html_path = "YOUR_DIRECTORY/big_report.html"
    html_doc = HTMLDocument(html_path, resource_handling_options=resource_options)

    # ---- Step 3: recursive extraction with safety guard ----
    def extract_headings(node, current_depth=0):
        if current_depth > resource_options.max_handling_depth:
            return []  # stop deeper recursion

        headings = []
        if node.tag_name in ("h1", "h2", "h3"):
            headings.append(node.text_content.strip())

        # Safely iterate over children if they exist
        if hasattr(node, "children"):
            for child in node.children:
                headings.extend(extract_headings(child, current_depth + 1))
        return headings

    # Run extraction starting from the document root
    headings = extract_headings(html_doc.root)
    print("Collected headings:", headings)

if __name__ == "__main__":
    main()
```

运行脚本：

```bash
python parse_report.py
```

你应该会在控制台看到标题列表，确认解析器遵守了深度限制并 **防止了无限递归**。

## 后续步骤

* **解析其他元素** – 将 `extract_headings` 改造为收集表格、链接或图片。
* **流式处理大文件** – 当处理多 GB 报告时，使用增量解析 (`HTMLDocument.stream`)。
* **与 asyncio 集成** – 如需非阻塞 I/O，可将加载步骤包装在 async 函数中。

深入这些主题可帮助你 **加载 HTML 文档** 对象时高效且完全掌控递归深度。

---

通过本指南，你现在了解了 **如何解析 HTML** 的安全方法，掌握了使用自定义深度限制 **加载 HTML 文档** 的技巧，并能够在任何递归遍历中 **防止无限递归**。将此模式应用到自己的项目中，并根据源文件的复杂度调整深度设置。祝编码愉快！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步提升。每个资源都提供完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [How to Parse HTML Java – Load, Query & Count Elements](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)
- [how to query html in Java – load HTML, CSS selector, and extract headings](/html/english/java/css-html-form-editing/how-to-query-html-in-java-load-html-css-selector-and-extract/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}