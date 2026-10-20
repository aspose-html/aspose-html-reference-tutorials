---
category: general
date: 2026-05-31
description: 學習如何使用 Python 下載圖示。我們還會在同一個教學中說明如何擷取 favicon、使用 Python 讀取 HTML 文件，以及寫入二進位檔案。
draft: false
keywords:
- how to download icons
- how to extract favicon
- write binary file python
- read html document python
- load html python
language: zh-hant
og_description: 一步步教你使用 Python 下載圖示。學習提取網站圖示（favicon）、使用 Python 讀取 HTML 文件，以及寫入二進位檔案。
og_title: 使用 Python 下載圖示的完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to download icons using Python. We'll also cover how to extract
    favicon, read HTML document Python, and write binary file python in a single tutorial.
  headline: How to Download Icons with Python – Complete Guide
  type: TechArticle
tags:
- python
- web-scraping
- favicon
- file-io
title: 如何使用 Python 下載圖示 – 完整指南
url: /zh-hant/python/general/how-to-download-icons-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 下載圖示 – 完整指南

有沒有想過 **如何下載圖示** 從網站，而不必手動右鍵點擊每一個？你並不是唯一有此需求的人。無論你是在打造品牌審核工具，還是只想取得每個遇到的 favicon 的本地副本，掌握這項技巧都能為你節省時間與鍵擊次數。

在本教學中，我們將示範如何使用純粹的 Python 從 HTML 檔案 **下載圖示**。我們也會說明 **如何擷取 favicon**、展示 **read html document python**，以及解釋 **write binary file python**，讓你最終得到一個整齊的 .ico 檔案資料夾，可供任何專案使用。

---

## 需要的條件

- Python 3.8+（標準函式庫已足夠）
- 需要掃描的 HTML 頁面的本地副本（或可取得的 URL）
- 基本的 Python 檔案 I/O 知識
- 不需要外部套件，但若你偏好，可使用 `beautifulsoup4` 讓流程更順暢（可選）

都有了嗎？太好了——讓我們開始吧。

![How to download icons example](https://example.com/placeholder.png "how to download icons example")

---

## 步驟 1：在 Python 中載入 HTML 文件  

首先，我們需要以 **load html python** 方式載入 HTML——將檔案讀入記憶體，以便檢查其中的 `<link>` 標籤。最簡單的做法是使用內建的 `open` 函式以文字模式開啟檔案並讀取。

```python
# Step 1: Load the HTML document
HTML_PATH = "YOUR_DIRECTORY/sample.html"

# Using the built‑in open() to read the file as a string
with open(HTML_PATH, "r", encoding="utf-8") as f:
    html_content = f.read()
```

*為什麼需要這一步？*  
讀取 HTML 後會得到一個原始字串，供我們解析。如果跳過這一步直接使用路徑，解析器將沒有任何內容可供檢查。

---

## 步驟 2：解析文件並尋找圖示連結  

現在我們需要以 **read html document python** 方式進行解析。雖然可以使用正規表達式，但使用輕量的 HTML 解析器更可靠。Python 內建的 `html.parser` 可供我們繼承使用。

```python
from html.parser import HTMLParser

class IconLinkParser(HTMLParser):
    """Collects href attributes from <link rel='icon'> tags."""
    def __init__(self):
        super().__init__()
        self.icon_hrefs = []

    def handle_starttag(self, tag, attrs):
        if tag.lower() != "link":
            return
        attrs_dict = dict(attrs)
        # Look for rel="icon" (or rel="shortcut icon")
        rel = attrs_dict.get("rel", "").lower()
        if "icon" in rel:
            href = attrs_dict.get("href")
            if href:
                self.icon_hrefs.append(href)

# Instantiate and feed the HTML content
parser = IconLinkParser()
parser.feed(html_content)

# Now we have a list of all icon URLs
icon_hrefs = parser.icon_hrefs
print(f"Found {len(icon_hrefs)} icon link(s):", icon_hrefs)
```

**說明**  

- `handle_starttag` 會在每個開始標籤時觸發。  
- 我們篩選 `<link>` 元素，且其 `rel` 屬性包含 *icon* 這個字。這同時涵蓋 `rel="icon"` 與較舊的 `rel="shortcut icon"`。  
- `href` 的值會被存入 `icon_hrefs`，以備下一步使用。

---

## 步驟 3：解析相對路徑（可選但有幫助）

如果 HTML 使用相對 URL，我們必須將其轉換為絕對檔案系統路徑。這時 **load html python** 的知識會與 `urllib.parse` 結合。

```python
import os
from urllib.parse import urljoin

# Base directory where the HTML file lives
BASE_DIR = os.path.dirname(os.path.abspath(HTML_PATH))

def resolve_path(href):
    # If href already looks like an absolute path, return it unchanged
    if os.path.isabs(href):
        return href
    # Otherwise, join it with the base directory
    return os.path.normpath(os.path.join(BASE_DIR, href))

resolved_icon_paths = [resolve_path(h) for h in icon_hrefs]
print("Resolved paths:", resolved_icon_paths)
```

*為什麼要這麼做？*  
當你之後執行 **write binary file python** 時，需要一個真實的檔案路徑。像 `images/favicon.ico` 這樣的相對 URL 否則會導致 `FileNotFoundError`。

---

## 步驟 4：將每個圖示寫入本地二進位檔案  

這就是 **how to download icons** 的核心。我們會遍歷已解析的路徑，將每個圖示以二進位資料讀取，並寫入專屬的 `icons/` 資料夾中。

```python
import shutil

OUTPUT_DIR = "YOUR_DIRECTORY/icons"
os.makedirs(OUTPUT_DIR, exist_ok=True)

for index, icon_path in enumerate(resolved_icon_paths):
    # Guard against missing files
    if not os.path.isfile(icon_path):
        print(f"⚠️  Icon file not found: {icon_path}")
        continue

    # Destination filename: icon_0.ico, icon_1.ico, …
    dest_path = os.path.join(OUTPUT_DIR, f"icon_{index}.ico")

    # **write binary file python** – copy the binary data
    with open(icon_path, "rb") as src_file, open(dest_path, "wb") as dst_file:
        shutil.copyfileobj(src_file, dst_file)

    print(f"✅ Saved {dest_path}")
```

**發生了什麼？**  

- `os.makedirs(..., exist_ok=True)` 確保輸出資料夾已存在。  
- `shutil.copyfileobj` 會將位元組從來源串流至目的地，這是執行 **write binary file python** 最省記憶體的方式。  
- 我們將每個檔案命名為 `icon_<index>.ico`，以避免衝突。

**預期輸出**  

```
Found 2 icon link(s): ['images/favicon.ico', 'icons/custom.ico']
Resolved paths: ['/path/to/YOUR_DIRECTORY/images/favicon.ico',
                '/path/to/YOUR_DIRECTORY/icons/custom.ico']
✅ Saved YOUR_DIRECTORY/icons/icon_0.ico
✅ Saved YOUR_DIRECTORY/icons/icon_1.ico
```

腳本執行完畢後，你將擁有一個整潔的圖示檔案集合，可供任何後續任務使用。

---

## 步驟 5：額外 – 從遠端 URL 直接下載圖示  

如果你的 HTML 位於網路上而非本機磁碟，請將讀檔部分改為使用簡短的 `requests` 呼叫。這示範了如何從任何即時頁面 **how to extract favicon**。

```python
import requests

REMOTE_URL = "https://example.com"

# Grab the HTML
response = requests.get(REMOTE_URL)
response.raise_for_status()
html_content = response.text

# Re‑run the parser (same as before) to get icon URLs
parser = IconLinkParser()
parser.feed(html_content)
icon_hrefs = parser.icon_hrefs

# Download each icon via HTTP
for index, href in enumerate(icon_hrefs):
    # Resolve relative URLs against the page URL
    icon_url = urljoin(REMOTE_URL, href)
    r = requests.get(icon_url, stream=True)
    r.raise_for_status()
    dest_path = os.path.join(OUTPUT_DIR, f"remote_icon_{index}.ico")
    with open(dest_path, "wb") as out_file:
        shutil.copyfileobj(r.raw, out_file)
    print(f"✅ Downloaded {icon_url} → {dest_path}")
```

**為什麼要加入這段？**  
許多實務專案需要從即時網站擷取 favicon。這段程式碼顯示只需幾行額外程式，即可將相同的 **how to download icons** 邏輯延伸至網路。

---

## 常見陷阱與專業技巧

- **缺少 `rel="icon"`** – 有些網站透過 `<meta>` 標籤或 CSS 嵌入圖示。若需要這些，請擴充解析器以搜尋 `<meta name="msapplication‑TileImage">` 或 CSS 的 `background-image` URL。  
- **非 ICO 格式** – 現代的 favicon 常使用 `.png` 或 `.svg`。上述程式碼對任何二進位圖像皆適用；若在意保留原始格式，只需在 `dest_path` 中調整副檔名。  
- **權限錯誤** – 寫入檔案時，請確保腳本對目標資料夾具有寫入權限。使用 `os.makedirs(..., exist_ok=True)` 可避免「找不到目錄」的崩潰。  
- **大型 HTML 檔案** – 對於巨量頁面，建議逐行串流讀取檔案，而非一次載入整個字串至記憶體。內建的 `HTMLParser` 能處理增量的 feed。  

---

## 結論

你剛剛學會了如何使用純 Python 從 HTML 文件 **下載圖示**。透過 **reading html document python**、解析 `<link rel="icon">` 標籤、解析任何相對路徑，最後使用 **write binary file python** 將每個圖示儲存於本地，你現在擁有一支可重複使用的腳本，適用於本機與遠端頁面。

接下來的步驟？試著擴充解析器以捕捉 Apple touch icons（`rel="apple-touch-icon"`），或將此腳本整合至更大型的網路爬蟲管線，為數百個網域收集 favicon。此處涵蓋的基礎——HTML 解析、路徑解析與二進位檔案處理——是許多網路自動化任務的構件。

有任何問題或想分享有趣的使用案例嗎？歡迎在下方留言，祝你圖示收集愉快！

## 接下來你可以學什麼？

- [如何在 Aspose.HTML for Java 中編輯 HTML 文件樹](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [如何將 HTML 轉換為 PDF（Java） – 使用 Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [如何使用 Aspose.HTML for Java 將 HTML 轉換為 JPEG](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}