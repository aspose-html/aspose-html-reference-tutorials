---
category: general
date: 2026-06-10
description: 在 Python 中載入 HTML，從頁面提取 SVG 圖像——逐步程式碼、技巧與邊緣案例處理。
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: zh-hant
og_description: 在 Python 中載入 HTML 並提取 SVG 圖像，提供清晰可執行的範例。學習如何搜尋 HTML 中的 SVG 元素及處理邊緣情況。
og_title: 在 Python 中載入 HTML – 高效提取 SVG 圖像
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
title: 在 Python 中載入 HTML – 完整提取 SVG 圖像指南
url: /zh-hant/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中載入 HTML – 完整指南：提取 SVG 圖像

曾經需要 **load HTML in Python** 只為了從頁面中抓取所有 SVG 圖形嗎？你並不是唯一有此需求的人。無論你是在建立網路爬蟲、產生資產報告，或只是好奇網站使用了哪些圖示，了解如何 **extract SVG images** 都能為你省下大量手動搜尋的時間。

在本教學中，我們將逐步說明一個實用的端到端解決方案，該方案 **loads HTML in Python**，接著 **searches HTML SVG** 元素，**finds inline SVG**，甚至抓取 `<img>` 標籤所引用的外部 SVG 檔案。完成後，你將擁有可重複使用的腳本、一些處理棘手問題的技巧，以及對輸出結果的清晰概念。

## 你將學到的內容

* 一個可完整執行的 Python 腳本，可解析本機 HTML 檔案（或抓取的頁面），並列出它能找到的所有 SVG。  
* 了解 **inline SVG** (`<svg>…</svg>`) 與 **external SVG** (`<img src="… .svg">`) 之間的差異。  
* 處理 malformed markup、missing files 與 namespace quirks 的策略。  
* 擴充程式碼的想法——儲存 SVG、轉換為 PNG，或寫入資料庫。  

### 前置條件

* 已安裝 Python 3.8+。  
* 基本熟悉 Python 的 `requests` 與 `BeautifulSoup` 函式庫（我們會匯入它們，無需深入探討）。  
* 一個本機 HTML 檔案或你想要掃描的 URL。  

現在，讓我們開始吧。

## 在 Python 中載入 HTML – 設定解析器

第一步就是 **load HTML in Python**。你可以從磁碟讀取檔案，或抓取遠端頁面。以下是一個簡潔且穩健的輔助函式，兩者皆可使用：

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

> **為什麼這很重要：** 使用 `BeautifulSoup` 抽象掉原始字串解析的種種怪異，且此函式能優雅地處理本機檔案與遠端 URL。若網路請求失敗，它也會拋出例外——讓你立即得知問題所在。

## 提取 SVG 圖像 – 找尋 Inline SVG 元素

文件載入後，接下來的合乎邏輯的步驟是 **find inline SVG** 標籤。Inline SVG 直接嵌入於 HTML 標記中，意味著你可以直接從 DOM 抓取它。

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

*小技巧：* 若頁面使用 SVG 命名空間 (`<svg xmlns="http://www.w3.org/2000/svg">`)，`BeautifulSoup` 仍能找到該標籤，因為預設會忽略命名空間。當你僅在 **searching HTML SVG** 時，這相當方便。

## 搜尋 HTML SVG – 處理外部 `<img>` 參照

許多網站不直接嵌入 SVG，而是透過 `<img src="icon.svg">` 參照外部檔案。要捕捉這些，我們需要遍歷每個 `<img>` 標籤，檢查其 `src`，並判斷是否以 `.svg` 結尾。

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

> **邊緣案例提醒：** 有些頁面使用查詢字串 (`icon.svg?v=2`) 或片段 (`icon.svg#layer`)。`endswith(".svg")` 檢查仍然有效，因為我們只檢查字串的小寫尾部。若需要更嚴格的驗證，可考慮先使用 `urllib.parse` 去除參數。

## 找出 Inline SVG – 報告結果

現在我們有兩個清單——一個是 inline SVG 標記，另一個是外部檔案參照——我們可以將它們合併並報告總數。這與你先前貼出的原始程式碼片段相同，但加入了更多說明。

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## 整合所有步驟 – 完整腳本

以下是完整、可直接執行的程式。將其儲存為 `extract_svg.py`，並指向本機 HTML 檔案或 URL。

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

### 預期輸出

對 `sample.html` 範例執行此腳本可能會產生以下結果：

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

如果取消註解下載區塊，外部 SVG

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上進一步延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}