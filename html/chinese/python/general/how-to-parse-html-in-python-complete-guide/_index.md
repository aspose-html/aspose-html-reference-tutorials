---
category: general
date: 2026-05-28
description: 如何快速在 Python 中解析 HTML——加载 HTML 文件，使用 CSS 选择器，并通过 XPath contains 示例提取
  href 属性。
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: zh
og_description: 如何在 Python 中解析 HTML：学习加载 HTML 文件、使用 CSS 选择器，并通过 XPath contains 示例获取
  href 属性。
og_title: 如何在 Python 中解析 HTML – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: 如何在 Python 中解析 HTML – 完整指南
url: /zh/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中解析 HTML – 完整指南

有没有想过 **如何在 Python 脚本中解析 HTML**，而不需要引入笨重的浏览器？你并不孤单。我们大多数人只需要 **加载 HTML 文件**，抓取几个标题，或许再提取一两个下载链接。在本教程中，我将向你展示如何使用一个小型库、CSS 选择器以及 XPath contains 示例来 **获取 href 属性** 值。

我们将一步步演示完整流程，从读取本地 HTML 文档到打印你关心的数据。没有废话，只有一个实用、可直接运行的示例，今天就可以把它放进你的项目中使用。

## 你将学到

- 如何使用轻量级解析器 **加载 HTML 文件**。
- 如何使用 **CSS 选择器** 语法获取如文章标题之类的元素。
- 如何编写 **XPath contains 示例** 来过滤链接。
- 如何安全地 **获取 href 属性** 值。
- 处理错误标记以及扩展脚本的技巧。

你只需要 Python 3.8+ 和 `lxml`、`cssselect` 两个包——均可通过一条 `pip` 命令安装。

---

## 第一步：加载 HTML 文件

在做任何操作之前，你需要把 HTML 内容读取到内存中。`lxml.html` 模块提供了便利的 `fromstring` 辅助函数，但当你有磁盘上的文件时，`parse` 函数更为简洁。

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **为什么这很重要：** 只加载一次文件可以保持内存占用低，并为你提供一个支持 CSS 选择器和 XPath 查询的单一 `root` 对象。如果文件缺失或不可读，`html.parse` 会抛出明确的 `OSError`，你可以在后面捕获它。

### 小技巧
如果你处理的是字符串而不是文件，请将 `html.parse` 换成 `html.fromstring(your_html_string)`。

---

## 第二步：使用 CSS 选择器获取标题

CSS 选择器简洁且对任何写过样式表的人都很熟悉。我们来抓取每个 `<article>` 中的 `<h2>`——这正好适合作为新闻标题。

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**预期输出**（假设示例 HTML 包含两个文章）：

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **为什么选 CSS？** 它易读、快速，并且 `lxml` 开箱即用。`cssselect` 方法在内部将选择器转换为 XPath 表达式，让你兼得两者优势。

---

## 第三步：XPath Contains 示例 – 查找 “download” 链接

有时你需要比 CSS 更细粒度的控制。XPath 的 `contains()` 函数在匹配属性内部子字符串时非常有用，例如所有指向下载的链接。

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**示例输出**：

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **为什么使用 XPath contains？** 它让你直接在属性值上过滤，而无需额外的 Python 循环。这就是教程中常见的 **xpath contains 示例**，但这里结合了真实场景。

---

## 第四步：封装为可复用函数

硬编码路径和打印语句适合快速测试，但生产代码更倾向于函数。下面是一个紧凑的助手函数，返回标题和下载链接。

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

现在你可以调用该函数并美化输出结果：

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

运行脚本会得到与之前相同的输出，但现在它已经被整齐地封装，便于复用。

---

## 第五步：处理边缘情况和常见陷阱

1. **缺失 `href` 属性** – 即使 `<a>` 节点没有 `href`，XPath 仍会返回该节点。需要对 `None` 做防护：

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **相对 URL 与绝对 URL** – 如果链接是相对路径，你可能需要相对于基准 URL 进行解析：

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **标记错误的 HTML** – `lxml` 容错性强，但极度破损的标记仍可能导致 `html.parse` 抛出 `XMLSyntaxError`。请将解析调用包装在 `try/except` 中，以记录并跳过有问题的文件。

4. **大文件的性能** – 对于多兆字节的页面，考虑使用 `iterparse` 流式解析，而不是一次性加载整个 DOM。

---

## 可视化概览（可选）

![如何解析 HTML 的流程图，展示加载文件 → CSS 选择器 → XPath contains → 获取 href 属性](how-to-parse-html-flow.png "如何解析 HTML 的流程图")

*Alt 文本包含主要关键词以满足 SEO。*

---

## 结论

我们已经完整演示了 **如何在 Python 中解析 HTML**：从加载 HTML 文件、使用 CSS 选择器提取文章标题、构造 XPath contains 示例定位下载链接，到安全 **获取 href 属性** 值。可复用的 `parse_news_html` 函数展示了一种简洁、可维护的方式，能够适配任何爬取任务。

准备好迎接下一个挑战了吗？尝试将脚本扩展为：

- 使用 `//table//tr` XPath 查询解析表格。
- 使用另一个 **xpath contains 示例** 提取图片 `src` 属性。
- 使用 `aiohttp` 实现对实时网页的异步抓取。

祝你爬取愉快，记住——掌握了这些基础后，HTML 抓取就轻而易举。如果遇到任何问题，欢迎在下方留言——我们一起排查解决！

## 相关教程

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}