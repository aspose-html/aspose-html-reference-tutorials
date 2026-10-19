---
category: general
date: 2026-06-10
description: 在 Python 中加载 HTML，以从页面中提取 SVG 图像——逐步代码、技巧以及边缘情况处理。
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: zh
og_description: 在 Python 中加载 HTML 并提取 SVG 图像，提供清晰可运行的示例。学习如何搜索 HTML 中的 SVG 元素并处理边缘情况。
og_title: 在 Python 中加载 HTML – 高效提取 SVG 图像
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: 在 Python 中加载 HTML – 提取 SVG 图像的完整指南
url: /zh/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中加载 HTML – 提取 SVG 图像的完整指南

是否曾经需要 **在 Python 中加载 HTML** 只为从页面中提取所有 SVG 图形？你并不是唯一有此需求的人。无论你是在构建网页爬虫、生成资产报告，还是仅仅对站点使用的图标感到好奇，了解如何 **提取 SVG 图像** 都能为你省去大量手动搜索的时间。

在本教程中，我们将逐步演示一个实用的端到端解决方案：**在 Python 中加载 HTML**，随后 **搜索 HTML SVG** 元素，**查找内联 SVG**，甚至获取 `<img>` 标签引用的外部 SVG 文件。完成后，你将拥有一个可复用的脚本、一系列处理棘手问题的技巧，以及对输出结果的清晰认识。

## 你将收获什么

* 一个可直接运行的 Python 脚本，能够解析本地 HTML 文件（或抓取的页面），列出所有能找到的 SVG。  
* 对 **内联 SVG**（`<svg>…</svg>`）和 **外部 SVG**（`<img src="… .svg">`）之间区别的理解。  
* 处理标记错误、文件缺失以及命名空间怪癖的策略。  
* 扩展代码的思路——保存 SVG、转换为 PNG，或将其写入数据库。

### 前置条件

* 已安装 Python 3.8+。  
* 对 Python 的 `requests` 和 `BeautifulSoup` 库有基本了解（我们会导入它们，无需深入）。  
* 一个本地 HTML 文件或你想要扫描的 URL。  

现在，开始吧。

## 在 Python 中加载 HTML – 设置解析器

第一步就是 **在 Python 中加载 HTML**。你可以从磁盘读取文件，也可以抓取远程页面。下面是一个既简洁又稳健的辅助函数，兼顾两种情况：

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **为什么重要：** 使用 `BeautifulSoup` 可以屏蔽原始字符串解析的各种怪癖，该函数还能优雅地处理本地文件和远程 URL。如果网络请求失败，它会抛出异常——这样你能立刻知道哪里出问题了。

## 提取 SVG 图像 – 查找内联 SVG 元素

文档加载完毕后，接下来要 **查找内联 SVG** 标签。内联 SVG 直接嵌入 HTML 标记中，这意味着你可以直接从 DOM 中获取它们。

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*小技巧：* 如果页面使用了 SVG 命名空间（`<svg xmlns="http://www.w3.org/2000/svg">`），`BeautifulSoup` 仍然能够找到该标签，因为默认会忽略命名空间。这在你仅仅 **搜索 HTML SVG** 时非常方便。

## 搜索 HTML SVG – 处理外部 `<img>` 引用

许多站点并不直接嵌入 SVG，而是通过 `<img src="icon.svg">` 引用外部文件。要捕获这些文件，需要遍历所有 `<img>` 标签，检查其 `src` 是否以 `.svg` 结尾。

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **边缘情况提示：** 有些页面会使用查询字符串（`icon.svg?v=2`）或片段标识（`icon.svg#layer`）。`endswith(".svg")` 检查仍然有效，因为我们只检查字符串的低位后缀。如果需要更严格的校验，可以先使用 `urllib.parse` 去除参数再进行判断。

## 查找内联 SVG – 报告结果

现在我们拥有两份列表——一份是内联 SVG 标记，另一份是外部文件引用。我们可以将它们合并并统计总数。这与您最初提供的代码片段功能相同，只是加入了更多上下文说明。

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## 综合示例 – 完整脚本

下面是完整的、可直接运行的程序。将其保存为 `extract_svg.py`，然后指向本地 HTML 文件或 URL 即可。

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### 预期输出

对示例 `sample.html` 运行脚本可能得到如下输出：

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

如果取消注释下载块，外部 SVG 将会被下载到本地。

## 接下来该学习什么？

以下教程与本指南紧密相关，进一步扩展了本章节展示的技术。每篇资源都提供完整可运行的代码示例，并配有逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [svg to png java – 使用 Aspose.HTML for Java 将 SVG 转换为图像](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}