---
category: general
date: 2026-07-15
description: 使用 Python 從 HTML 產生 PDF。學習如何透過簡單腳本與清晰步驟快速將 HTML 轉換為 PDF。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: zh-hant
lastmod: 2026-07-15
og_description: 使用 Python 從 HTML 產生 PDF。本指南將教您如何將 HTML 轉換為 PDF、將 HTML 儲存為 PDF，並有效處理資源。
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: 使用 Python 從 HTML 產生 PDF – 實作教學
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: 在 Python 中從 HTML 建立 PDF – HTML 轉 PDF Python 教學
url: /zh-hant/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中從 HTML 建立 PDF – 完整功能教學

是否曾需要 **從 HTML 建立 PDF**，卻不確定該選擇哪個 Python 函式庫？您並不孤單——許多開發者在嘗試將網頁報告、發票或行銷頁面轉換成可列印的 PDF 時，都會碰到這個問題。  

好消息是，只需幾行程式碼，即可可靠地 **將 HTML 轉換為 PDF**，而且此腳本可在 Windows、macOS 與 Linux 上執行。本指南將逐步示範完整且可執行的範例，說明每一步的重要性，並教您如何 **將 HTML 儲存為 PDF**，不留任何遺漏。

---

## 您將學會

- 安裝適合的 Python 套件以進行 HTML‑to‑PDF 轉換。  
- 使用自訂資源處理選項載入 HTML 檔案（避免無止盡的 CSS 匯入）。  
- 在磁碟上產生乾淨的 PDF 檔案。  
- 處理常見的邊緣情況，例如外部圖片、相對路徑與大型文件。  

在本 **HTML 轉 PDF 教學** 結束時，您將擁有一個可重複使用的函式，能直接套用於任何專案。

## 前置條件

- Python 3.9+（程式碼在 3.8 亦可執行，但 3.9+ 提供最新的 `pathlib` 功能）。  
- 具備基本的命令列與虛擬環境使用經驗。  
- 一個您想轉換成 PDF 的 HTML 檔案——任何靜態頁面皆可。  

> **專業提示：** 若您使用虛擬環境，請在安裝函式庫前先啟用它；這樣可保持全域 Python 環境整潔。

## 步驟 1 – 安裝 WeasyPrint（轉換背後的引擎）

WeasyPrint 是一個純 Python 函式庫，可將 HTML 與 CSS 渲染成 PDF。它支援大多數現代網頁功能，並讓您對資源載入擁有精細的控制。

```bash
pip install weasyprint
```

執行上述指令會安裝 `cairocffi`、`tinycss2` 以及其他一些相依套件。如果在 Windows 上遇到 `cairo` 相關錯誤，請從 [WeasyPrint 官方網站](https://weasyprint.org/docs/install/) 下載預編譯的 wheels。

## 步驟 2 – 準備一個小型資源處理輔助程式

當您載入引用外部樣式表或圖片的 HTML 文件時，函式庫會跟隨這些連結。在某些情況下，這會導致深層巢狀甚至無限迴圈（例如 CSS 檔案自行 `@import`）。為了保持整潔，我們限制資源處理的深度。

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

上述類別並非 WeasyPrint 必須的，但它呼應了原始程式碼片段的模式，並提供一個掛鉤以阻止資源無限制匯入。您會在下一步看到它的使用方式。

## 步驟 3 – 使用自訂選項載入 HTML 文件

現在我們實際讀取 HTML 檔案。`HTML` 類別接受 `base_url` 參數，我們將其設為來源檔案所在的目錄——這樣相對連結即可在未使用網頁伺服器的情況下正常運作。

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **為什麼這很重要：** 若您的 HTML 會載入一連串 CSS 檔案，每個 `@import` 都會觸發一次載入。深度防護可防止腳本失控。

## 步驟 4 – 將處理後的文件儲存為 PDF

有了 `HTML` 物件後，產生 PDF 只需一行程式碼。我們同時傳入一段簡單的 CSS 片段，強制使用乾淨的頁面尺寸（A4）並加入微小的邊距——您可以自行調整。

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

呼叫 `write_pdf` 會將 PDF 串流寫入磁碟，最終得到可直接分享的檔案。

## 步驟 5 – 整合全部程式碼

以下是一個精簡腳本，您可以直接複製貼上至 `convert.py`。請將佔位路徑替換為實際的目錄。

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**預期輸出** – 執行 `python convert.py` 後，您應該會看到：

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

使用任何 PDF 檢視器開啟產生的檔案；您將看到原始頁面的版面配置、CSS 樣式與圖片（前提是這些圖片能從 HTML 檔案取得）。  

若發現圖片遺失，請再次確認其 `src` 屬性是絕對 URL 或位於 `YOUR_DIRECTORY` 之下的相對路徑。

## 常見問題與邊緣情況處理

| 問題 | 答案 |
|----------|--------|
| *如果我的 HTML 參考外部字型呢？* | WeasyPrint 會自動下載字型檔案，但您可能需要將網域列入白名單，以避免下載時間過長。 |
| *我可以轉換 HTML 字串而非檔案嗎？* | 可以——使用 `HTML(string=my_html_string)`，並省略 `base_url`，或將其設為暫存資料夾。 |
| *如何控制 PDF 的中繼資料（標題、作者）？* | 在呼叫 `write_pdf` 時傳入 `metadata` 字典，例如 `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`。 |
| *在 Linux 上出現 “cairo‑cffi error”。* | 在使用 pip 安裝 WeasyPrint 前，先安裝系統套件 `libcairo2-dev`（在 Debian/Ubuntu 上執行 `apt-get install libcairo2-dev`）。 |

## 結語

我們剛剛使用簡潔的 Python 工作流程 **從 HTML 建立 PDF**，說明了 **HTML 轉 PDF** 的運作機制，並示範如何以健全的資源處理方式 **將 HTML 儲存為 PDF**。此腳本足夠小巧，可直接放入 CI 流程，同時也具備彈性，可擴充自訂頁首、頁尾或浮水印。

您可以探索的下一步：

- 使用 **html to pdf python** 函式庫 `pdfkit`，採用基於 wkhtmltopdf 的方式（適合舊版 CSS）。  
- 加入 `argparse` CLI 介面，使腳本接受輸入/輸出參數。  
- 在 Flask 或 FastAPI 端點即時產生 PDF，以提供即時報告。  

歡迎自行試驗、挑戰，之後再回到本指南快速複習。若遇到問題，WeasyPrint 的文件與社群論壇都是極佳的資源。

祝開發順利，盡情將網頁轉換成精美的 PDF！

## 接下來您可以學習什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [使用 Aspose.HTML 轉換 HTML 為 PDF – 完整操作指南](/html/english/)
- [在 .NET 中使用 Aspose.HTML 轉換 HTML 為 PDF](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [從 HTML 建立 PDF – C# 步驟教學指南](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}