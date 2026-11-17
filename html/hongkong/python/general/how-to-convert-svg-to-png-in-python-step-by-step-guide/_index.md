---
category: general
date: 2026-11-17
description: 將 SVG 轉換為 PNG，只需幾行 Python 程式碼。學習如何將 SVG 儲存為 PNG，並可使用可選的轉換設定。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert svg to png
- save svg as png
- export svg as png
- svg to raster image
- how to convert svg to png
language: zh-hant
lastmod: 2026-11-17
og_description: 在 Python 中使用簡潔範例將 SVG 轉換為 PNG。按照步驟高效匯出 SVG 為 PNG。
og_image_alt: Diagram illustrating convert svg to png workflow in Python
og_title: 在 Python 中將 SVG 轉換為 PNG – 快速指南
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: convert svg to png using Python in a few lines. Learn to save SVG as
    PNG with optional conversion settings.
  headline: How to convert SVG to PNG in Python – step‑by‑step guide
  type: TechArticle
tags:
- svg
- png
- python
- image conversion
title: 如何在 Python 中將 SVG 轉換為 PNG – 步驟指南
url: /zh-hant/python/general/how-to-convert-svg-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中將 SVG 轉換為 PNG – 步驟說明指南

如果你需要 **convert svg to png**，本指南提供一個完整的解決方案，讓你今天就能執行。你還會看到如何 **save svg as png**，並可自行設定尺寸與背景顏色。

將向量 SVG 檔案產生點陣圖是常見需求，無論是為瀏覽器提供圖形、建立縮圖，或是嵌入 PDF 中。本教學涵蓋從安裝所需套件到處理缺少檔案或超大型 SVG 等邊緣情況的全部步驟。

## 前置條件

開始之前，請確保你已具備：

* Python 3.8 或更新版本。
* 可使用的終端機或命令提示字元。
* `cairosvg` 套件，負責 **svg to raster image** 轉換的主要工作。

你可以使用以下單一 pip 指令安裝套件：

```bash
pip install cairosvg
```

> **小技巧：** 使用虛擬環境 (virtual environment) 以將相依套件與其他專案隔離。

## 如何在 Python 中將 SVG 轉換為 PNG

此流程的核心包含三個動作：載入 SVG、（可選）調整轉換參數，最後寫入 PNG 檔案。以下程式碼在可重用的函式中實作了這三個步驟。

```python
import cairosvg
from pathlib import Path

def convert_svg_to_png(svg_path: str, png_path: str) -> None:
    """
    Convert an SVG file to a PNG raster image.

    Parameters
    ----------
    svg_path : str
        Path to the source SVG file.
    png_path : str
        Destination path for the generated PNG file.
    """
    # Verify that the SVG file exists
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    # Perform the conversion using default settings
    cairosvg.svg2png(url=svg_path, write_to=png_path)

# Example usage
if __name__ == "__main__":
    svg_file = "YOUR_DIRECTORY/image.svg"
    png_file = "YOUR_DIRECTORY/image.png"
    convert_svg_to_png(svg_file, png_file)
    print(f"Converted {svg_file} to {png_file}")
```

### 為什麼這樣可行

* `cairosvg.svg2png` 會讀取 SVG 檔案 (`url=svg_path`) 並寫入 PNG 檔案 (`write_to=png_path`)。  
* 若找不到來源 SVG，函式會拋出明確的錯誤，協助你提前偵測路徑問題。  
* 將轉換邏輯封裝在函式內，可輕鬆在多個腳本或大型應用程式中重複使用。

## 可選：微調轉換參數

如果你需要特定的輸出尺寸或不同的背景色，`cairosvg.svg2png` 接受額外參數。以下範例將寬度設定為 300 px，背景設為白色。

```python
def convert_svg_to_png_custom(svg_path: str, png_path: str,
                              width: int = 300,
                              background_color: str = "white") -> None:
    """
    Convert an SVG to PNG with custom dimensions and background.

    Parameters
    ----------
    width : int
        Desired width of the PNG in pixels; height scales proportionally.
    background_color : str
        Hex or named color for the PNG background.
    """
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    cairosvg.svg2png(
        url=svg_path,
        write_to=png_path,
        output_width=width,
        background_color=background_color
    )
```

呼叫此函式的方式與基本版相同，只要傳入你想要的寬度或顏色即可。

## 常見問題與邊緣情況

**如果 SVG 包含外部字型該怎麼辦？**  
`cairosvg` 會自動嵌入引用的字型，但字型檔必須能從 SVG 所在位置被存取。請將字型檔放在 SVG 同目錄，或使用絕對 URL。

**如何處理非常大的 SVG？**  
大型檔案可能佔用大量記憶體。你可以改為串流 SVG 內容，而不是一次讀入磁碟：

```python
with open(svg_path, "rb") as svg_stream:
    cairosvg.svg2png(file_obj=svg_stream, write_to=png_path)
```

**可以一次批次轉換多個檔案嗎？**  
將轉換呼叫包在迴圈中，並使用 `Path.glob("*.svg")` 來搜尋目錄下的所有 SVG。

## 預期輸出

執行範例腳本時會印出一行文字，確認轉換已完成：

```
Converted YOUR_DIRECTORY/image.svg to YOUR_DIRECTORY/image.png
```

產生的 `image.png` 會存於相同目錄，且可使用任何圖像檢視器開啟。

## 結論

現在你已了解如何在 Python 中 **convert svg to png**、如何 **save svg as png**，以及如何使用自訂尺寸 **export svg as png**。相同的做法適用於任何 SVG 檔，將向量圖形轉換為適合網頁、報告或縮圖的 **svg to raster image** 格式。

接下來可以考慮：

* 探索 `export svg as png` 的 DPI 參數控制。
* 將轉換函式整合至 Flask 或 Django 端點，提供即時影像產生服務。
* 使用次要關鍵字 **how to convert svg to png** 搜尋更進階的使用情境，例如批次處理或 CI/CD 流程。

歡迎自行嘗試不同設定，並與社群分享你的成果！

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，能在此基礎上延伸更多 API 功能與實作方式，每篇皆提供完整可執行的程式碼範例與逐步說明，協助你在專案中靈活運用。

- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)
- [Convert SVG to PNG in Python – Complete Step‑by‑Step Guide](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}