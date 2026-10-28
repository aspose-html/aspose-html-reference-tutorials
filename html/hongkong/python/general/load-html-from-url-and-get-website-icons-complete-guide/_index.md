---
category: general
date: 2026-06-10
description: 從 URL 載入 HTML，快速取得網站圖示。學習如何提取 favicon、獲取網站 favicon URL，並在 Python 中處理邊緣情況。
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: zh-hant
og_description: 從 URL 載入 HTML 以提取網站圖示並取得圖示 URL。一步一步的 Python 教學，適合開發者。
og_title: 從 URL 載入 HTML 並取得網站圖示 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML from URL to get website icons quickly. Learn how to extract
    favicons, fetch website favicon URLs, and handle edge cases in Python.
  headline: Load HTML from URL and Get Website Icons – Complete Guide
  type: TechArticle
tags:
- web scraping
- favicon extraction
- python
- html parsing
title: 從 URL 載入 HTML 並取得網站圖示 – 完整指南
url: /zh-hant/python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 URL 載入 HTML 並取得網站圖示 – 完整指南

有沒有曾經只為了抓取網站的小圖示而 **從 URL 載入 HTML**？你並不孤單。無論你是在打造書籤管理器、SEO 儀表板，或只是個人興趣專案，取得網站圖示都是一個小卻關鍵的環節。

在本教學中，我們將示範如何使用純 Python **抽取 favicon**——不需要笨重的 Selenium，也不需要瀏覽器魔法。完成後，你將能 **取得網站 favicon URL**、處理相對路徑，甚至在網站提供多個圖示時一次抓取。準備好了嗎？讓我們開始吧。

## 為什麼一開始就要從 URL 載入 HTML？

載入頁面的原始 HTML 可以直接取得瀏覽器用來定位 favicon 的 `<link>` 標籤。這些標籤通常長這樣：

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

只要抓到這段 markup，就能以程式方式讀取 `href` 屬性並自行下載圖像。這比擷取螢幕截圖更快，也適用於遵循標準慣例的任何網站。

## Step 1 – 從 URL 載入 HTML 文件

首先，我們需要一個方式取得頁面原始碼。Python 中最常用的選擇是 **requests** 套件，因為它簡單、可靠，且自動處理重新導向。

```python
import requests

def fetch_html(url: str) -> str:
    """
    Retrieve the raw HTML from the given URL.
    Raises an exception if the request fails.
    """
    response = requests.get(url, timeout=10)
    response.raise_for_status()          # Fail fast on HTTP errors
    return response.text
```

> **小技巧：** 若你在公司代理伺服器後工作，請在 `requests.get` 中傳入 `proxies=`。同時設定較短的 timeout 可以防止腳本在死站上卡住。

現在我們可以呼叫 `fetch_html("https://example.com")`，取得包含頁面 markup 的字串。這就是 **從 URL 載入 HTML** 的核心——後續流程皆以此字串為基礎。

## Step 2 – 取得網站圖示

取得 HTML 後，接下來要找出所有 `rel` 屬性包含「icon」的 `<link>` 元素。內建的 `html.parser` 模組可以完成這項工作，但 **BeautifulSoup** 讓程式碼更易讀。

```python
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def extract_icon_links(html: str, base_url: str) -> list[str]:
    """
    Parse the HTML and return a list of absolute URLs pointing to icons.
    Handles relative hrefs by joining them with the page’s base URL.
    """
    soup = BeautifulSoup(html, "html.parser")
    icons = []

    # Look for any <link> tag where rel contains "icon"
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            # Convert relative URLs to absolute ones
            absolute_url = urljoin(base_url, href)
            icons.append(absolute_url)

    return icons
```

留意我們使用 `urljoin` 把 `"/favicon.ico"` 轉成 `"https://example.com/favicon.ico"`——這是 **取得網站圖示** 時常見的邊緣案例。有些網站會為不同裝置提供不同圖示，因此最終可能會得到好幾個 URL。沒問題，我們只要把它們全部收集起來即可。

## Step 3 – 抽取 Favicon URL 並顯示

把上述步驟串起來非常直接。我們先抓取 HTML、執行抽取器，最後把結果列印出來。完整腳本如下：

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def extract_icon_links(html: str, base_url: str) -> list[str]:
    soup = BeautifulSoup(html, "html.parser")
    icons = []
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            icons.append(urljoin(base_url, href))
    return icons

def main():
    target = "https://example.com"
    html = fetch_html(target)
    icon_urls = extract_icon_links(html, target)
    print("Found icon URLs:", icon_urls)

if __name__ == "__main__":
    main()
```

### 預期輸出

對提供標準 favicon 的網站執行腳本，可能會得到：

```
Found icon URLs: ['https://example.com/favicon.ico']
```

如果網站提供多種圖示（Apple touch icon、shortcut icon 等），則會看到較長的列表：

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

這就是完整的 **抽取 favicon URL** 工作流程——簡潔、依賴少，隨時可以嵌入任何專案。

## Handling Common Pitfalls

| 問題 | 為何會發生 | 快速解決方案 |
|------|------------|--------------|
| **相對 `href` 且沒有 `<base>` 標籤** | `urljoin` 會以頁面 URL 作為基礎，對大多數情況都適用。 | 若存在 `<base href="...">` 標籤，先讀取它並將其作為 `base_url` 傳入。 |
| **缺少 `rel="icon"`** | 有些網站使用 `rel="shortcut icon"` 或自訂值。 | 擴充 lambda：`rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`。 |
| **重新導向至不同網域** | favicon 可能放在 CDN 上。 | `urljoin` 會正確解析新網域，因為它使用最終請求的 URL (`response.url`)。 |
| **連結失效（404）** | HTML 指向的檔案已不存在。 | 抽取 URL 後，可先用 HEAD 請求驗證每個連結是否有效。 |
| **多個 `<link>` 標籤指向相同圖示** | 重複條目會膨脹列表。 | 在回傳前使用 `set(icon_urls)` 去除重複。 |

## Going Further – 大量抓取網站 Favicon URL

如果需要為一系列網域 **抓取網站 favicon URL**，只要把 `main` 邏輯包在迴圈中即可：

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

此模式易於擴展，且可加入快取（例如使用 `functools.lru_cache`）以避免對同一網站頻繁請求。

## Visual Overview

![Load HTML from URL diagram](load-html-url.png)

*Alt text: 從 URL 載入 HTML 流程圖，顯示 fetch → parse → extract 步驟。*

上圖將三步驟流程濃縮為：**從 URL 載入 HTML**、**取得網站圖示**、以及 **抽取 favicon URL**。在向同事說明時非常實用。

## Conclusion

我們已完整示範如何使用 Python 的 requests 與 BeautifulSoup，打造一套 **從 URL 載入 HTML** 並 **取得網站圖示** 的生產級解決方案。透過抽取 `<link rel="icon">` 標籤的 `href` 屬性，你可以 **抽取 favicon URL**、處理相對路徑，甚至取得多種圖示格式——全部只需數十行程式碼。

接下來可以嘗試將圖示下載至本機資料夾、產生 domain‑to‑favicon 映射的 CSV，或將此邏輯嵌入 Flask API，隨時提供圖示服務。**抓取網站 favicon URL** 的可能性無窮，而核心技巧始終如一。

有關邊緣案例的問題，或想分享巧妙的調整嗎？歡迎在下方留言——祝你抓圖順利！

## What Should You Learn Next?

以下教學與本指南緊密相關，能進一步深化所學技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，助你掌握更多 API 功能，並在自己的專案中探索不同實作方式。

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Load HTML Documents from Stream with Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Handle Document Load Events in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}