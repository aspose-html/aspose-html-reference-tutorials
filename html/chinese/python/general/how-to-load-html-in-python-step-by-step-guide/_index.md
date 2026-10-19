---
category: general
date: 2026-07-02
description: 学习如何在 Python 中加载 HTML，按 ID 获取元素，并从文件中提取文本。本实用教程展示了使用 BeautifulSoup 读取
  HTML 文件。
draft: false
keywords:
- how to load html
- how to get element
- how to extract text
- get element by id
- read html file python
language: zh
og_description: 如何在 Python 中加载 HTML 并使用 BeautifulSoup 提取文本。按照指南读取 HTML 文件，按 id 获取元素并打印其内容。
og_title: 如何在 Python 中加载 HTML – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  headline: How to Load HTML in Python – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  name: How to Load HTML in Python – Step‑by‑Step Guide
  steps:
  - name: What if the HTML is malformed?
    text: BeautifulSoup’s `lxml` parser is forgiving, but for severely broken markup
      you might want to fallback to the built‑in `html.parser`. Swap `"lxml"` with
      `"html.parser"` in the `BeautifulSoup` constructor.
  - name: How to handle multiple elements with the same ID?
    text: HTML spec says IDs should be unique, but reality sometimes disagrees. Use
      `soup.find_all(id="duplicate-id")` to retrieve a list, then iterate over it.
  - name: Need to read from a URL instead of a file?
    text: Replace the file‑reading logic with `requests.get(url).text`. Remember to
      install the `requests` package (`pip install requests`) and handle network errors
      gracefully.
  - name: Want to extract other attributes (e.g., `class` or `href`)?
    text: 'Simply access them like a dictionary: `header[''class'']` or `header[''href'']`.
      If the attribute might be missing, use `.get(''class'')` to avoid `KeyError`.'
  type: HowTo
tags:
- Python
- HTML parsing
- BeautifulSoup
title: 如何在 Python 中加载 HTML – 步骤指南
url: /zh/python/general/how-to-load-html-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中加载 HTML – 完整教程

是否曾经想过在 Python 脚本中 **如何加载 HTML** 而不抓狂？你并不是唯一的。无论是爬取新闻网站、处理本地报告，还是仅仅需要从电子邮件模板中提取标题，掌握加载 HTML 的技巧都是每个开发者必备的技能。

在本指南中，我们将逐步演示 **如何通过 ID 获取元素**、**如何提取文本**，以及最终打印结果——全部保持代码简洁且符合 Pythonic 风格。我们还会覆盖 **在 Python 中读取 HTML 文件** 的细节，让你可以立即复制粘贴一个可运行的解决方案。

> **专业提示：** 示例使用流行的 *BeautifulSoup* 库，因为它轻量、文档完善，并且能够处理简单和复杂的 HTML 结构。

## 您需要的环境

在开始之前，请确保您已经拥有：

- Python 3.9 或更高版本（代码在 3.10+ 也可运行）
- 已安装 `beautifulsoup4` 和 `lxml`（`pip install beautifulsoup4 lxml`）
- 一个示例 HTML 文件——我们将其命名为 `sample.html` 并放置在名为 `YOUR_DIRECTORY` 的文件夹中

就这些。无需笨重的浏览器，也不需要 Selenium，仅用纯 Python 即可。

## 第一步：如何加载 HTML – 将文件读取到内存

首先要做的就是 **读取 HTML 文件** 并将其加载到内存中。这是后续所有步骤的基础，请务必做好。

```python
from pathlib import Path

# Define the path to the HTML file
html_path = Path("YOUR_DIRECTORY/sample.html")

# Read the file contents as a string
html_content = html_path.read_text(encoding="utf-8")
```

*为什么这很重要：* 使用 `Path.read_text` 可以抽象掉操作系统特定的换行符，并自动处理 UTF‑8 编码——这已成为现代网页的事实标准。如果文件缺失，`Path.read_text` 会抛出明确的 `FileNotFoundError`，让调试变得轻而易举。

## 第二步：解析 HTML 文档

现在我们已经拥有原始字符串，需要将 **HTML 加载** 到解析器对象中。BeautifulSoup 为我们提供了便捷的 API 来遍历 DOM。

```python
from bs4 import BeautifulSoup

# Create a BeautifulSoup object using the lxml parser (fast and reliable)
soup = BeautifulSoup(html_content, "lxml")
```

*为什么选择 lxml？* `lxml` 解析器比 Python 内置的解析器快得多，并且对错误标记的容错更好——非常适合实际爬取时遇到的各种 HTML。

## 第三步：通过 ID 获取元素 – 定位标题

文档解析完毕后，让我们回答 **如何通过 ID 获取元素** 的问题。在本例中，我们要查找 `<h1>` 标签，其 `id` 属性等于 `"main-header"`。

```python
# Retrieve the element with the specific ID
header = soup.find(id="main-header")
```

如果未找到该元素，`header` 将为 `None`。最好做好防护：

```python
if header is None:
    raise ValueError("Element with id='main-header' not found in the HTML file.")
```

## 第四步：如何提取文本 – 获取内部内容

有了元素后，提取其文本内容轻而易举。这正是 **如何提取文本** 的答案。

```python
# Extract the visible text inside the element
header_text = header.get_text(strip=True)  # strip removes surrounding whitespace
```

`get_text` 会自动拼接所有嵌套的文本节点，无需手动遍历子节点。`strip=True` 参数会去除换行符和空格，返回干净的字符串。

## 第五步：打印结果 – 验证一切正常

最后，将值输出到控制台。这相当于原代码片段中的 `print(header.text_content)` 行。

```python
print(header_text)  # prints: The text inside <h1 id="main-header">
```

如果运行脚本后看到预期的标题，恭喜你——你已经成功 **在 Python 中读取 HTML 文件**、通过 ID 定位元素并提取了其文本。

## 完整可运行示例

下面是完整的、可直接运行的脚本。复制到名为 `extract_header.py` 的文件中，然后执行 `python extract_header.py`。

```python
# extract_header.py
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(file_path: str) -> str:
    """Read an HTML file and return its contents as a string."""
    path = Path(file_path)
    if not path.is_file():
        raise FileNotFoundError(f"Unable to locate the file: {file_path}")
    return path.read_text(encoding="utf-8")

def get_element_by_id(soup: BeautifulSoup, element_id: str):
    """Return the first tag with the given id, or raise an informative error."""
    element = soup.find(id=element_id)
    if element is None:
        raise ValueError(f"Element with id='{element_id}' not found.")
    return element

def main():
    # Step 1: Load the HTML document
    html = load_html("YOUR_DIRECTORY/sample.html")
    
    # Step 2: Parse the HTML with BeautifulSoup
    soup = BeautifulSoup(html, "lxml")
    
    # Step 3: Retrieve the element by its ID
    header = get_element_by_id(soup, "main-header")
    
    # Step 4: Extract and print the text content
    print(header.get_text(strip=True))

if __name__ == "__main__":
    main()
```

**预期输出**（假设 `sample.html` 包含 `<h1 id="main-header">Welcome to My Site</h1>`）：

```
Welcome to My Site
```

就是这么简单——一个脚本，除 BeautifulSoup 和 lxml 外无需其他依赖。

## 常见问题与边缘情况

### 如果 HTML 损坏怎么办？

BeautifulSoup 的 `lxml` 解析器容错性强，但对于严重损坏的标记，您可以回退到内置的 `html.parser`。只需在 `BeautifulSoup` 构造函数中将 `"lxml"` 替换为 `"html.parser"`。

### 如何处理多个相同 ID 的元素？

HTML 规范要求 ID 唯一，但实际情况有时并非如此。使用 `soup.find_all(id="duplicate-id")` 可获取一个列表，然后遍历它。

### 需要从 URL 而不是文件读取？

将文件读取逻辑替换为 `requests.get(url).text`。记得安装 `requests` 包（`pip install requests`），并妥善处理网络错误。

### 想提取其他属性（例如 `class` 或 `href`）？

直接像字典一样访问：`header['class']` 或 `header['href']`。如果属性可能不存在，使用 `.get('class')` 可避免 `KeyError`。

## 可视化摘要

![如何加载 html 示例](https://example.com/placeholder-image.png "如何加载 html 示例")

*Alt text:* 如何加载 html 示例 – 展示从文件读取到文本提取的流程图。

## 小结

我们已经介绍了 **如何在 Python 中加载 HTML**，演示了 **如何通过 ID 获取元素**，并展示了 **如何从该元素提取文本**。按照上述步骤，你可以可靠地 **在 Python 中读取 HTML 文件**、操作 DOM，并精准提取所需内容。

## 接下来可以做什么？

- **探索 CSS 选择器：** 使用 `soup.select_one('.my-class')` 进行更灵活的查询。
- **批量爬取多个页面：** 将此模式与 `requests` 以及循环结合，实现站点批处理。
- **写回 HTML：** BeautifulSoup 也支持修改树结构并保存——对模板任务非常实用。
- **性能调优：** 对于超大文件，可考虑使用 `lxml.etree.iterparse` 等流式解析器。

尽情实验吧——更换 ID、尝试不同标签，甚至在处理 XHTML 时切换到 `xml.etree.ElementTree`。概念保持不变，而你已经拥有了进行任何 HTML 解析冒险的坚实基础。

祝编码愉快！如果遇到问题或有酷炫的使用案例想分享，欢迎在下方留言。

## 接下来应该学习什么？

以下教程与本指南紧密相关，基于本篇示例的技术进一步展开。每篇资源都提供完整可运行的代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}