---
category: general
date: 2026-09-29
description: 如何使用 Python 儲存 SVG 並匯出 SVG 為 PNG。學會在數分鐘內使用精細調整的選項將 SVG 轉換為 PNG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: zh-hant
lastmod: 2026-09-29
og_description: 如何使用 Python 儲存 SVG 並將 SVG 匯出為 PNG。跟隨本指南，全面掌控選項將 SVG 轉換為 PNG。
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: 如何使用 Python 將 SVG 另存為 PNG – 步驟說明
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  headline: How to save SVG as PNG with Python – complete guide
  type: TechArticle
- description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  name: How to save SVG as PNG with Python – complete guide
  steps:
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: (Optional) Create image‑save options
    text: '```python from aspose.svg import ImageSaveOptions'
  - name: Save the SVG as PNG
    text: '```python # Export the SVG to a PNG file using the options defined above
      svg_doc.save("YOUR_DIRECTORY/vector.png", options) ```'
  - name: Full script
    text: 'Putting the pieces together yields a complete, runnable program:'
  - name: Missing file or invalid path
    text: 'If `src_path` does not exist, `SVGDocument` raises a `FileNotFoundError`.
      Wrap the call in a `try/except` block to provide a friendly error message:'
  - name: Preserving aspect ratio
    text: When only one dimension (width **or** height) is set, the library automatically
      scales the other dimension to maintain the original aspect ratio. If you set
      both dimensions, the image may stretch. Choose the approach that matches your
      UI requirements.
  - name: Transparent backgrounds
    text: 'If the original SVG relies on transparency (e.g., icons), you can keep
      the PNG transparent by omitting `background_color`:'
  type: HowTo
tags:
- Python
- SVG
- Image conversion
title: 如何使用 Python 將 SVG 另存為 PNG – 完整指南
url: /zh-hant/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 將 SVG 儲存為 PNG – 完整指南

如果你需要 **how to save SVG** 為點陣圖，這篇教學會提供一個即時可執行的解決方案。你將學會如何載入向量 SVG 檔案、可選地調整影像儲存設定，並僅用三行程式碼將結果匯出為 PNG。

將 SVG 檔案儲存為 PNG 在想要於網頁嵌入圖形、產生縮圖，或將點陣圖供機器學習流程使用時相當常見。此方法在 Windows、macOS 與 Linux 上皆可運作，且不需額外的原生相依性。

## 前置條件

在開始之前，請確保你已具備：

* Python 3.9 或更新版本已安裝
* `aspose.svg` 套件（官方的 Aspose SVG for Python via .NET）。使用以下指令安裝：

```bash
pip install aspose-svg
```

* 磁碟上有效的 SVG 檔案（例如 `vector.svg`）

這些需求讓範例保持自給自足，並避免使用外部工具，例如 CairoSVG。

## 如何使用 Python 儲存 SVG

此流程的核心分為三個步驟：載入、設定與儲存。以下各節將逐一說明每個步驟。

### 步驟 1：載入 SVG 文件

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

`SVGDocument` 會解析 SVG XML 並建立記憶體中的表示。必須先載入檔案；否則儲存操作將沒有來源資料。

### 步驟 2：（可選）建立影像儲存選項

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

`ImageSaveOptions` 讓你微調 PNG 輸出。調整寬度與高度會保留長寬比，除非你同時明確設定兩者。設定背景顏色在原始 SVG 含有透明度但你需要不透明 PNG 時相當有用。

### 步驟 3：將 SVG 儲存為 PNG

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

`save` 方法會將 PNG 檔寫入目標路徑。若省略 `options` 參數，函式庫會使用從 SVG 的 viewBox 推算出的預設尺寸。

### 完整腳本

將上述片段組合起來即可得到完整、可執行的程式：

```python
# -*- coding: utf-8 -*-
"""
How to save SVG as PNG with Python.
This script loads an SVG file, applies optional image‑save settings,
and exports the result to PNG.
"""

from aspose.svg import SVGDocument, ImageSaveOptions

def convert_svg_to_png(
    src_path: str,
    dst_path: str,
    width: int = 800,
    height: int = 600,
    background: str = "#FFFFFF"
) -> None:
    """Convert an SVG file to PNG with custom dimensions and background."""
    # Load the SVG document
    svg_doc = SVGDocument(src_path)

    # Prepare save options
    options = ImageSaveOptions()
    options.width = width
    options.height = height
    options.background_color = background

    # Save as PNG
    svg_doc.save(dst_path, options)


if __name__ == "__main__":
    # Example usage
    convert_svg_to_png(
        src_path="YOUR_DIRECTORY/vector.svg",
        dst_path="YOUR_DIRECTORY/vector.png",
        width=1024,
        height=768,
        background="#FFFFFF"
    )
    print("SVG successfully saved as PNG.")
```

執行腳本後會印出 **“SVG successfully saved as PNG.”**，並在同一資料夾產生 `vector.png`。

## 轉換 SVG 為 PNG – 處理常見陷阱

### 檔案遺失或路徑無效

若 `src_path` 不存在，`SVGDocument` 會拋出 `FileNotFoundError`。將呼叫包在 `try/except` 區塊中，以提供友善的錯誤訊息：

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### 保持長寬比

當只設定單一尺寸（寬度 **或** 高度）時，函式庫會自動縮放另一個尺寸以維持原始長寬比。若同時設定兩個尺寸，影像可能會被拉伸。請依照你的 UI 需求選擇適合的做法。

### 透明背景

若原始 SVG 依賴透明度（例如圖示），可透過省略 `background_color` 讓 PNG 保持透明：

```python
options.background_color = None   # PNG will retain transparency
```

此變化在 PNG 需要疊加於其他圖形上時相當有用。

## 匯出 SVG 為 PNG – 效能小技巧

* **重複使用 `ImageSaveOptions`** 在批次轉換多個檔案時。為每個檔案建立新的選項物件開銷極小，但重複使用可避免重複的記憶體配置。
* **批次處理**：遍歷 SVG 檔案目錄，對每個檔案呼叫 `convert_svg_to_png`。函式庫會獨立處理每個檔案，因此可使用 `concurrent.futures.ThreadPoolExecutor` 於多核心機器上平行執行迴圈，以加速轉換。

```python
import os
from concurrent.futures import ThreadPoolExecutor

svg_folder = "YOUR_DIRECTORY"
png_folder = "YOUR_DIRECTORY/pngs"
os.makedirs(png_folder, exist_ok=True)

def batch_convert(file_name):
    src = os.path.join(svg_folder, file_name)
    dst = os.path.join(png_folder, file_name.replace('.svg', '.png'))
    convert_svg_to_png(src, dst)

with ThreadPoolExecutor(max_workers=8) as executor:
    executor.map(batch_convert, [f for f in os.listdir(svg_folder) if f.endswith('.svg')])
```

## 儲存 SVG 為 PNG – 驗證

轉換完成後，你可以以程式方式驗證輸出：

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

典型輸出：

```
PNG size: (1024, 768), mode: RGBA
```

`mode` 為 `RGBA` 表示影像包含 alpha 通道（透明度）。若設定背景顏色，模式則會是 `RGB`。

## 結論

現在你已了解如何使用 Python **how to save SVG** 為 PNG、如何 **convert SVG to PNG**，以及如何以自訂尺寸與背景處理 **export SVG to PNG**。完整腳本示範了從載入向量 SVG 檔案到產生點陣 PNG 圖像的完整工作流程。

接下來，可探索相關主題，例如批次模式下的 **save SVG as PNG**、使用替代函式庫如 **CairoSVG**，或從 SVG 來源產生多頁 PDF。嘗試不同的 `ImageSaveOptions` 設定，以微調品質、DPI 與壓縮，符合你的特定使用情境。

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在本篇示範的技術之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [svg to png java – 使用 Aspose.HTML for Java 轉換 SVG 為影像](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [使用 Aspose.HTML 在 .NET 中將 SVG 文件呈現為 PNG](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [使用 Java 轉換 SVG 為 PNG 時如何設定 DPI](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}