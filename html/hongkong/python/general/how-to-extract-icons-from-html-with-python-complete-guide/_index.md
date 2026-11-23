---
category: general
date: 2026-07-02
description: 如何使用 Python 從 HTML 檔案中提取圖示。學習如何讀取 HTML 檔案、解析 HTML 文件，並提取 href 屬性以取得 favicon
  網址。
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: zh-hant
og_description: 如何使用 Python 從 HTML 頁面提取圖示。本教學將示範如何讀取 HTML 檔案、解析文件，並擷取 favicon URL。
og_title: 如何從 HTML 中提取圖示 – Python 指南
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: 如何使用 Python 從 HTML 中提取圖示 – 完整指南
url: /zh-hant/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 從 HTML 中提取圖示 – 完整指南

有沒有想過 **如何從網頁中提取圖示** 而不需要開啟瀏覽器？也許你正在建立網站目錄、SEO 稽核工具，或只是對在分頁中出現的微小 favicon 好奇。好消息是，你只需幾行 Python 代碼即可完成——不需要 Selenium、也不需要無頭 Chrome，只要一個純文字的 HTML 檔案。

在本教學中，我們將逐步說明如何使用 Python 讀取 HTML 檔案、解析 HTML 文件，最後 **擷取 `<link rel="icon">` 標籤的 href 屬性** 以取得這些 favicon 的 URL。完成後，你將擁有一段可重用的程式碼片段，能夠處理任何靜態 HTML，並且會學會如何應對相對路徑或多個圖示聲明等邊緣情況。

## 你將學會

- 使用 Python 載入本機 HTML 檔案 (read html file python)  
- 使用輕量級解析器安全地 **parse html document**  
- 定位聲明圖示的 `<link>` 元素  
- **Extract href attribute** 值並將其轉換為絕對 URL  
- 收集並列印所有發現的 **favicon URLs**  

不需要外部服務——只需標準函式庫以及流行的 **BeautifulSoup** 套件。

![顯示 Python 腳本提取圖示 – 如何提取圖示](https://example.com/images/extract-icons-python.png "如何提取圖示")

*圖片替代文字: "使用 Python 腳本提取圖示"*  

## 前置條件

- 已安裝 Python 3.8+  
- `beautifulsoup4` 套件 (`pip install beautifulsoup4`)  
- 你想要掃描的本機 HTML 檔案（例如 `sample.html`）  

如果你已經具備上述條件，我們直接開始吧。

## 步驟 1：讀取 HTML 檔案 Python – 載入文件

首先，我們需要開啟檔案並將其內容傳遞給解析器。使用 `with open(..., "r", encoding="utf‑8")` 可確保檔案自動關閉，且 UTF‑8 編碼能處理大多數現代網頁。

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**為什麼這很重要：** 使用正確的編碼開啟檔案可避免出現神祕的 `�` 字元，這些字元可能會在之後導致解析器失敗。使用標準函式庫的 `Path` 也能讓程式碼跨平台。

## 步驟 2：解析 HTML 文件 – 找出所有圖示連結

現在我們將原始 HTML 交給 **BeautifulSoup**，它會建立可導航的樹狀結構。我們會尋找所有 `rel` 屬性包含 `icon` 的 `<link>` 標籤。需注意 `rel` 可能是以空格分隔的清單（例如 `rel="shortcut icon"`），因此需要彈性的檢查。

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**為什麼此步驟關鍵：** 直接使用 `soup.find_all("link", rel="icon")` 會錯過 `rel="shortcut icon"` 或 `rel="apple-touch-icon"` 等變體。我們的輔助函式 `is_icon_link` 能涵蓋這些情況，使提取更穩健。

## 步驟 3：擷取 href 屬性 – 取得 URL

收集到相關標籤後，我們從每個標籤中擷取 `href` 屬性。有些頁面可能會遺漏 `href`（雖少見但有可能），因此我們會檢查 `None`。此外，favicon 通常以相對 URL 指定，我們會在知道頁面基礎 URL 時將其解析為絕對路徑。對於本機檔案，我們僅保留原始路徑。

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**為什麼要去除空白字元：** HTML 作者有時會不小心在 URL 前後加上空格，這會導致後續請求失敗。去除空白可確保取得乾淨的字串。

## 步驟 4：擷取 Favicon URL – 輸出結果

最後，我們列印（或回傳）發現的 URL 清單。在實務腳本中，你可能會將它們寫入 CSV、下載圖示，或傳遞給其他服務。以下是一個簡單的迴圈，會在主控台顯示結果。

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### 處理邊緣情況

- **多個 rel 值：** 我們的 `is_icon_link` 檢查已能捕捉 `rel="shortcut icon"` 與 `rel="apple-touch-icon"`。  
- **相對路徑：** 若之後需要絕對 URL，可使用 `urllib.parse.urljoin(base_url, href)`。  
- **缺少 href：** `if href:` 的檢查會跳過格式錯誤的標籤，避免 `NoneType` 錯誤。  
- **重複項目：** 你可以使用 `icon_urls = list(dict.fromkeys(icon_urls))` 來去除重複。

---

## 完整腳本 – 一站式解決方案

把所有步驟整合起來，以下是完整且可直接執行的程式。將其儲存為 `extract_icons.py`，並將 `html_path` 指向任意你想要的檔案。

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**預期輸出**（假設 `sample.html` 包含兩個圖示）：

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

使用 `python extract_icons.py` 執行，你將在主控台看到列印出的 URL。

## 常見問題

**Q: 如果 HTML 使用 `<meta>` 標籤來放置圖示，該怎麼辦？**  
A: 有些網站會透過 `<meta itemprop="image">` 內嵌圖示。可擴充 `is_icon_link`，同時檢查 `meta` 並具有 `itemprop="image"`，再擷取其 `content` 屬性。

**Q: 我可以自動下載圖示嗎？**  
A: 可以——只要將每個 URL 傳入 `requests.get(url, stream=True)` 並將內容寫入檔案。別忘了使用 `urljoin` 處理相對 URL。

**Q: 這能用於遠端網頁嗎？**  
A: 完全可以。將讀取檔案的步驟改為 `requests.get(page_url).text`，再把取得的 HTML 字串傳給 BeautifulSoup。只需留意 robots.txt 與速率限制。

## 總結

我們已說明如何使用 Python 從任何靜態 HTML 中 **提取圖示**，從讀取檔案到列印每個 favicon URL。核心概念——讀取檔案、解析文件、定位正確的標籤以及擷取 `href` 屬性——都是在許多網路爬蟲任務中可重用的模式。

接下來的步驟？試著擴充腳本：

- 將相對 URL 解析為頁面的基礎 URL  
- 下載每個圖示並儲存至本機  
- 支援其他圖示格式（如 Safari 的 `rel="mask-icon"`）  

歡迎自行實驗，若遇到問題，請在下方留言。祝爬蟲愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何在 Java 中查詢 HTML – 完整教學](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [如何在 Aspose.HTML for Java 中編輯 HTML 文件樹](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [在 Aspose.HTML for Java 中將 HTML 文件儲存為檔案](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}