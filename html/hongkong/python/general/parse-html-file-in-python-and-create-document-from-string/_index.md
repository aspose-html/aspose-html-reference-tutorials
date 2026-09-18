---
category: general
date: 2026-09-16
description: 在 Python 中解析 HTML 檔案，從檔案載入 HTML 文件，並以簡單、可直接執行的程式碼從字串建立 HTML 文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- parse html file in python
- create html document from string
- load html document from file
- read local html file python
language: zh-hant
lastmod: 2026-09-16
og_description: 在 Python 中解析 HTML 檔案，以快速可靠地讀取本機 HTML 檔案，並從字串建立 HTML 文件。
og_image_alt: Screenshot of Python code parsing an HTML file and creating a document
  from a string
og_title: 在 Python 中解析 HTML 檔案 – 從字串建立文件
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  headline: Parse HTML file in Python and create document from string
  type: TechArticle
- description: Parse HTML file in Python, load HTML document from file, and create
    HTML document from string with simple, ready‑to‑run code.
  name: Parse HTML file in Python and create document from string
  steps:
  - name: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
    text: '**Detect source type** – The constructor checks whether the supplied `source`
      exists on disk. If it does, we **load html document from file**; otherwise we
      treat it as a raw string, satisfying the **create html document from string**
      requirement.'
  - name: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
    text: '**Read the file** – We use `Path.read_text(encoding="utf-8")` which is
      the recommended way to **read local html file python** safely.'
  - name: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
    text: '**Parse with BeautifulSoup** – The `lxml` parser is fast and tolerant of
      malformed markup.'
  type: HowTo
tags:
- python html parsing
- html document creation
- file handling python
title: 在 Python 中解析 HTML 檔案，並從字串建立文件
url: /zh-hant/python/general/parse-html-file-in-python-and-create-document-from-string/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中解析 HTML 檔案並從字串建立文件

如果你需要 **在 Python 中解析 HTML 檔案**，本指南會精確說明如何讀取本機 HTML 檔案、從檔案載入 HTML 文件，以及 **從字串建立 HTML 文件**。無論你是進行資料爬取、測試模板，或是產生動態內容，以下步驟都會提供完整且可執行的解決方案。

在本教學中，你將學會：

* 使用 Python 標準函式庫讀取本機 HTML 檔案。
* 從檔案路徑載入 HTML 文件。
* 直接從 HTML 字串建立文件。
* 處理常見的例外情況，例如檔案遺失與編碼問題。

唯一的前置條件是 Python 3.8+ 與 `beautifulsoup4` 套件，我們會在第一步安裝它。

## 前置條件

| 需求 | 重要原因 |
|------|----------|
| Python 3.8 或更新版本 | 確保與型別提示與現代語法相容。 |
| `beautifulsoup4` 與 `lxml` 套件 | 提供強韌的解析器，能處理不良格式的 HTML，並提供方便的 `HTMLDocument`‑like 物件。 |
| 專案資料夾中的範例 HTML 檔案 (`index.html`) | 作為 **load html document from file** 範例的輸入。 |

使用 pip 安裝相依套件：

```bash
pip install beautifulsoup4 lxml
```

## 在 Python 中解析 HTML 檔案

本教學的核心是 **parse html file in python** 操作。我們會將 BeautifulSoup 包裝在一個名為 `HTMLDocument` 的小型輔助類別中，使 API 與先前看到的範例相符。

```python
from pathlib import Path
from bs4 import BeautifulSoup
from typing import Union

class HTMLDocument:
    """
    Simple wrapper that mimics a “document” object.
    Accepts either a file path or a raw HTML string.
    """
    def __init__(self, source: Union[str, Path]):
        if Path(source).exists():
            # Load html document from file
            self._load_from_file(Path(source))
        else:
            # Assume source is a raw HTML string
            self._load_from_string(source)

    def _load_from_file(self, file_path: Path):
        try:
            # read local html file python – explicit UTF‑8 handling
            html = file_path.read_text(encoding="utf-8")
        except FileNotFoundError:
            raise FileNotFoundError(f"File not found: {file_path}")
        self.soup = BeautifulSoup(html, "lxml")

    def _load_from_string(self, html_string: str):
        self.soup = BeautifulSoup(html_string, "lxml")

    def title(self) -> str:
        """Return the content of the <title> tag, or an empty string."""
        if self.soup.title:
            return self.soup.title.string.strip()
        return ""

    def pretty(self) -> str:
        """Return a nicely formatted HTML representation."""
        return self.soup.prettify()
```

### 運作原理

1. **Detect source type** – 建構子會檢查提供的 `source` 是否在磁碟上存在。若存在，我們會 **load html document from file**；否則將其視為原始字串，以符合 **create html document from string** 的需求。  
2. **Read the file** – 我們使用 `Path.read_text(encoding="utf-8")`，這是安全地 **read local html file python** 的推薦方式。  
3. **Parse with BeautifulSoup** – `lxml` 解析器速度快且能容忍格式不良的標記。

## 從檔案載入 HTML 文件

既然已有 `HTMLDocument` 類別，載入檔案變得相當直接：

```python
# Step 1: Load an HTML document from a local file
doc = HTMLDocument("YOUR_DIRECTORY/index.html")

# Verify that the file was parsed correctly
print("Document title:", doc.title())
```

**預期輸出**（假設 `index.html` 包含 `<title>My Page</title>`）：

```
Document title: My Page
```

如果檔案不存在，類別會拋出清楚的 `FileNotFoundError`，你可以在正式程式碼中捕獲它。

## 從字串建立 HTML 文件

直接從字串建立文件對於測試或即時產生 HTML 十分有用：

```python
# Step 2: Create an HTML document directly from an HTML string
html_content = "<html><head><title>Hello</title></head><body><h1>Hello</h1></body></html>"
doc_from_string = HTMLDocument(html_content)

print("String‑based title:", doc_from_string.title())
```

**預期輸出**：

```
String-based title: Hello
```

因為相同的 `HTMLDocument` 類別同時處理兩種情況，你即可取得一致的 API 來 **parse html file in python**，不論來源是檔案或字串。

## 讀取本機 HTML 檔案（Python）– 處理例外情況

在處理真實世界的檔案時，你常會遇到：

* **Missing files** – 已由 `FileNotFoundError` 處理。  
* **Different encodings** – 你可以讓 BeautifulSoup 自行偵測編碼，但明確指定 UTF‑8 最安全。  
* **Large files** – 讀取整個檔案至記憶體可能成本高；如有需要可使用 `BeautifulSoup(open(...), "lxml")` 進行串流。

以下是一個防禦式的包裝器，加入了上述保護措施：

```python
def safe_load_html(path: Union[str, Path]) -> HTMLDocument:
    """
    Load an HTML file safely, handling missing files and encoding issues.
    Returns an HTMLDocument instance or raises a descriptive exception.
    """
    try:
        return HTMLDocument(path)
    except FileNotFoundError as e:
        raise RuntimeError(f"Unable to read local HTML file Python: {e}")
    except UnicodeDecodeError:
        raise RuntimeError("File encoding is not UTF-8; consider specifying the correct encoding.")
```

現在你可以呼叫 `safe_load_html("index.html")`，並自信地取得相同的 `HTMLDocument` 物件，錯誤會被清楚回報。

## 專業提示與常見陷阱

* **Avoid “just” using `open(...).read()`** – `Path.read_text` 只用一行就能處理路徑展開與編碼。  
* **Don’t forget to close file handles** – `Path.read_text` 會自動關閉檔案；若使用 `open()`，請以 `with` 區塊包住。  
* **Prefer `lxml` over the default parser** – 它更快且更能容忍破損的標記，這在你 **parse html file in python** 從網路抓取時尤為重要。  
* **When creating from a string, ensure it’s a complete HTML document** – 缺少 `<html>` 或 `<body>` 標籤可能導致查詢元素時得到意外的 `None` 結果。

## 完整腳本（可直接複製貼上）

以下是一個自包含的腳本，示範本文討論的每一步。將它儲存為 `html_demo.py`，然後執行 `python html_demo.py`。



## 接下來你應該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸技術。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [在 Aspose.HTML for Java 中將 HTML 文件儲存至檔案](/html/english/java/saving-html-documents/save-html-to-file/)
- [在 Aspose.HTML for Java 中從檔案載入 HTML 文件](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [使用 Aspose.HTML 建立 HTML 文件 – 步驟說明指南](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}