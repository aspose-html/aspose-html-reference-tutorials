---
category: general
date: 2026-10-28
description: 學習如何在 Python 中光柵化 SVG，並使用 CairoSVG 的簡單腳本將 SVG 轉換為 PNG。只需幾秒鐘即可將 SVG 儲存為
  PNG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rasterize svg
- convert svg to png
- save svg as png
- svg to png python
- export svg as png
language: zh-hant
lastmod: 2026-10-28
og_description: 如何在 Python 中將 SVG 點陣化：本指南將示範如何使用 CairoSVG 將 SVG 轉換為 PNG，涵蓋安裝、程式碼與故障排除。
og_image_alt: Screenshot of Python code that rasterizes SVG to PNG
og_title: 如何在 Python 中將 SVG 點陣化 – 快速 SVG 轉 PNG 指南
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  headline: How to rasterize SVG in Python – convert SVG to PNG easily
  type: TechArticle
- description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  name: How to rasterize SVG in Python – convert SVG to PNG easily
  steps:
  - name: Why CairoSVG?
    text: '- **Pure Python**: No need for external command‑line tools once the package
      is installed. - **SVG‑compliant**: Supports most SVG 1.1 features, including
      gradients, masks, and text. - **Flexible output**: Besides PNG, you can export
      to PDF, PS, or even raw bytes.'
  - name: Step‑by‑step breakdown
    text: 1. **Install the library** – `pip install cairosvg` pulls in the compiled
      Cairo bindings. 2. **Import the module** – `import cairosvg` gives you access
      to the `svg2png` helper. 3. **Call `svg2png`** – Pass the SVG file path (or
      a URL) and the destination PNG path. Optional `output_width`, `output_he
  - name: Edge cases you might encounter
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | **Large SVG (megapixel dimensions)** | Increase `dpi` or set explicit `output_width`/`output_height`
      to avoid memory spikes. | | **Missing fonts** | Install the required fonts on
      the system or em'
  type: HowTo
tags:
- svg
- python
- image processing
- cairosvg
title: 如何在 Python 中點陣化 SVG – 輕鬆將 SVG 轉換為 PNG
url: /zh-hant/python/general/how-to-rasterize-svg-in-python-convert-svg-to-png-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中光柵化 SVG – 輕鬆將 SVG 轉換為 PNG

如果你需要在網頁應用、報告或自動化建置中 **how to rasterize svg**，本指南提供即時可執行的解決方案。你將看到只需幾行 Python 就能 **convert svg to png**，且產生的 PNG 清晰銳利，可立即儲存或提供服務。

本教學涵蓋從安裝所需函式庫到處理大型檔案或自訂 DPI 設定等邊緣情況的全部步驟。完成後，你將能夠 **save svg as png**、**export svg as png**，並將此流程整合至任何 Python 工作流程中。

## 需求環境

- Python 3.8+（此程式碼在 3.9、3.10 及更新版本皆可執行）
- 使用 `pip` 安裝套件
- 本機 SVG 檔案（例如 `logo.svg`），即欲光柵化的檔案
- （可選）使用虛擬環境以便乾淨管理相依性

> **小技巧：** 使用虛擬環境（`python -m venv .venv`）可將 CairoSVG 相依性與全域 Python 套件分離。

## 如何在 Python 中光柵化 SVG

最直接的 **how to rasterize svg** 方法是使用 **CairoSVG** 函式庫。CairoSVG 會讀取 SVG XML，利用 Cairo 圖形引擎渲染，並將光柵圖像寫入 PNG、PDF 或其他點陣格式。

```bash
# Install CairoSVG and its binary dependencies
pip install cairosvg
```

```python
# rasterize_svg.py
import sys
from pathlib import Path
import cairosvg

def rasterize_svg(input_path: str, output_path: str,
                  width: int | None = None,
                  height: int | None = None,
                  dpi: int = 96) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the PNG file.
    width : int | None
        Desired output width in pixels (maintains aspect ratio if height is None).
    height : int | None
        Desired output height in pixels (maintains aspect ratio if width is None).
    dpi : int
        Dots per inch for the rasterization. Higher DPI yields larger files but more detail.
    """
    try:
        # CairoSVG can read from a file path directly
        cairosvg.svg2png(url=Path(input_path).as_uri(),
                         write_to=output_path,
                         output_width=width,
                         output_height=height,
                         dpi=dpi)
        print(f"✅ Successfully saved PNG to {output_path}")
    except Exception as e:
        print(f"❌ Failed to rasterize {input_path}: {e}", file=sys.stderr)
        raise

if __name__ == "__main__":
    # Example usage:
    # python rasterize_svg.py ./assets/logo.svg ./output/logo.png 300 300
    if len(sys.argv) < 3:
        print("Usage: python rasterize_svg.py <input_svg> <output_png> [width] [height] [dpi]")
        sys.exit(1)

    input_svg = sys.argv[1]
    output_png = sys.argv[2]
    w = int(sys.argv[3]) if len(sys.argv) > 3 else None
    h = int(sys.argv[4]) if len(sys.argv) > 4 else None
    d = int(sys.argv[5]) if len(sys.argv) > 5 else 96

    rasterize_svg(input_svg, output_png, width=w, height=h, dpi=d)
```

### 為什麼選擇 CairoSVG？

- **Pure Python**：安裝套件後無需外部指令列工具。
- **SVG‑compliant**：支援大多數 SVG 1.1 功能，包括漸層、遮罩與文字。
- **Flexible output**：除了 PNG，亦可匯出為 PDF、PS，甚至原始位元組。

### 步驟說明

1. **安裝函式庫** – `pip install cairosvg` 會下載已編譯的 Cairo 綁定。  
2. **匯入模組** – `import cairosvg` 讓你可以使用 `svg2png` 輔助函式。  
3. **呼叫 `svg2png`** – 傳入 SVG 檔案路徑（或 URL）以及目標 PNG 路徑。可選的 `output_width`、`output_height` 與 `dpi` 參數可控制尺寸與解析度。  
4. **處理錯誤** – `try/except` 區塊會在 SVG 格式錯誤或輸出目錄不可寫入時顯示清晰訊息。

## 使用 CairoSVG 轉換 SVG 為 PNG

如果只需要一行程式碼快速轉換，以下程式碼片段即可在不使用封裝函式的情況下完成任務：

```python
import cairosvg

cairosvg.svg2png(url="logo.svg", write_to="logo.png")
```

這是最簡潔的 **convert svg to png** 示範。它會從目前目錄讀取 `logo.svg`，並在同一目錄產生 `logo.png`。

## 儲存 SVG 為 PNG – 驗證結果

執行腳本後，你應該會在目標路徑看到 PNG 檔案。使用任何影像檢視器開啟以確認：

```bash
# Linux/macOS
xdg-open ./output/logo.png   # or open on macOS
# Windows
start ./output/logo.png
```

若 PNG 看起來模糊，可提升 `dpi` 參數（例如 `dpi=300`）以產生更高解析度的光柵圖像。

## 以不同格式匯出 SVG 為 PNG

CairoSVG 也能輸出 **PDF**、**PostScript** 或原始 **PNG bytes**。以下示範在需要將影像保留於記憶體中（例如 Flask 回應）時，如何匯出至 `BytesIO` 物件：

```python
import io
import cairosvg

svg_path = "logo.svg"
png_bytes = io.BytesIO()
cairosvg.svg2png(url=Path(svg_path).as_uri(), write_to=png_bytes)
png_bytes.seek(0)  # Ready for sending over HTTP
```

### 可能遇到的邊緣情況

| 情況 | 建議處理方式 |
|------|--------------|
| **大型 SVG（百萬像素尺寸）** | 提升 `dpi` 或設定明確的 `output_width`/`output_height` 以避免記憶體激增。 |
| **缺少字型** | 在系統上安裝所需字型，或使用 `<style>` 標籤將字型嵌入 SVG 中。 |
| **透明度問題** | PNG 預設保留 alpha；若需實心背景，可在 `svg2png` 中傳入 `background_color="#FFFFFF"`。 |
| **批次處理** | 迭代 SVG 目錄，對每個檔案呼叫 `rasterize_svg`。 |

## 完整可執行範例

以下是一個最小且獨立的腳本，你可以直接複製貼上為 `svg_to_png.py`，然後立即執行。

```python
# svg_to_png.py
import cairosvg
from pathlib import Path

def main():
    src = Path("example.svg")
    dst = Path("example.png")
    if not src.is_file():
        raise FileNotFoundError(f"Source SVG not found: {src}")

    # Convert with default DPI (96) and keep original dimensions
    cairosvg.svg2png(url=src.as_uri(), write_to=dst)
    print(f"✅ {src.name} → {dst.name} created successfully.")

if __name__ == "__main__":
    main()
```

Running `python svg_to_png


## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與步驟說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何在 Python 中光柵化 SVG – 完整指南](/html/english/python/general/how-to-rasterize-svg-in-python-complete-guide/)
- [在 Python 中將 SVG 轉換為 PNG – 高解析度匯出指南](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [在 Python 中建立 SVG 文件 – SVG 轉 PNG 指南](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}