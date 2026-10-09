---
category: general
date: 2026-10-09
description: 学习如何使用 Python 创建 HTML，如何添加 body，以及如何插入段落。一步一步的代码展示了如何设置文本以及如何追加子元素。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to create html
- how to add body
- how to insert paragraph
- how to set text
- how to append child
language: zh
lastmod: 2026-10-09
og_description: 如何使用 Python 创建 HTML。请跟随本教程学习如何添加 body、插入段落、设置文本以及追加子元素。
og_image_alt: Diagram illustrating how to create HTML using Python’s xml.dom.minidom
og_title: 如何以编程方式创建HTML——一步步指南
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn how to create HTML, how to add body, and how to insert paragraph
    using Python. Step‑by‑step code shows how to set text and how to append child
    elements.
  headline: How to create HTML programmatically – a complete guide
  type: TechArticle
tags:
- HTML generation
- Python
- DOM manipulation
title: 如何以编程方式创建HTML——完整指南
url: /zh/python/general/how-to-create-html-programmatically-a-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何以编程方式创建 HTML – 完整指南

如果你需要 **how to create html** 从零开始，本教程将为你展示完整过程。你还将学习 **how to add body**、**how to insert paragraph**、**how to set text**，以及使用 Python 标准库 **how to append child** 元素的方式。阅读完本指南后，你将拥有一个完整的 HTML 文档，能够保存到磁盘或嵌入到网页响应中。

以编程方式创建 HTML 可以避免手动输入错误，并且可以根据数据生成动态标记。以下步骤适用于 Python 3.11 或更高版本，且不需要任何第三方库，因此可以在任何支持标准库的环境中运行。

## 前置条件

- 已安装 Python 3.11+
- 对 Python 函数和对象有基本了解
- 用于运行脚本的编辑器或 IDE（如 VS Code、PyCharm，或普通终端）

无需外部库，因为本方案使用 `xml.dom.minidom`，它是 Python 内置的 `xml` 包的一部分。

## 如何使用 Python 的 xml.dom.minidom 创建 HTML

第一步是导入 DOM 实现并创建一个新的文档对象。该文档将作为后续所有节点的容器。

```python
"""Create a minimal HTML document using xml.dom.minidom."""
from xml.dom.minidom import Document

def build_html():
    # Step 1: Create a new HTML document
    doc = Document()
    # The document itself does not contain any elements yet.
    return doc
```

*为什么重要：* `Document()` 为你提供一个符合 W3C DOM 规范的干净起点，使得 **how to create html** 结构能够保持良好格式并可序列化。

## 如何向文档添加 body

在创建了 `<html>` 根元素后，需要一个 `<body>` 元素来放置可见内容。本步骤演示 **how to add body** 的正确做法。

```python
def add_body(doc: Document):
    # Step 2: Create the <html> root element and attach it to the document
    html_elem = doc.createElement('html')
    doc.appendChild(html_elem)

    # Step 2 continued: Add a <body> element to the document
    body_elem = doc.createElement('body')
    html_elem.appendChild(body_elem)   # This is how to append child elements
    return body_elem
```

*为什么重要：* `<body>` 标签是任何可见标记的必需部分。使用 `appendChild` 可以遵循 DOM 的 **how to append child** 模式，确保层级结构得到保留。

## 如何在 body 中插入段落

有了 `<body>` 后，你现在可以演示 **how to insert paragraph** 元素。段落是最常见的块级文本容器。

```python
def insert_paragraph(body_elem):
    # Step 3: Create a <p> element
    p_elem = body_elem.ownerDocument.createElement('p')
    body_elem.appendChild(p_elem)   # This shows how to append child again
    return p_elem
```

*为什么重要：* 插入 `<p>` 标签为文本提供了语义化的容器。使用 `ownerDocument` 能保证新元素属于同一文档，这对构建有效的 DOM 树至关重要。

## 如何为段落设置文本

现在已经拥有 `<p>` 元素，需要在其中放入实际内容。本代码片段解释了 **how to set text** 的实现方式。

```python
def set_paragraph_text(p_elem, text):
    # Step 4: Create a text node and attach it to the paragraph
    text_node = p_elem.ownerDocument.createTextNode(text)
    p_elem.appendChild(text_node)   # This is another example of how to append child
```

*为什么重要：* 文本节点是唯一可以在元素内部存放原始字符的方式。使用 `createTextNode` 符合标准的 **how to set text** 方法，避免编码问题。

## 正确追加子元素的完整示例（全流程）

将上述各部分组合起来，即可得到完整的 **how to create html**、**how to add body**、**how to insert paragraph**、**how to set text** 与 **how to append child** 工作流的可运行脚本。

```python
from xml.dom.minidom import Document

def build_html():
    # Create the document
    doc = Document()

    # Add <html> and <body>
    html_elem = doc.createElement('html')
    doc.appendChild(html_elem)

    body_elem = doc.createElement('body')
    html_elem.appendChild(body_elem)   # how to append child

    # Insert a paragraph
    p_elem = doc.createElement('p')
    body_elem.appendChild(p_elem)      # how to insert paragraph and how to append child

    # Set paragraph text
    text_node = doc.createTextNode('Hello, Aspose!')
    p_elem.appendChild(text_node)      # how to set text and how to append child

    return doc

if __name__ == '__main__':
    # Build the HTML document
    document = build_html()

    # Serialize to a pretty‑printed string
    html_string = document.toprettyxml(indent='  ', encoding='UTF-8')
    # Write to a file for inspection
    with open('output.html', 'wb') as f:
        f.write(html_string)

    print('HTML file "output.html" created successfully.')
```

**预期输出（`output.html`）：**

```html
<?xml version="1.0" encoding="UTF-8"?>
<html>
  <body>
    <p>Hello, Aspose!</p>
  </body>
</html>
```

*为什么重要：* 该脚本在同一位置演示了所有必需操作。你可以将其作为独立文件运行，生成的 `output.html` 可在任意浏览器中打开，以验证段落是否如预期显示。

## 常见变体与边缘情况

- **添加多个段落：** 多次调用 `insert_paragraph` 并将每个新 `<p>` 传递给 `set_paragraph_text`。记得 **how to append child** 每个新节点到 `<body>`。
- **设置属性（如 class 或 id）：** 在追加子节点之前使用 `element.setAttribute('class', 'my-class')`。这不会影响 **how to set text** 流程，但会丰富标记。
- **生成 UTF‑8 字符：** `toprettyxml` 已经以 UTF‑8 输出。确保源字符串是 Unicode 字面量（在旧版 Python 中需加 `u` 前缀），以避免编码错误。
- **避免空文本节点：** 如果创建 `<p>` 后未调用 **how to set text**，浏览器可能渲染出空行。请始终附加文本节点，或在元素保持空白时将其移除。

## 专业技巧

- **复用文档对象：** 为每个小片段创建新的 `Document` 代价较高。生成大型页面时，保持单一文档实例可提升效率。
- **验证输出：** 使用 `xml.dom.minidom.parseString` 对生成的字符串进行解析，可提前捕获不合法的标记。
- **性能提示：** 对于非常大的 HTML 文件，考虑使用 `xml.sax` 流式输出，而不是一次性在内存中构建完整 DOM。

## 结论

现在你已经掌握了使用 Python 内置 DOM API **how to create html**、**how to add body**、**how to insert paragraph**、**how to set text** 与 **how to append child** 元素的清晰、可复用模式。完整示例可直接复制、修改，并集成到 Web 框架、邮件生成器或静态站点流水线中。

接下来，探索相关主题，如 **how to add head elements**、**how to embed CSS**，以及 **how to generate tables with DOM**。这些内容都基于本指南展示的相同原理，帮助你自信地扩展此基础。

祝编码愉快！


## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，每个资源都提供完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能，并在自己的项目中尝试不同实现方式。

- [How to Create HTML and Add CSS Style Element – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/how-to-create-html-and-add-css-style-element-step-by-step-gu/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Append Child in Java DOM – Complete Aspose.HTML Guide](/html/english/java/editing-html-documents/how-to-append-child-in-java-dom-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}