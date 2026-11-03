---
category: general
date: 2026-08-25
description: 學習如何使用簡單的 Python 程式碼建立 HTML 文件、選取元素的 CSS、修改 HTML 文字，並儲存 HTML 檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: zh-hant
lastmod: 2026-08-25
og_description: 使用幾行 Python 建立 HTML 文件、選取元素 CSS、修改 HTML 文字並儲存 HTML 檔案。跟隨此完整教學。
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: 使用 Python 建立 HTML 文件並編輯其內容 – 步驟說明指南
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: 如何在 Python 中建立 HTML 文件並編輯其內容
url: /zh-hant/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中建立 html 文件並編輯其內容

如果你需要從頭**create html document**並以程式方式變更其元素，本指南會完整說明。你將看到一段簡短且可執行的腳本，該腳本會建立檔案、使用 CSS selector 選取段落、更新文字，並將結果寫回磁碟。

在 Python 中處理 HTML 是在產生報告、電子郵件範本或靜態網站內容時的常見需求。完成本教學後，你將能夠**select element css**、**modify html text**以及**save html file**，且全程不必離開你的 IDE。

## 前置條件

* 已安裝 Python 3.9 或更新版本。
* `beautifulsoup4` 與 `lxml` 套件（使用 `pip install beautifulsoup4 lxml` 安裝）。
* 具備寫入目標目錄的權限，以儲存輸出檔案。

不需要額外工具；標準函式庫已能處理檔案 I/O。

## 步驟 1：安裝必要的函式庫

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` 提供便利的 API 用於解析與操作 HTML，而 `lxml` 則提供支援 CSS selector 的高速解析器。

## 步驟 2：建立初始 HTML 文件

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

`BeautifulSoup` 建構子會在記憶體中建立一個 **create html document** 物件。使用 `"lxml"` 解析器可確保完整的 CSS selector 支援。

## 步驟 3：使用 CSS selector 選取段落元素

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

`select_one` 方法實作 **select element css** 邏輯，回傳第一個符合的標籤。若 selector 找不到任何匹配，`para` 會是 `None`，因此在正式程式碼中建議加入防呆檢查。

## 步驟 4：修改段落的文字內容

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

將 `para.string` 設定為新值會執行 **modify html text** 操作。BeautifulSoup 會更新底層的 DOM 樹，因而在文件序列化時呈現變更。

## 步驟 5：將更新後的 HTML 儲存至檔案

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

`open` 搭配 `write` 實作 **save html file** 功能。使用 `prettify()` 可產生格式良好的縮排輸出，對除錯很有幫助。

### 完整腳本，方便直接複製貼上

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

執行 `python edit_html.py` 後會產生包含以下內容的 `updated.html`：

```html
<p>
 New
</p>
```

## 常見變形與邊緣情況

### 選取多個元素

如果需要 **select element css** 能匹配多個標籤（例如 `"div.note"`），可使用 `doc.select("div.note")`，它會回傳一個列表。遍歷該列表即可對每個元素套用變更。

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### 保留現有屬性

當你替換文字時，BeautifulSoup 會保留標籤上的所有屬性。例如：

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### 優雅處理缺失的元素

在正式腳本中，常會遇到不完整的 HTML。請如 Step 4 所示，將選取動作包在條件判斷或 try‑except 區塊中，以避免程式崩潰。

### 寫入特定目錄

將 `output_path` 替換為絕對或相對路徑：

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

請確保目錄已存在；否則 Python 會拋出 `FileNotFoundError`。

## 專業提示

* **Performance** – 對於大型 HTML 檔案，建議直接使用 `lxml.etree`；BeautifulSoup 雖提供便利的抽象層，但速度稍慢。
* **Encoding** – 開啟檔案時務必使用 `encoding="utf-8"`，以保留非 ASCII 字元。
* **Testing** – 變更完成後，可在單元測試中使用 `assert "New" in open(output_path).read()` 來驗證輸出。

## 結論

現在你已掌握如何 **create html document**、使用 **select element css** 查詢定位節點、**modify html text**，以及最終以 Python **save html file**。此流程可擴展至更複雜的轉換，例如批次更新、屬性變更或範本產生。

接下來，可探索相關主題，如使用 XPath 表達式 **how to edit html**、以 Jinja2 產生完整 HTML 頁面，或自動化多檔案的批次處理。這些皆以本教學的核心步驟為基礎，擴充你在程式化 HTML 操作上的工具箱。

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [使用 Aspose.HTML 建立 HTML 文件 – 步驟說明指南](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [如何在 Aspose.HTML for Java 中編輯 HTML 文件樹](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [在 Aspose.HTML for Java 中儲存 HTML 文件](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}