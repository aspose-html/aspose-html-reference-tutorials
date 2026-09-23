---
category: general
date: 2026-09-23
description: 使用 Python 更改 HTML 檔案中的元素文字。學習如何載入 HTML 檔案、編輯 title 標籤，並有效地更新 HTML 標題。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change element text
- how to change title
- edit title tag
- load html file
- update html title
language: zh-hant
lastmod: 2026-09-23
og_description: 使用 Python 更改 HTML 文件中的元素文字。本教學示範如何載入 HTML 檔案、編輯 title 標籤，並僅用幾行程式碼更新
  HTML 標題。
og_image_alt: Screenshot showing change element text in HTML using Python code
og_title: 使用 Python 更改 HTML 中的元素文字 – 快速指南
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  headline: Change element text in HTML with Python – step‑by‑step guide
  type: TechArticle
- description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  name: Change element text in HTML with Python – step‑by‑step guide
  steps:
  - name: 'Edge case: Multiple `<title>` tags'
    text: 'HTML standards allow only one `<title>` element, but malformed files sometimes
      contain more. If you need to handle that situation, iterate over all matches:'
  - name: Editing other elements (e.g., `<h1>`)
    text: 'If you need to **change element text** for a heading instead of the title,
      adjust the XPath:'
  - name: Preserving existing whitespace
    text: 'When the original HTML uses indentation inside tags, `pretty_print` may
      reformat it. To keep the original formatting, omit `pretty_print`:'
  - name: Working with Unicode characters
    text: '`lxml` handles Unicode automatically. Ensure the source file is saved with
      UTF‑8 encoding; otherwise, specify the correct encoding when opening the file.'
  type: HowTo
tags:
- Python
- HTML manipulation
- Web scraping
title: 使用 Python 更改 HTML 元素文字 – 步驟教學
url: /zh-hant/python/general/change-element-text-in-html-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 更改 HTML 中元素文字 – 步驟指南

如果你需要在 HTML 文件中**更改元素文字**，本指南會精確說明如何使用 Python 完成。無論是要修正過時的 `<title>` 標籤或更新其他任何元素，你都會學會**載入 HTML 檔案**、修改文字，並安全地**更新 HTML 標題**（或任何元素）。

更改網頁的標題是清理爬取資料、產生靜態網站頁面或自動化 SEO 更新時的常見任務。在本教學中，你將會：

* 從磁碟載入 HTML 檔案。
* 找到 `<title>` 元素並**編輯 title 標籤**。
* 儲存已修改的文件，有效地**更新 HTML 標題**。

所有必要的程式碼皆已提供，且每一步都說明**為什麼**此操作重要，而不僅僅是**要輸入什麼**。

## 前置條件

在開始之前，請確保你已具備以下條件：

* 已安裝 Python 3.9 或更新版本。
* `lxml` 套件（`pip install lxml`）。  
  `lxml` 提供快速、符合標準的 HTML 解析與操作。
* 包含欲編輯之 HTML 檔案的目錄（將 `YOUR_DIRECTORY` 替換為實際路徑）。

## 步驟 1：載入 HTML 檔案

第一步是將 **載入 HTML 檔案** 成為 Python 可操作的 DOM（文件物件模型）樹。使用 `lxml.html` 可提供 XPath 支援與可靠的元素處理。

```python
from pathlib import Path
from lxml import html

# Path to the source HTML document
source_path = Path("YOUR_DIRECTORY/page.html")

# Parse the file into an HTML tree
doc = html.parse(str(source_path))
```

**為什麼這很重要：**  
解析會產生頁面的結構化表示，讓你能直接查詢元素。若未載入檔案，就無法安全地**更改元素文字**，因為只能處理原始字串，容易出錯。

## 步驟 2：定位 `<title>` 元素並**更改元素文字**

現在文件已載入，你可以**編輯 title 標籤**。XPath 表達式 `".//title"` 會在文件層級中找到第一個 `<title>` 元素。

```python
# Find the <title> element (the first occurrence)
title_elem = doc.find(".//title")

# Guard against missing <title>
if title_elem is None:
    raise ValueError("The document does not contain a <title> element.")

# Change the text inside the <title> tag
title_elem.text = "New Title"
```

**為什麼這很重要：**  
直接對 `title_elem.text` 進行賦值即可**更改元素文字**，而不會改動周圍的標記。此方式保留空白、註解與其他標籤，確保輸出仍為有效的 HTML。

### 邊緣情況：多個 `<title>` 標籤

HTML 標準只允許一個 `<title>` 元素，但不良格式的檔案有時會出現多個。若需處理此情況，可遍歷所有匹配項目：

```python
for t in doc.findall(".//title"):
    t.text = "New Title"
```

## 步驟 3：儲存已修改的文件 – **更新 HTML 標題**

完成修改後，將樹寫回磁碟。使用 `pretty_print=True` 可保持檔案可讀性。

```python
# Destination path for the updated file
output_path = Path("YOUR_DIRECTORY/updated.html")

# Write the updated HTML back to a file
doc.write(str(output_path), encoding="utf-8", pretty_print=True)
print(f"HTML saved to {output_path}")
```

**為什麼這很重要：**  
儲存會產生一個新檔案，反映**更改元素文字**的操作。若需覆寫原始檔案，只要將 `output_path` 設為相同路徑即可。

## 完整腳本（單一程式碼區塊）

將所有步驟整合在一起，以下是一個自包含的腳本，可**載入 HTML 檔案**、**更改元素文字**，並**更新 HTML 標題**：

```python
"""Change element text in an HTML document – update the <title> tag."""

from pathlib import Path
from lxml import html

def change_title(source: str, new_title: str, destination: str) -> None:
    """Load an HTML file, edit its title, and save the result."""
    # Load the HTML document
    doc = html.parse(source)

    # Locate the <title> element
    title_elem = doc.find(".//title")
    if title_elem is None:
        raise ValueError("No <title> element found in the document.")

    # Change element text
    title_elem.text = new_title

    # Save the updated document
    doc.write(destination, encoding="utf-8", pretty_print=True)

if __name__ == "__main__":
    src = "YOUR_DIRECTORY/page.html"
    dst = "YOUR_DIRECTORY/updated.html"
    change_title(src, "New Title", dst)
    print(f"Updated title saved to {dst}")
```

執行此腳本會產生 `updated.html` 檔案，其 `<title>` 現在為 **New Title**。

## 常見的技巧變形

### 編輯其他元素（例如 `<h1>`）

如果你需要為標題而非 title **更改元素文字**，請調整 XPath：

```python
heading = doc.find(".//h1")
if heading is not None:
    heading.text = "Updated Heading"
```

### 保留原有空白

當原始 HTML 在標籤內使用縮排時，`pretty_print` 可能會重新格式化。若要保留原始格式，請省略 `pretty_print`：

```python
doc.write(destination, encoding="utf-8")
```

### 處理 Unicode 字元

`lxml` 會自動處理 Unicode。請確保來源檔案以 UTF‑8 編碼儲存；若不是，則在開啟檔案時指定正確的編碼。

## 專業提示與常見陷阱

* **專業提示：** 若只需要文字內容而不修改元素，可使用 `doc.xpath("//title/text()")`。
* **注意：** 含有 `<title>` 位於 `<svg>` 或其他非 HTML 命名空間的 HTML 檔案。此時請將 XPath 精確到 `<head>` 部分：`doc.find(".//head/title")`。
* **效能提示：** 若批次處理上千個檔案，重複使用同一個 parser 實例以減少開銷。

## 結論

現在你已了解如何使用 Python 在 HTML 文件中**更改元素文字**，特別是**載入 HTML 檔案**、**編輯 title 標籤**以及**更新 HTML 標題**。完整範例展示了一種可靠、基於函式庫的方法，適用於格式良好或略有錯誤的 HTML。

接下來你可以：

* 將相同模式套用到其他標籤（`<h2>`、`<meta>` 等）。
* 將此腳本與網頁爬蟲流程結合，清理大量頁面。
* 探索 `lxml` 更豐富的 API，用於屬性操作、CSS 選擇器與 HTML 序列化。

祝程式開發順利，歡迎隨意嘗試不同元素，以精通 Python 的 HTML 操作！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在所示技巧之上。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [在 Aspose.HTML for Java 中從檔案載入 HTML 文件](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [在 Aspose.HTML for Java 中編輯 HTML 文件樹](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [在 Aspose.HTML for Java 中解析 HTML – 載入、查詢與計算元素](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}