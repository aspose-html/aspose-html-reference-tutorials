---
category: general
date: 2026-05-31
description: 學習如何使用 Python 透過 ID 取得元素、更改 HTML 背景顏色、讀取 HTML 文字以及設定 HTML 屬性。一步一步的教學。
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: zh-hant
og_description: 使用 Python 在單一步驟、易於跟隨的指南中，透過 id 取得元素、讀取 HTML 文字、設定 HTML 屬性及變更背景顏色。
og_title: 在 Python 中透過 ID 取得元素 – 完整 HTML 操作教學
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: 在 Python 中透過 id 取得元素 – 完整 HTML 操作指南
url: /zh-hant/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中透過 ID 取得元素 – 完整 HTML 操作指南

有沒有曾經在寫快速的 Python 腳本時，需要從 HTML 頁面 **get element by id**？你並不孤單——大多數開發者在開始爬取網站或調整本地報告時，都會遇到這個障礙。好消息是，只要幾行程式碼，就能讀取元素的文字、變更其背景顏色，甚至設定新屬性，全部都在編輯器內完成。

在本教學中，我們將示範一個真實案例：載入本機的 `sample.html`，取得 ID 為 `main‑content` 的元素，印出其內部文字，最後將背景顏色換成淡灰色。完成後，你還會了解 **how to read HTML text**、**how to set HTML attribute**，以及為什麼 **manipulate HTML with Python** 是任何自動化工具箱中實用的技能。

## 需要的環境

- **Python 3.9+**（任何較新版本皆可）
- **`lxml`** 函式庫（或 **BeautifulSoup**，若你偏好）——我們會使用 `lxml.html`，因為它提供類似 `get_element_by_id` 的乾淨 API。
- 一個名為 `sample.html` 的小型 HTML 檔案，放在名為 `YOUR_DIRECTORY` 的資料夾中。隨意將下方程式碼片段複製到該檔案內：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

就這樣——不需要任何花俏框架，只要純粹的 Python 與一個靜態 HTML 檔案。

## 步驟 1：安裝必要的函式庫

如果尚未安裝 `lxml`，請開啟終端機並執行：

```bash
pip install lxml
```

*小技巧：* 使用虛擬環境可以保持全域 Python 的整潔，特別是當你同時處理多個專案時。

## 步驟 2：載入 HTML 文件

現在我們將把檔案讀入 `lxml.html` 的文件物件。可以把它想像成把原始文字轉換成可導航的樹狀結構。

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

執行後會印出「Document loaded successfully.」如果找不到檔案，Python 會拋出 `FileNotFoundError`——提前捕捉此錯誤可以避免追逐不存在的元素。

## 步驟 3：透過 ID 取得元素

這就是重點所在。`lxml` 提供了便利的 `get_element_by_id` 方法，與在 JavaScript 中使用的 DOM API 相呼應。

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

當元素存在時，控制台會印出「Element found!」。這就是 **get element by id** 步驟，為我們之後的大部分操作提供基礎。

## 步驟 4：如何讀取 HTML 文字

取得元素後，提取其可見文字非常簡單。`text_content()` 方法會回傳內部所有文字，且去除標籤。

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

預期輸出：

```
Inner text: Hello, world! This is the original text.
```

你可能會想，*如果元素內含巢狀標籤會怎樣？* `text_content()` 仍然有效——它會串接所有子孫文字節點，提供一個乾淨的字串，方便你記錄、儲存或作為其他演算法的輸入。

## 步驟 5：如何設定 HTML 屬性

變更或新增屬性同樣簡單。`set` 方法允許你指定任意屬性名稱。

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

輸出：

```
New attribute value: true
```

這行示範了即時 **how to set HTML attribute**。你可以將 `"data-modified"` 替換為 `"class"`、`"title"` 或任何該元素支援的屬性。

## 步驟 6：變更 HTML 背景顏色

接下來是視覺調整。要變更背景顏色，我們會注入一個 `style` 屬性來覆寫預設值。

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

執行腳本後，當你在瀏覽器開啟 `sample.html` 時，裡面的 `div` 會呈現如下：

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

這就是可重複使用於任何元素的 **change background colour html** 技巧——只要更換顏色代碼即可。

## 步驟 7：使用 Python 操作 HTML – 完整整合

以下是結合所有步驟的完整可執行腳本。將其儲存為 `modify_html.py`，並在與 `YOUR_DIRECTORY` 資料夾相同的目錄下執行。

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### 腳本逐行說明

1. **匯入** `lxml.html` 用於解析，並匯入 `pathlib` 以取得跨作業系統的路徑。  
2. **載入** `sample.html`，若檔案不存在則以清晰的錯誤訊息中止。  
3. **取得** 元素，使用 **get element by id**。  
4. **印出** 元素的文字——示範 **how to read HTML text**。  
5. **新增** 自訂屬性，說明 **how to set HTML attribute**。  
6. **變更** 背景顏色，滿足 **change background colour html** 的需求。  
7. **寫入** 更新後的標記至 `sample_modified.html`，讓你可以在瀏覽器中開啟並看到變更。

執行腳本會產生類似以下的控制台輸出：

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

開啟 `sample_modified.html`，你會看到文字背後的灰色背景——證明 **manipulate HTML with python** 確實可行。

## 常見陷阱與避免方法

- **Missing ID** – 若目標元素不存在，`get_element_by_id` 會回傳 `None`。在存取屬性前務必檢查是否為 `None`，否則會拋出 `AttributeError`。  
- **Encoding issues** – 讀取非 ASCII 頁面時，請在 `html.parse` 中傳入 `encoding='utf-8'`，或確保檔案以 UTF‑8 編碼儲存。  
- **Overwriting existing styles** – 設定 `style` 屬性會覆寫先前的內聯樣式。若需保留既有規則，請先讀取目前的 `style` 值，加入新規則後再寫回。  
- **File permissions** – 在唯讀系統中寫回同一資料夾可能失敗。請選擇可寫入的輸出路徑，如我們使用的 `sample_modified.html`。

## 延伸範例

既然你已掌握基礎，請考慮以下進階步驟：

- **Loop over multiple IDs** – 使用 ID 列表，搭配 `for` 迴圈批次處理頁面中的多個區段。  
- **Replace text content** – 呼叫 `elem.text = "New text"` 以修改可見字串。  
- **Add child elements** – 使用 `

## 接下來該學什麼？

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}