---
category: general
date: 2026-07-02
description: 學習如何在 Python 中載入 HTML、透過 ID 取得元素，並從檔案中擷取文字。本實用教學示範如何使用 BeautifulSoup
  讀取 HTML 檔案。
draft: false
keywords:
- how to load html
- how to get element
- how to extract text
- get element by id
- read html file python
language: zh-hant
og_description: 如何在 Python 中載入 HTML 並使用 BeautifulSoup 抽取文字。請跟隨本指南讀取 HTML 檔案、透過 id
  取得元素，並列印其內容。
og_title: 如何在 Python 中載入 HTML – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  headline: How to Load HTML in Python – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to load HTML in Python, get element by id, and extract text
    from a file. This practical tutorial shows reading HTML files with BeautifulSoup.
  name: How to Load HTML in Python – Step‑by‑Step Guide
  steps:
  - name: What if the HTML is malformed?
    text: BeautifulSoup’s `lxml` parser is forgiving, but for severely broken markup
      you might want to fallback to the built‑in `html.parser`. Swap `"lxml"` with
      `"html.parser"` in the `BeautifulSoup` constructor.
  - name: How to handle multiple elements with the same ID?
    text: HTML spec says IDs should be unique, but reality sometimes disagrees. Use
      `soup.find_all(id="duplicate-id")` to retrieve a list, then iterate over it.
  - name: Need to read from a URL instead of a file?
    text: Replace the file‑reading logic with `requests.get(url).text`. Remember to
      install the `requests` package (`pip install requests`) and handle network errors
      gracefully.
  - name: Want to extract other attributes (e.g., `class` or `href`)?
    text: 'Simply access them like a dictionary: `header[''class'']` or `header[''href'']`.
      If the attribute might be missing, use `.get(''class'')` to avoid `KeyError`.'
  type: HowTo
tags:
- Python
- HTML parsing
- BeautifulSoup
title: 如何在 Python 中載入 HTML – 步驟指南
url: /zh-hant/python/general/how-to-load-html-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中載入 HTML – 完整教學

有沒有想過 **如何在 Python 程式中載入 HTML** 而不抓狂？你並不是唯一有此困擾的人。無論是爬取新聞網站、處理本機報告，或只是需要從電子郵件範本中抓取標題，掌握載入 HTML 的技巧都是每位開發者必備的能力。

在本指南中，我們將一步步說明 **如何依 ID 取得元素**、**如何擷取文字**，最後列印結果——同時保持程式碼簡潔且具 Python 風格。我們也會討論 **在 Python 中讀取 HTML 檔案** 的細節，讓你現在就能直接複製貼上可執行的解決方案。

> **專業小技巧：** 範例使用廣受歡迎的 *BeautifulSoup* 套件，因為它輕量、文件齊全，且能處理簡單與複雜的 HTML 結構。

## 需要的環境

在開始之前，請確保你已具備：

- Python 3.9 或更新版本（程式碼亦相容於 3.10+）
- 已安裝 `beautifulsoup4` 與 `lxml`（`pip install beautifulsoup4 lxml`）
- 一個範例 HTML 檔案 — 我們稱之為 `sample.html`，放在名為 `YOUR_DIRECTORY` 的資料夾內

就這樣。無需沉重的瀏覽器、無需 Selenium，純粹使用 Python。

## 步驟 1：如何載入 HTML – 將檔案讀入記憶體

首先要做的事就是 **讀取 HTML 檔案**。這是所有後續步驟的基礎，務必要做好。

```python
from pathlib import Path

# Define the path to the HTML file
html_path = Path("YOUR_DIRECTORY/sample.html")

# Read the file contents as a string
html_content = html_path.read_text(encoding="utf-8")
```

*為什麼這很重要：* 使用 `Path.read_text` 可抽象化作業系統特有的換行符，並自動處理 UTF‑8（現代網頁的事實標準編碼）。若檔案遺失，`Path.read_text` 會拋出清晰的 `FileNotFoundError`，讓除錯變得輕鬆。

## 步驟 2：解析 HTML 文件

取得原始字串後，我們需要 **載入 HTML** 到解析器物件。BeautifulSoup 提供了便利的 API 讓你在 DOM 中巡航。

```python
from bs4 import BeautifulSoup

# Create a BeautifulSoup object using the lxml parser (fast and reliable)
soup = BeautifulSoup(html_content, "lxml")
```

*為什麼選擇 lxml？* `lxml` 解析器比 Python 內建的解析器快許多，且對不完整的標記容錯度更高——非常適合實務上可能會爬到的雜亂 HTML。

## 步驟 3：依 ID 取得元素 – 定位標題

文件已解析完畢，接下來回答 **如何依 ID 取得元素** 的問題。在本例中，我們要找的是 `id` 屬性等於 `"main-header"` 的 `<h1>` 標籤。

```python
# Retrieve the element with the specific ID
header = soup.find(id="main-header")
```

如果找不到元素，`header` 會是 `None`。最佳實踐是對此情況做好防護：

```python
if header is None:
    raise ValueError("Element with id='main-header' not found in the HTML file.")
```

## 步驟 4：如何擷取文字 – 取得內部內容

取得元素後，擷取其文字內容變得輕而易舉。這就是 **如何擷取文字** 從標籤的答案。

```python
# Extract the visible text inside the element
header_text = header.get_text(strip=True)  # strip removes surrounding whitespace
```

`get_text` 會自動串接所有子文字節點，無需自行迭代子節點。`strip=True` 參數會去除換行與多餘空格，讓你得到乾淨的字串。

## 步驟 5：列印結果 – 驗證一切正常

最後，將結果輸出到主控台。這相當於原始範例中的 `print(header.text_content)` 行為。

```python
print(header_text)  # prints: The text inside <h1 id="main-header">
```

執行腳本後若看到預期的標題，恭喜你！你已成功 **在 Python 中讀取 HTML 檔案**、依 ID 定位元素，並擷取其文字。

## 完整可執行範例

以下是完整、可直接執行的腳本。將它存為 `extract_header.py`，然後執行 `python extract_header.py`。

```python
# extract_header.py
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(file_path: str) -> str:
    """Read an HTML file and return its contents as a string."""
    path = Path(file_path)
    if not path.is_file():
        raise FileNotFoundError(f"Unable to locate the file: {file_path}")
    return path.read_text(encoding="utf-8")

def get_element_by_id(soup: BeautifulSoup, element_id: str):
    """Return the first tag with the given id, or raise an informative error."""
    element = soup.find(id=element_id)
    if element is None:
        raise ValueError(f"Element with id='{element_id}' not found.")
    return element

def main():
    # Step 1: Load the HTML document
    html = load_html("YOUR_DIRECTORY/sample.html")
    
    # Step 2: Parse the HTML with BeautifulSoup
    soup = BeautifulSoup(html, "lxml")
    
    # Step 3: Retrieve the element by its ID
    header = get_element_by_id(soup, "main-header")
    
    # Step 4: Extract and print the text content
    print(header.get_text(strip=True))

if __name__ == "__main__":
    main()
```

**預期輸出**（假設 `sample.html` 內含 `<h1 id="main-header">Welcome to My Site</h1>`）：

```
Welcome to My Site
```

就這樣——只需一個腳本，除了 BeautifulSoup 與 lxml 之外不需要其他相依套件。

## 常見問題與邊緣案例

### HTML 損壞時該怎麼辦？

BeautifulSoup 的 `lxml` 解析器相當寬容，但若標記嚴重損毀，建議改用內建的 `html.parser`。只要在 `BeautifulSoup` 建構子中將 `"lxml"` 換成 `"html.parser"` 即可。

### 同一 ID 出現多次該如何處理？

HTML 規範要求 ID 必須唯一，但實務上有時會違規。使用 `soup.find_all(id="duplicate-id")` 取得列表，然後自行迭代。

### 想從 URL 讀取而非檔案？

將讀檔邏輯改為 `requests.get(url).text`。別忘了安裝 `requests` 套件（`pip install requests`），並妥善處理網路錯誤。

### 想擷取其他屬性（例如 `class` 或 `href`）？

直接像字典一樣存取：`header['class']` 或 `header['href']`。若屬性可能不存在，使用 `.get('class')` 以避免 `KeyError`。

## 視覺摘要

![如何載入 HTML 範例](https://example.com/placeholder-image.png "如何載入 HTML 範例")

*替代文字：* 如何載入 HTML 範例 – 示意圖說明從檔案讀取到文字擷取的流程。

## 重點回顧

我們已說明 **如何在 Python 中載入 HTML**，示範 **如何依 ID 取得元素**，以及 **如何從該元素擷取文字**。依照上述步驟，你可以可靠地 **在 Python 中讀取 HTML 檔案**、操作 DOM，並抽取所需資訊。

## 接下來可以學什麼？

- **探索 CSS 選擇器：** 使用 `soup.select_one('.my-class')` 進行更彈性的查詢。
- **批次爬取多頁面：** 結合 `requests` 與迴圈，批次處理網站。
- **寫回 HTML：** BeautifulSoup 也支援修改樹狀結構並儲存——對於模板任務相當便利。
- **效能調校：** 處理大型檔案時，可考慮使用 `lxml.etree.iterparse` 等串流解析器。

盡情實驗吧——換掉 ID、嘗試不同標籤，甚至改用 `xml.etree.ElementTree` 來處理 XHTML。概念相同，而你現在已擁有堅實的基礎，迎接任何 HTML 解析的挑戰。

祝編程愉快！如果遇到問題或有酷炫的使用案例想分享，歡迎在下方留言。

## 接下來該學什麼？

以下教學與本篇內容密切相關，能在此基礎上延伸技巧。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並探索在專案中實作的不同方式。

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}