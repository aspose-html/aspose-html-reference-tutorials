---
category: general
date: 2026-10-21
description: 学习如何在 Python 中解析 HTML，加载 HTML 文档，使用 CSS 选择器，并快速提取 HTML 中的超链接。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: zh
lastmod: 2026-10-21
og_description: 如何使用 CSS 选择器在 Python 中解析 HTML。加载 HTML 文档，选择链接，并使用简洁代码从 HTML 中提取超链接。
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: 如何在 Python 中解析 HTML – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: 如何在 Python 中使用 CSS 选择器解析 HTML
url: /zh/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 CSS 选择器解析 HTML

如果你需要在 Python 脚本中 **how to parse html**，本指南将为你展示具体方法。你将学习如何加载 HTML 文档、如何使用选择器语法查找元素，以及如何在不编写自定义解析器的情况下从 html 中提取超链接。

解析 HTML 是网页爬虫、数据分析流水线或自动化测试的常见任务。完成本教程后，你将拥有一个可复用的函数，能够加载 HTML 文档、使用 CSS 选择器选取所有 `<a>` 标签，并返回一个干净的 URL 列表。

## 你需要的环境

- Python 3.8+（代码在任何近期版本均可运行）  
- **lxml** 库（`pip install lxml`）——提供快速的 HTML 解析和 CSS 选择器支持  
- 你想要分析的 HTML 文件（例如 `sample.html`）  

无需额外工具；所有操作均使用标准库和一个第三方包即可完成。

## 步骤 1：如何解析 HTML – 加载文档

第一步是将文件读取到内存中。使用 **lxml.html** 可以得到一个支持 CSS 选择器的树对象。

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**为什么这很重要：**  
`load_html` 抽象了文件读取的样板代码，并确保文档使用容错的 HTML 解析器进行解析。这是 **load html document python** 的最安全方式，无需担心标记不完整。

## 步骤 2：如何使用选择器 – 查找所有链接元素

文档加载后，你可以使用 CSS 选择器定位每个 `<a>` 标签。选择器 `"a"` 匹配所有锚点元素，但你也可以细化（例如 `"a.external"` 或 `"nav a"`）。

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**为什么这很重要：**  
**how to use selector** 方法让你能够在单个可读的字符串中表达复杂查询，避免手动遍历树结构。它适用于 `lxml.cssselect` 支持的任何 CSS 模式。

## 步骤 3：从 HTML 中提取超链接并处理它们

现在你已经拥有 `<a>` 元素的列表，可以从每个元素中提取 `href` 属性。下面的辅助函数还会在提供基准 URL 时对相对 URL 进行标准化。

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**预期输出**（假设 `sample.html` 包含三个链接）：

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**为什么这很重要：**  
`extract_hyperlinks` 是 **extract hyperlinks from html** 的核心。它能够优雅地处理缺失的 `href` 属性，解析相对链接，并返回一个普通的 Python 列表，供后续处理（如 requests、pandas 或数据库）使用。

## 完整的端到端示例

将这三个函数组合在一起，即可得到一个脚本：加载文件、选取所有锚点并打印每个超链接。

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

运行 `python parse_links.py` 会在控制台打印出每个已完整解析的超链接。此脚本演示了 **how to parse html**、**how to use selector** 和 **extract hyperlinks from html** 的完整、可复用流程。

## 常见变体和边缘情况处理

| 情况 | 需要更改的内容 | 原因 |
|-----------|----------------|--------|
| **仅需要绝对 URL** | 在 `extract_hyperlinks` 中省略 `base_url` 参数 | 保持相对 URL 不变 |
| **你还需要链接文本** | 让 `extract_hyperlinks` 返回元组 `(href, link.text_content())` | 方便同时存储 URL 和锚文本 |
| **大型 HTML 文件** | 使用带 CSS 选择器过滤的 `lxml.etree.iterparse` | 通过流式处理降低内存使用 |
| **不同的选择器** | 将 `"a"` 替换为 `"nav a[href]"` 或 `"div.content a.external"` | 针对链接子集，在复杂页面中使用 **how to use selector** 时很有用 |

**专业提示：** 在发起网络请求前务必验证提取的 URL。快速的 `urlparse` 检查可以过滤掉格式错误的字符串，保护爬虫免于崩溃。

## 结论

你现在已经掌握了 **how to parse html** 的方法，了解了 **load html document python**，会使用 **how to use selector** 定位元素，并能高效地 **extract hyperlinks from html**。上面的完整示例可以直接复制到你的项目中，并可根据分页、JavaScript 生成内容或多页爬取等更高级的使用场景进行改造。

接下来你可以探索的步骤包括：

- 使用 **requests‑html** 或 **Playwright** 获取需要 JavaScript 执行的页面。  
- 将提取的 URL 存储在 CSV 或 SQLite 数据库中以便后续分析。  
- 为网络超时和 HTTP 状态码添加错误处理。

祝你解析愉快，欢迎尝试不同的选择器，充分发挥 Python 中基于 CSS 的 HTML 查询的强大功能！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步提升。每篇资源都提供完整可运行的代码示例和逐步解释，助你掌握更多 API 功能并在项目中探索替代实现方案。

- [如何在 Python 中配置 HTML 资源处理并加载 HTML 文档](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [如何在 Python 中解析 HTML – 完整指南](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [如何在 Python 中加载 HTML – 步骤指南](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}