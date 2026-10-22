---
category: general
date: 2026-10-21
description: 學習如何快速將 HTML 轉換為 PNG。本教程還涵蓋將網頁匯出為 PNG 以及使用 Python 將 HTML 檔案轉換為 PNG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: zh-hant
lastmod: 2026-10-21
og_description: 使用 Python 將 HTML 轉換為 PNG。跟隨此清晰指南，將網頁匯出為 PNG，處理特殊情況，並自動化圖像產生。
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: 將 HTML 轉換為 PNG（Python）– 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: 如何在 Python 中將 HTML 轉換為 PNG – 逐步指南
url: /zh-hant/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 將 HTML 轉換為 PNG – 完整程式指南

如果你需要 **將 HTML 轉換為 PNG**，本指南會示範如何使用純 Python 以可靠的方式完成。無論是匯出靜態報告、為相簿產生縮圖，或是自動化測試截圖，你都能在幾分鐘內得到完整、可直接執行的解決方案。

你還會看到如何 **匯出網頁為 PNG**、了解將 HTML 檔案與即時 URL 轉換的差異，並學習處理大型頁面或動態內容的最佳實踐。全程不需要外部服務——只要幾個 Python 套件與一段簡短腳本即可。

## 前置條件

在開始之前，請確保你已具備：

- 已安裝 Python 3.9+（此程式碼在 Windows、macOS 與 Linux 都可執行）
- 可使用終端機或命令提示字元
- 具備 Python 套件管理工具 (`pip`) 的基本認識

你需要安裝 `imgkit` 套件（`wkhtmltoimage` 的薄層封裝）以及 `wkhtmltoimage` 本身的執行檔。兩者皆為免費開源軟體。

## 步驟 1：安裝必要工具

第一步是安裝 `wkhtmltoimage` 與與之溝通的 Python 包裝器。

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **為什麼這一步很重要** – `wkhtmltoimage` 以 WebKit 引擎渲染 HTML，產生像素完美的 PNG。`imgkit` 只會把你的選項直接傳給執行檔，讓你得到與瀏覽器相同的品質。

## 步驟 2：驗證安裝

執行簡短檢查，確認 Python 能找到該執行檔。

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

如果腳本印出 `wkhtmltoimage` 的路徑，代表已可開始將 HTML 轉換為 PNG。若出現 `OSError`，請再次確認執行檔已加入系統 `PATH`。

## 步驟 3：撰寫可重用的轉換函式

將邏輯封裝在函式中，可讓你在專案任何地方輕鬆 **將 HTML 檔案轉換為 PNG** 或 **匯出網頁為 PNG**。

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **為什麼同時包裝 `from_file` 與 `from_url`** – 同一個函式現在同時支援 **如何將 HTML 轉換為圖片** 的本機檔案與即時網頁，讓程式碼保持 DRY（Don’t Repeat Yourself）原則。

## 步驟 4：將本機 HTML 檔案轉換為 PNG

在名為 `assets` 的資料夾內放入 `sample.html`，然後呼叫剛才定義的輔助函式：

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### 預期輸出

執行腳本後會印出：

```
✅ Successfully saved PNG to: output/sample.png
```

此時會在 `output/sample.png` 產生一個像素完美的 `sample.html` 快照。用任何圖像檢視器開啟，都會看到與瀏覽器中完全相同的渲染結果。

## 步驟 5：匯出即時網頁為 PNG

若需要 **匯出網頁為 PNG**（例如頻繁變動的儀表板），只要傳入 URL 字串取代檔案路徑即可。

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### 為什麼要調整視口大小？

桌面版網頁在窄幅渲染時常會顯得擁擠。透過增大 `width` 與 `height` 參數，你可以捕捉完整版面，這在 **匯出網頁為 PNG** 任務中特別有用。

## 步驟 6：處理常見邊緣情況

### 6.1 大型頁面或無限捲動

對於使用懶載入（例如無限捲動）的頁面，可延長 JavaScript 延遲時間，並視需要設定更大的視口：

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 需要驗證的保護頁面

若頁面需要 session cookie，可在請求中加入 cookie 標頭：

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 缺少圖片或字型

`wkhtmltoimage` 為安全起見會預設啟用 `--disable-local-file-access`。如果你的 HTML 參照本機資源，必須明確允許：

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## 步驟 7：以程式方式驗證結果（可選）

有時需要在 CI 流程中確認 PNG 是否正確產生。以下程式碼會檢查檔案大小與尺寸：

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

只要 PNG 通過這些檢查，即可安全用於後續流程，如 PDF 產生、電子郵件附件或機器學習管線。

## 結論

現在你已掌握使用 Python **將 HTML 轉換為 PNG** 的完整、可投入生產的方式。本指南涵蓋：

- 安裝 `wkhtmltoimage` 與 `imgkit`
- 驗證執行環境
- 可重用的 `convert_html_to_png` 函式，支援本機檔案與 URL
- 真實案例：**匯出網頁為 PNG**、**如何將 HTML 轉換為圖片**、**將 HTML 檔案轉換為 PNG**
- 大型頁面、驗證需求與本機資源的邊緣情況處理
- CI/CD 流程的可選驗證步驟

歡迎自行嘗試 `imgkit` 的其他參數，例如 `zoom`、`crop-h` 或 `crop-w`，以微調輸出符合你的特定需求。接下來，你可以探索：

- 使用 `img2pdf` 套件將 PNG 轉為 PDF 報告
- 批次轉換整個資料夾的 HTML 檔案
- 針對需要完整瀏覽器渲染的頁面（例如大型 JavaScript 框架）改用 Selenium

祝開發順利，享受像素完美的截圖吧！


## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步延伸所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，助你掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [將 HTML 轉換為 PNG – 完整 Python 教程](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [在 Python 中將 HTML 轉換為 PNG – 完整串流儲存指南](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [使用 Aspose.HTML 在 Python 中將 SVG 轉換為 PNG](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}