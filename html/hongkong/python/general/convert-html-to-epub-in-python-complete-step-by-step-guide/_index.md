---
category: general
date: 2026-07-18
description: 在 Python 中快速將 HTML 轉換為 EPUB。學習如何在 Python 載入 HTML 檔案，並使用簡易函式庫將 HTML 轉換為
  MHTML。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: zh-hant
lastmod: 2026-07-18
og_description: 使用 Python 將 HTML 轉換為 EPUB，提供清晰可執行的範例。同時學習如何在 Python 中載入 HTML 檔案，並在數分鐘內將
  HTML 轉換為 MHTML。
og_image_alt: Diagram showing convert html to epub workflow
og_title: 使用 Python 將 HTML 轉換為 EPUB – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: 使用 Python 將 HTML 轉換為 EPUB – 完整逐步指南
url: /zh-hant/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中將 HTML 轉換為 EPUB – 完整步驟指南

有沒有想過要 **將 HTML 轉換成 EPUB** 卻不想抓狂？你不是唯一的開發者——大家常常需要把網頁變成離線閱讀的電子書，而在 Python 中完成這件事其實相當簡單。本文將示範如何在 Python 中載入 HTML 檔案、將 HTML 轉成 EPUB，甚至再把同一來源轉成 MHTML（適合寄信的單檔網頁封存）。

閱讀完本指南後，你將擁有一支可直接執行的腳本，只要給它一個 `sample.html`，就能同時產出 `sample.epub` 與 `sample.mhtml`。沒有神祕，只要清晰的程式碼與說明。

---

![Conversion pipeline diagram](https://example.com/images/convert-html-epub.png "Diagram showing convert html to epub workflow")

## 你將會建立的功能

- **在 Python 中載入 HTML 檔案**，使用內建的 `pathlib` 與 `io` 模組。  
- **使用 ebooklib 套件將 HTML 轉成 EPUB**，它會自動處理 EPUB 容器格式。  
- **使用 email 套件將 HTML 轉成 MHTML**（亦稱 MHT），產生瀏覽器可直接開啟的單檔網頁封存。  

我們還會說明：

- 必要的相依套件以及安裝方式。  
- 錯誤處理，讓腳本能優雅失敗。  
- 如何自訂 EPUB 的 metadata（如書名、作者）。  

準備好了嗎？讓我們開始吧。

---

## 前置條件

在開始寫程式之前，請先確認你已具備：

1. **Python 3.9+** – 本教學使用的語法在任何近期版本皆可執行。  
2. **pip** – 用來安裝第三方套件。  
3. 一個簡單的 HTML 檔案，例如 `sample.html`，放在你可控制的資料夾內。  

如果以上都已備妥，請直接跳到下一節。

> **小技巧：** 請確保你的 HTML 結構完整（正確的 `<head>` 與 `<body>`）。雖然 `ebooklib` 會嘗試自動修正小問題，但乾淨的原始碼能減少之後的麻煩。

---

## 步驟 1 – 安裝必要的函式庫

我們需要兩個外部套件：

- **ebooklib** – 用於產生 EPUB。  
- **beautifulsoup4** – 雖非必須，但在轉換前清理 HTML 時非常方便。

在終端機執行以下指令：

```bash
pip install ebooklib beautifulsoup4
```

> **為什麼需要這兩個套件？** `ebooklib` 會為你建立 ZIP 結構的 EPUB，並自動處理 `META‑INF` 資料夾、`content.opf` 與 `toc.ncx`。`beautifulsoup4` 則可協助整理 HTML，確保最終的電子書在各種閱讀器上都能正確顯示。

---

## 步驟 2 – 在 Python 中載入 HTML 檔案

載入 HTML 檔案相當簡單，我們會把它包裝成一個小工具函式，回傳 **BeautifulSoup** 物件供後續使用。

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**說明：**  
- `Path` 提供跨平台的檔案操作。  
- 使用 `read_text` 可免除手動 `open`/`close` 的樣板程式碼。  
- 回傳 `BeautifulSoup` 物件後，我們就能在 **將 HTML 轉換為 EPUB** 前，移除 script、修正破損標籤或注入樣式表。

---

## 步驟 3 – 將 HTML 轉成 EPUB

現在我們已能 **在 Python 中載入 HTML 檔案**，接下來把它轉換成乾淨的 EPUB。以下函式接受 `BeautifulSoup` 物件、目標路徑，並可自行設定 metadata。

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**為什麼這樣可行：**  
- `ebooklib.epub.EpubBook` 抽象化了 ZIP 容器與必要的 manifest 檔案。  
- 我們產生一個 UUID 作為識別碼，避免大量產書時出現重複 ID。  
- `spine` 定義章節順序；對於大多數簡單的 HTML 來源，單章節書即可。

**執行轉換：**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

執行腳本後，你會看到一個綠色勾勾，顯示 EPUB 檔案已成功產生。

---

## 步驟 4 – 將 HTML 轉成 MHTML

MHTML（或 MHT）會把 HTML 與所有資源（圖片、CSS）打包成單一 MIME 檔案。Python 的 `email` 套件即可在不安裝額外套件的情況下產生此格式。

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**重點說明：**  

- `multipart/related` MIME 類型告訴瀏覽器，HTML 部分與其資源屬於同一組。  
- 我們會遍歷 `<img>` 標籤將圖片內嵌；若不需要圖片，可略過此段程式。  
- `Content-Location` 使用 `file://` URI，讓瀏覽器在本機內部解析資源。

**呼叫函式：**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

現在 `sample.epub` 與 `sample.mhtml` 已經並排放在同一目錄下。

---

## 完整腳本 – 一次搞定所有步驟

以下是完整、可直接執行的腳本，將前面的所有步驟整合在一起。將它存為 `convert_html.py`，並將 `YOUR_DIRECTORY` 替換成放置 `sample.html` 的路徑。

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
convert_html.py

A tiny utility that demonstrates:
- How to load an HTML file in Python
- How to convert HTML to EPUB (convert html to epub)
- How to convert HTML to MHTML (convert html to mhtml)

Author: Your Name
Date: 2026‑07‑18
"""

from pathlib import Path
import uuid
import mimetypes


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [How to Convert EPUB to Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}