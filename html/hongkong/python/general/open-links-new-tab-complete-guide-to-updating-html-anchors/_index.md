---
category: general
date: 2026-07-05
description: 使用 Python 在新分頁開啟連結 – 學習如何加入 target='_blank'、變更連結目標、使用屬性包含選擇器，並輕鬆儲存修改後的
  HTML。
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: zh-hant
og_description: 快速在新分頁開啟連結。本教學示範如何加入 target="_blank"、變更連結目標，並使用 Python 儲存修改後的 HTML。
og_title: 在新分頁開啟連結 – 逐步 HTML 更新指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: 在新分頁開啟連結 – HTML 錨點更新完整指南
url: /zh-hant/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在新分頁開啟連結 – 更新 HTML 錨點的完整指南

是否曾經需要在靜態 HTML 頁面上 **open links new tab**，卻不知從何下手？你並不孤單。許多開發者在清理舊有網站或加入無障礙調整時，都會遇到這個問題。在本教學中，我們將示範一個實用的解決方案，能 **adds target blank**、**changes link target**，並安全地 **saves modified html**——只需幾行 Python 程式碼。

我們還會說明如何使用 **attribute contains selector**，只對真正需要的錨點進行操作（例如，所有指向 *example.com* 的連結）。完成後，你將擁有一個可重複使用的腳本，無論專案大小，都能直接套用。

## 你將學會

- 將 HTML 檔案載入可操作的文件物件。  
- 選取 `href` 屬性包含特定子字串的 `<a>` 元素。  
- **Add target blank** 並設定 `rel="noopener"` 屬性以提升安全性。  
- **Save modified html** 回寫至磁碟且不失去格式。  

除了標準函式庫與 **beautifulsoup4**（只需小小安裝）之外，無需其他外部相依套件。如果你已在使用其他解析器，概念同樣適用。

---

## 前置條件

- 在機器上安裝 Python 3.8+。  
- 具備 HTML 與 Python 的基本知識。  
- `beautifulsoup4` 套件（`pip install beautifulsoup4`）。  

就這樣——不需要任何重量級框架。

---

## 步驟 1：載入 HTML 文件

首先，我們需要讀取來源檔案並交給 BeautifulSoup。把它想像成打開一張空白畫布，讓你可以在上面繪製新屬性。

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **為何重要：** 使用 `Path` 使程式碼跨作業系統，且 `html.parser` 為內建解析器，簡單任務不需額外解析器。

---

## 步驟 2：使用 Attribute Contains Selector 找到目標連結

我們只想處理指向 *example.com* 的錨點。CSS 選擇器 `a[href*='example.com']` 正好符合需求——`*=` 表示「包含」。BeautifulSoup 的 `select` 方法支援此語法。

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **小技巧：** 若需不分大小寫的比對，可改用小迴圈檢查 `if 'example.com' in a.get('href', '').lower()`。

現在 `anchor_elements` 包含了所有我們關心的連結，準備進行下一步轉換。

---

## 步驟 3：變更連結目標 – 加入 Target Blank 並加強安全性

在新分頁開啟連結只需要設定 `target="_blank"`。然而，現代瀏覽器建議同時加入 `rel="noopener"`（或 `noreferrer`），以防新開的頁面透過 `window.opener` 存取原始視窗。這個小小的安全調整可防止釣魚攻擊。

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **為何使用直接字典賦值：** 若屬性不存在會自動建立，若已存在則覆寫——非常適合 **change link target** 的操作。

---

## 步驟 4：將修改後的 HTML 儲存回磁碟

最後一步是將更新後的標記寫入新檔案。保留原始檔不變，可在發生問題時回復。

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **`prettify()` 的作用：** 它會將 HTML 以良好的縮排格式化，使儲存的檔案更易閱讀與比對。若想保留原始空白，請將 `prettify()` 改為 `str(soup)`。

---

## 完整腳本 – 一鍵解決方案

以下是完整、可直接執行的腳本。將其儲存為 `update_links.py`，然後在終端機執行 `python update_links.py`。

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### 預期結果

假設 `links.html` 原始內容為：

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

執行腳本後，`links-updated.html` 會變成：

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

只有指向 *example.com* 的連結被加入了 **add target blank** 屬性，證明我們的 **attribute contains selector** 正確運作。

---

## 常見問題與邊緣情況

### 如果連結已經有 `rel` 屬性呢？

我們的迴圈會將其覆寫為 `"noopener"`。若需保留原有值（例如 `"nofollow"`），可改為串接：

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### 如何處理多個網域？

只要擴充選擇器清單即可：

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### `prettify()` 會改變原始 HTML 結構嗎？

它會重新縮排，但不會改變標籤順序或屬性值。若必須保留完全相同的原始空白，請如前所述將 `prettify()` 改為 `str(soup)`。

---

## 生產環境腳本的專業提示

- **備份再覆寫：** 加入複製步驟（`shutil.copy`）以保護原始檔案。  
- **使用日誌取代 print：** 在可擴充的專案中使用 `logging` 模組。  
- **批次處理：** 使用 `Path.rglob("*.html")` 迴圈遍歷目錄，一次更新多個檔案。  

這些調整可將簡單的 **open links new tab** 腳本轉變為任何網站維護工作流程的強大工具。

---

## 結論

現在你已擁有一套穩固、可重複使用的方式，能在任何靜態 HTML 集合中 **open links new tab**。透過 **attribute contains selector**，你可以在需要的地方 **change link target**，**add target blank**，並 **save modified html** 而不失去格式。

先在測試頁面試跑一次，再擴展至整個網站。若需為 PDF、其他檔案或不同網域調整選擇器，只要修改 CSS 字串——其他部分保持不變。

如果遇到怪異情況，歡迎留下評論，或分享你如何在自己的專案中擴充此腳本。祝編程愉快，願所有錨點都能如你所願開啟！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在所示技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何使用 Aspose.HTML for Java 編輯 HTML](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [如何在 Aspose.HTML for Java 中加入 CSS – 內嵌 CSS 到 HTML 文件](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}