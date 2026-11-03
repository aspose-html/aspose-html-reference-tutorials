---
category: general
date: 2026-05-31
description: 學習如何使用 Python 從 HTML 中提取 SVG。這個一步一步的教學示範如何讀取 HTML 文件、儲存 SVG 檔案以及有效率地儲存內嵌
  SVG。
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: zh-hant
og_description: 如何使用 Python 從 HTML 中提取 SVG。跟隨本教程閱讀 HTML 文件、保存 SVG 檔案，並輕鬆處理內嵌 SVG。
og_title: 如何使用 Python 從 HTML 中提取 SVG – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: 使用 Python 從 HTML 中提取 SVG 完全指南
url: /zh-hant/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 從 HTML 中擷取 SVG – 完整指南

有沒有想過 **如何從雜亂的 HTML 頁面中擷取 SVG**，卻不想抓狂？你並不孤單。無論你是在打造網路爬蟲、設計工作流程，或只是需要批次匯出圖示，掌握 **如何擷取 SVG** 都是一個能省時省力的好技巧。

在本教學中，我們將示範 **如何使用 Aspose.HTML for Python** 來擷取 SVG。我們會讀取 HTML 文件，抽取內嵌的 `<svg>` 標記 **以及** 外部 SVG 參考，然後 **將 SVG 檔案** 儲存到磁碟——全程使用一段整潔、可重複使用的腳本。完成後，你將擁有一個即時可執行的解決方案，能依需求套用到自己的專案。

> **小技巧：** 若你只想快速檢視頁面內容，`BeautifulSoup` 也能搞定，但 Aspose.HTML 提供完整的 DOM，讓內嵌與外部 SVG 的擷取變得輕而易舉。

## 需要的環境

在開始之前，請確保你已具備：

* Python 3.8+（程式碼使用 f‑string，最低 3.6 以上）
* `pip install aspose-html` – 提供 HTML 解析功能的商業函式庫
* 一個包含 `input.html` 的資料夾，裡面有你想抽出的 SVG
* 對輸出目錄的寫入權限（本文稱為 `YOUR_DIRECTORY`）

就這樣——不需要額外的二進位檔案，也不需要無頭瀏覽器。簡單吧？

## 步驟 1：使用 Aspose.HTML 讀取 HTML 文件

首先必須 **讀取 HTML 文件**，才能遍歷其 DOM 樹。Aspose.HTML 會提供一個 `HTMLDocument` 物件，行為類似瀏覽器的 `document`。

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*為什麼這很重要：* 透過將 HTML 載入正式的 DOM，你可以避免正則表達式解析的陷阱，且自動取得 `get_elements_by_tag_name`、`query_selector_all` 等便利方法。

## 步驟 2：收集所有內嵌的 <svg> 元素

內嵌 SVG 指的是直接寫在 HTML 中的 `<svg>…</svg>` 區塊。要 **儲存內嵌 SVG**，只需要取得它們的 outer HTML 即可。

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

請注意，我們直接把原始標記加入 `svg_contents`。之後會判斷每筆資料是標記本身還是檔案路徑。

## 步驟 3：找出外部 SVG 參考（img 與 object 標籤）

許多頁面會透過 `<img src="icon.svg">` 或 `<object data="logo.svg">` 連結外部 SVG。要 **從 HTML 中擷取 SVG**，也必須捕捉這些 URL。

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*邊緣案例提醒：* 若 SVG URL 為相對路徑，記得與 HTML 檔案的基礎路徑合併。此處為簡化起見，假設 HTML 與 SVG 同目錄。

## 步驟 4：將每個 SVG 寫入獨立檔案

現在我們手上有混合了標記字串與檔案路徑的清單，接著會逐一 **儲存 SVG 檔案**。腳本會自動辨識是內嵌標記還是外部檔案參考。

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**執行結果會是：** 程式結束後，`YOUR_DIRECTORY` 內會出現 `svg_0.svg`、`svg_1.svg` … 等檔案，每個檔案都保存了原始的內嵌標記或外部 SVG 的副本。

### 預期輸出

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

如果參考的檔案遺失，腳本會印出警告但繼續執行——不會因單一斷裂連結而中止整個擷取流程。

## 常見問題處理

| 問題 | 為何會發生 | 快速解決方案 |
|------|------------|--------------|
| **相對 URL 失效** | `src` 可能是 `"../assets/icon.svg"` | 使用 `os.path.join(os.path.dirname(html_path), src)` 來解析。 |
| **檔名重複** | 兩個 SVG 同名會被覆寫 | 在檔名加入內容雜湊 (`hashlib.md5(content.encode()).hexdigest()[:8]`)。 |
| **大型內嵌 SVG 造成記憶體激增** | 事先把所有標記存入清單 | 改為逐筆直接寫入檔案，避免緩衝。 |
| **非 SVG 圖片誤抓** | 某些 `<img>` 以 `.svg?version=1` 結尾 | 在檢查副檔名前先去除查詢字串 (`src.split('?')[0]`)。 |

## 完整腳本（可直接複製貼上）

以下是完整、即時可執行的程式。存為 `extract_svg.py`，自行調整 `YOUR_DIRECTORY` 後，執行 `python extract_svg.py`。

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## 重點回顧 – 如何快速擷取 SVG

* 使用 `HTMLDocument` **讀取 HTML 文件**。
* 透過 `get_elements_by_tag_name` **收集內嵌 `<svg>`**。
* 用 CSS selector 抓取外部 SVG（以 `.svg` 結尾的 `img`、`object`）。
* **儲存每個片段**——直接寫入標記或複製參考檔案。
* 處理相對路徑、檔名衝突、缺失檔案等邊緣情況。

以上即是 **如何從 HTML 頁面中擷取 SVG** 的完整答案，全部封裝在一支易於修改的腳本裡。

## 接下來可以做什麼？

既然已能 **可靠地擷取 SVG**，不妨嘗試以下延伸想法：

* **批次處理：** 迴圈遍歷整個 HTML 資料夾，建立圖示庫。
* **最佳化：** 使用 SVGO（Node.js 優化工具）壓縮每個 SVG 檔案。
* **格式轉換：** 用 `cairosvg` 或 `svglib` 把 SVG 轉成 PNG，支援舊版瀏覽器。
* **中繼資料抽取：** 解析每個 SVG 內的 `<title>`、`<desc>`，作為可搜尋的標籤。

上述主題皆與次要關鍵字——**read HTML document**、**save svg files**、**save inline svg**、**extract svg from html**——息息相關，值得深入探索。

---

*祝開發順利！若遇到任何問題，歡迎在下方留言或於 GitHub 私訊我。SVG 的世界雖大，但有了正確的工具，擷取它們真的輕而易舉。*


## 接下來該學什麼？

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendre un document SVG au format PNG dans .NET avec Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}