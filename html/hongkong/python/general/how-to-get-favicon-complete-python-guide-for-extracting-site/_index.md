---
category: general
date: 2026-06-26
description: 學習如何透過從 URL 載入 HTML 並從 link 標籤中提取 href 來取得 favicon。一步一步的 Python 程式碼，快速取得網站圖示。
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: zh-hant
og_description: 如何快速取得網站圖示：從 URL 載入 HTML，尋找 link rel='icon'，並使用 Python 從 link 標籤中提取
  href。
og_title: 如何取得網站圖示 – Python 教學
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
title: 如何取得 Favicon – 完整的 Python 網站圖示提取指南
url: /zh-hant/python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何取得 Favicon – 完整的 Python 網站圖示擷取指南

有沒有想過 **how to get favicon** 從任何網站，而不必手動挖掘頁面原始碼？你並不是唯一有此需求的人——開發者、SEO 專家，甚至設計師常常需要代表網站的那個小圖示。在本教學中，我們將示範一種乾淨、以 Python 為中心的方式，從 URL 載入 HTML，定位 `<link rel="icon">` 標籤，並抽取圖示 URL。完成後，你將能精確掌握 **how to get favicon** 於任何網域，並擁有可重複使用的腳本供專案使用。

我們將涵蓋從取得 HTML 到處理相對 URL 及多種圖示格式等邊緣案例的全部步驟。無需外部服務——只需要標準的 `requests` 套件與輕量級的 HTML 解析器。準備好了嗎？讓我們開始吧。

## 前置條件

- 已安裝 Python 3.8+（程式碼在 3.10 亦可執行）  
- 具備 `requests` 與 list comprehensions 的基本概念  
- 能連上目標網站的網際網路  

如果你已具備上述條件，太好了——直接跳到第一步。否則，請安裝唯一需要的相依套件：

```bash
pip install requests beautifulsoup4
```

> **Pro tip:** `beautifulsoup4` 是經過實戰驗證的解析器，讓「load html from url」變得輕而易舉。

## 步驟 1：使用 Python 從 URL 載入 HTML  

學習 **how to get favicon** 時，你需要先取得頁面的原始碼。這就是「load html from url」的步驟。

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

為什麼使用 `requests`？它會自動處理重新導向、HTTPS 驗證與逾時，讓你在稍後嘗試 **get website icons** 時不會遇到太多意外。

## 步驟 2：解析文件並尋找圖示連結  

現在我們已取得 HTML，需要找出所有 `rel` 屬性指示圖示的 `<link>` 元素。這是 **how to get favicon** 的核心。

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

請注意我們同時檢查 `icon` 與 `shortcut icon`，因為較舊的網站仍會使用後者。這個細微差異常常讓人在搜尋「how to extract favicons」時卡關。

## 步驟 3：從連結元素抽取 href  

取得相關標籤後，下一個合乎邏輯的步驟——**extract href from link**——相當直接。

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

使用 `urljoin` 可確保即使網站提供相對路徑（例如 `/favicon.ico`），最終也會得到正確的絕對 URL，這對於可靠的 **how to get favicon** 腳本至關重要。

## 步驟 4：可選 – 驗證與過濾圖示 URL  

有時頁面會列出許多圖示（Apple touch icon、不同尺寸的 PNG 等）。如果你只在意傳統的 `.ico` 檔案，可依此過濾。此步驟示範 **how to extract favicons** 某一特定類型的方式。

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

隨意調整過濾條件：將 `".ico"` 改成 `".png"`，或檢查 `rel="apple-touch-icon"` 以取得高解析度圖示。

## 步驟 5：下載圖示檔案（如果你想要實際的圖像）  

抽取 URL 只完成了一半；下載後即可取得可顯示或儲存的檔案。以下是一個快速的輔助函式：

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

在前面的步驟之後執行此程式，即可在本機取得每個發現的 favicon，十分適合快取或離線分析。

## 步驟 6：整合全部 – 完整可執行範例  

以下是完整、可直接執行的腳本，示範 **how to get favicon** 從任意網站。複製貼上、修改 `target_url`，即可看到輸出。

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

**預期輸出（為簡潔起見已截斷）：**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

如果網站僅提供 PNG 或 Apple touch icon，腳本會列出那些 URL，讓你清楚看到在各種情況下 **how to get favicon** 的結果。

## 常見問題與邊緣案例  

### 如果網站使用 `<meta>` 標籤而非 `<link>` 該怎麼辦？

某些較舊的頁面會將圖示 URL 嵌入 `<meta name="msapplication‑TileImage">`。你可以擴充 `find_icon_links`，同時搜尋這類 meta 標籤，並以相同方式處理。

### 如何處理以 `//` 開頭的相對 URL？

`urljoin` 會自動根據基礎 URL 的協定解析協定相對 URL（`//example.com/favicon.ico`），因此不需要額外的邏輯。

### 我能自動取得多種尺寸（例如 32×32、180×180）嗎？

可以——只要省略 `filter_ico_urls` 步驟。腳本會回傳它發現的所有圖示 URL，包括不同尺寸的 PNG。之後你可以依檔名模式自行排序或挑選。

### 這在會阻擋機器人的網站上能運作嗎？

如果網站回傳 403 或需要自訂 User‑Agent，只要調整 `requests.get` 呼叫即可：

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

這個小變更常能解決在較嚴格的網域上「how to get favicon」的問題。

## 視覺概覽  

![展示如何從網站取得 favicon 流程的圖示 – 載入 HTML、解析 link 標籤、抽取 href、可選下載](how-to-get-favicon-diagram.png "how to get favicon 流程圖")

*圖片的 alt 文字包含主要關鍵字，符合圖像 SEO 的需求。*

## 結論  

我們已一步步說明 **how to get favicon**：從 URL 載入 HTML、解析 `<link>` 標籤、抽取 href，並可選擇下載圖示檔案，最終得到可靠的圖示取得流程。

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題，讓你在此基礎上進一步精進。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 C# 中儲存 HTML – 使用自訂資源處理程式的完整指南](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [如何使用 Aspose.HTML for Java 編輯 HTML](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [如何將 HTML 轉換為 PDF（Java） – 使用 Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}