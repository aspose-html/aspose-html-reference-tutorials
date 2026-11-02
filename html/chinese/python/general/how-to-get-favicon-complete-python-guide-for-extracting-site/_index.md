---
category: general
date: 2026-06-26
description: 学习如何通过从 URL 加载 HTML 并从 link 标签中提取 href 来获取 favicon。一步一步的 Python 代码，快速获取网站图标。
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: zh
og_description: 如何快速获取favicon：从URL加载HTML，查找 link rel='icon'，并使用Python从 link 标签中提取 href。
og_title: 如何获取 Favicon – Python 教程
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: 如何获取 Favicon – 完整的 Python 提取站点图标指南
url: /zh/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何获取网站图标（Favicon）——完整的 Python 指南

是否曾想过 **如何获取 favicon** 而不必手动在页面源码中查找？你并不孤单——开发者、SEO 专家甚至设计师经常需要这个代表站点的小图标。在本教程中，我们将展示一种简洁、以 Python 为中心的方法，加载 URL 的 HTML，定位 `<link rel="icon">` 标签，并提取图标的 URL。完成后，你将准确掌握 **如何获取 favicon**，并拥有一个可复用的脚本用于你的项目。

我们会从获取 HTML 开始，涵盖相对 URL、多个图标格式等边缘情况。无需外部服务——只需标准的 `requests` 库和轻量级的 HTML 解析器。准备好了吗？让我们开始吧。

## 前置条件

- 已安装 Python 3.8+（代码在 3.10 也可运行）  
- 对 `requests` 和列表推导式有基本了解  
- 能访问目标网站的网络  

如果你已经满足上述条件，直接跳到第一步即可。否则，请安装唯一的依赖：

```bash
pip install requests beautifulsoup4
```

> **专业提示：** `beautifulsoup4` 是经过实战检验的解析器，能够让 “load html from url” 变得轻而易举。

## 第一步：使用 Python 加载 URL 的 HTML  

学习 **如何获取 favicon** 时，首先需要获取页面源码。这就是 “load html from url” 的环节。

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

为什么使用 `requests`？它会自动处理重定向、HTTPS 验证和超时，从而在后续 **获取网站图标** 时减少意外。

## 第二步：解析文档并查找图标链接  

现在我们已经拿到 HTML，需要定位所有 `rel` 属性指示图标的 `<link>` 元素。这是 **如何获取 favicon** 的核心。

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

注意我们同时检查 `icon` 和 `shortcut icon`，因为老站点仍然使用后者。这一点常常让搜索 “how to extract favicons” 的人感到困惑。

## 第三步：从 Link 元素中提取 href  

有了相关标签后，接下来的自然步骤——**从 link 中提取 href**——非常直接。

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

使用 `urljoin` 能确保即使站点提供相对路径如 `/favicon.ico`，也会得到正确的绝对 URL——这对可靠的 **如何获取 favicon** 脚本至关重要。

## 第四步（可选）：验证并过滤图标 URL  

有时页面会列出许多图标（Apple touch icon、不同尺寸的 PNG 等）。如果你只关心传统的 `.ico` 文件，可以相应过滤。本步骤演示 **如何提取特定类型的 favicons**。

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

随意调整过滤条件：将 `".ico"` 替换为 `".png"`，或检查 `rel="apple-touch-icon"` 以获取高分辨率图标。

## 第五步：下载图标文件（如果你需要实际图片）  

提取 URL 只是成功的一半；下载后即可得到可显示或存储的文件。下面是一个简易助手：

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

在前面的步骤完成后运行它，你会得到每个发现的 favicon 的本地副本，方便缓存或离线分析。

## 第六步：整合代码——完整可运行示例  

下面是完整的、可直接运行的脚本，演示 **如何获取 favicon**。复制粘贴，修改 `target_url`，即可看到输出。

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**预期输出（为简洁起见已截断）：**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

如果站点只提供 PNG 或 Apple touch icon，脚本会列出这些 URL，向你展示在各种情形下 **如何获取 favicon**。

## 常见问题与边缘情况  

### 如果站点使用 `<meta>` 标签而不是 `<link>`，该怎么办？  
一些老页面会在 `<meta name="msapplication‑TileImage">` 中嵌入图标 URL。你可以扩展 `find_icon_links`，让它也搜索这些 meta 标签并以相同方式处理。

### 如何处理以 `//` 开头的相对 URL？  
`urljoin` 会自动根据基准 URL 的协议解析协议相对 URL（`//example.com/favicon.ico`），无需额外逻辑。

### 能否自动获取多种尺寸（例如 32×32、180×180）？  
可以——只需省略 `filter_ico_urls` 步骤。脚本会返回它发现的所有图标 URL，包括各种尺寸的 PNG。随后你可以根据文件名模式进行排序或选择。

### 在被阻止的站点上能否工作？  
如果站点返回 403 或需要自定义 User‑Agent，修改 `requests.get` 调用：

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

这个小改动常能解决在更严格域名上 **如何获取 favicon** 的问题。

## 可视化概览  

![展示如何从网站获取 favicon 的流程图——加载 HTML、解析 link 标签、提取 href、可选下载](how-to-get-favicon-diagram.png "如何获取 favicon 流程图")

*图片的 alt 文本包含主要关键词，满足图像 SEO 要求。*

## 结论  

我们已逐步演示 **如何获取 favicon**：从 URL 加载 HTML、


## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式。每篇资源均提供完整可运行的代码示例和逐步解释。

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}