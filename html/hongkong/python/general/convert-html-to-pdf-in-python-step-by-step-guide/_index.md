---
category: general
date: 2026-08-06
description: 使用 Python 將 HTML 轉換為 PDF 的完整範例。學習如何從 HTML 產生 PDF、將 HTML 儲存為 PDF，並處理常見的邊緣案例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: zh-hant
lastmod: 2026-08-06
og_description: 使用 Python 將 HTML 轉換為 PDF 並自動化文件建立。跟隨本指南從 HTML 產生 PDF、將 HTML 儲存為 PDF，並自訂輸出。
og_image_alt: Example of convert html to pdf script in Python
og_title: 在 Python 中將 HTML 轉換為 PDF – 全面教學
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: 在 Python 中將 HTML 轉換為 PDF – 步驟教學
url: /zh-hant/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to PDF in Python – step‑by‑step guide

如果你需要 **快速將 HTML 轉換成 PDF**，本教學將在 Python 中示範完整解決方案。你將學會如何從 HTML 產生 PDF、將 HTML 儲存為 PDF，並在程式碼內控制轉換流程。

本指南會一步步說明安裝可靠的函式庫、載入 HTML 文件、執行轉換以及驗證結果。完成後，你即可在任何 Python 專案中，無論來源是靜態頁面或動態產生的標記，都能將 HTML 轉成 PDF。

## 你將學會

* 安裝 `pdfkit` 與 `wkhtmltopdf` 兩個必須的相依套件，以執行 HTML → PDF 轉換。  
* 從磁碟或字串載入 HTML 文件。  
* 使用自訂頁面尺寸、邊距與編碼選項，從 HTML 產生 PDF。  
* 只需一行程式碼即可將 HTML 儲存為 PDF。  
* 處理常見的例外情況，例如資源遺失、Unicode 字元與大型檔案。  

**先備條件** – Python 3.8+ 以及基本的檔案 I/O 知識。無需外部服務。

## Convert HTML to PDF – overall workflow

轉換流程分為三個邏輯階段：

1. **準備階段** – 安裝轉換器並確保 `wkhtmltopdf` 可執行檔可被找到。  
2. **輸入處理** – 讀取 HTML 檔案或程式動態產生標記。  
3. **輸出產生** – 呼叫轉換器、寫入 PDF 檔案，並確認結果。

以下每個階段都有專屬步驟說明。

## Step 1: Install required libraries

`pdfkit` 為廣受使用的 `wkhtmltopdf` 引擎提供輕量的 Python 包裝器。使用 `pip` 同時安裝兩者，並驗證二進位檔路徑。

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

如果你偏好可攜式二進位檔，請從 [wkhtmltopdf GitHub page](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) 下載相應版本，並放置於已加入 `PATH` 的目錄中。腳本稍後會自動檢查路徑。

## Step 2: Load the HTML document

你可以讀取本機檔案、抓取遠端內容，或即時產生 HTML。以下範例載入位於自訂目錄下的 `sample.html` 本機檔案。

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

以 Unicode 字串讀取檔案，可確保「é」、「ß」或亞洲字形等字元在轉換過程中不會遺失。當你 **從 HTML 產生 PDF** 且內容包含國際文字時，此步驟相當重要。

## Step 3: Generate PDF from HTML

`pdfkit.from_string` 會將包含 HTML 標記的字串轉換成 PDF 檔案。你可以傳入選項字典，以控制頁面尺寸、邊距與頁首/頁尾行為。

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

上述呼叫 **從 HTML 檔案建立 PDF**，結果儲存於 `sample.pdf`。若來源 HTML 參照本機 CSS 或圖片，`enable‑local‑file‑access` 旗標會讓 `wkhtmltopdf` 正確解析這些資源。

### Why this approach works

* `pdfkit` 將繁重的渲染工作交給 `wkhtmltopdf`，後者使用 WebKit 引擎渲染 HTML，確保版面與原始頁面高度相符。  
* 透過選項字典即可微調輸出，無需修改 HTML 本身。  
* 使用 `from_string` 可全程在記憶體中處理，適合即時產生的 HTML。

## Step 4: Save HTML as PDF and verify output

轉換完成後，你可能想確認 PDF 是否已正確產生且可讀。以下程式碼會檢查檔案大小，並以系統預設的檢視器開啟 PDF（依平台而異）。

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

執行腳本後會印出成功訊息，並自動開啟 PDF 檢視器，讓你即時驗證版面是否與原始 HTML 相符。此步驟完成 **save html as pdf** 的完整循環。

## Step 5: Advanced options – create PDF from HTML file with custom settings

有時你已經有實體的 HTML 檔案，想直接使用 `pdfkit.from_file` 而非自行讀取內容。當 HTML 含有複雜的相對路徑時，此方法特別方便。

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

你亦可透過擴充 `options` 字典，加入封面頁、目錄或 JavaScript 執行旗標。例如，加入封面頁的寫法如下：

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

這些調整示範了 **how to convert HTML to PDF** 在更進階的出版流程中的應用方式。

## Common pitfalls and how to avoid them

| Issue | Cause | Remedy |
|-------|-------|--------|
| 圖片或 CSS 無法顯示 | `wkhtmltopdf` 預設阻止本機檔案存取 | 在 options 字典中加入 `"enable-local-file-access": None` |
| Unicode 字元變成亂碼 | 缺少 `encoding` 選項或以錯誤編碼讀取檔案 | 必須設定 `"encoding": "UTF-8"`，且以 UTF‑8 讀取 HTML |
| PDF 為空白 | `wkhtmltopdf` 二進位檔路徑不正確 | 明確提供路徑：`pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| 大型 HTML 檔案逾時 | 預設逾時時間過短 | 設定 `"javascript-delay": "2000"` 或以 `"timeout": "60"` 延長逾時時間 |

解決上述問題即可在各種環境下穩定執行 **generate pdf from html**。

## Full script – end‑to‑end example

將以下程式碼存為 `html_to_pdf.py`，並以 `python html_to_pdf.py` 執行。請自行將 `YOUR_DIRECTORY` 改為你的專案資料夾路徑。

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## What Should You Learn Next?

以下教學與本篇內容密切相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並探索在專案中使用的其他實作方式。

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}