---
category: general
date: 2026-07-05
description: 在 Python 中建立 SVG 文件，並學習如何快速將 SVG 轉換為 PNG。包括保存 SVG 檔案的步驟以及匯出 SVG 為 PNG。
draft: false
keywords:
- create SVG document
- convert SVG to PNG
- SVG to PNG Python
- save SVG file
- export SVG as PNG
language: zh-hant
og_description: 於 Python 中建立 SVG 文件，並即時轉換為 PNG。請跟隨此一步一步的教學，將 SVG 檔案儲存並匯出為 PNG。
og_title: 在 Python 中建立 SVG 文件 – 將 SVG 轉換為 PNG
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create SVG document in Python and learn how to convert SVG to PNG quickly.
    Includes save SVG file steps and export SVG as PNG.
  headline: Create SVG Document in Python – Convert SVG to PNG Guide
  type: TechArticle
tags:
- Python
- Aspose.HTML
- Image Conversion
title: 在 Python 中建立 SVG 檔案 – SVG 轉 PNG 教學
url: /zh-hant/python/general/create-svg-document-in-python-convert-svg-to-png-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中建立 SVG 文件 – SVG 轉 PNG 指南

是否曾經需要在 Python 中 **create SVG document**，卻不知從何開始？你並非唯一有此困惑的開發者——大家常問：「如何在不使用外部工具的情況下，將向量圖轉換成 PNG？」好消息是，使用 Aspose.HTML for Python，你可以快速建立 SVG，**save SVG file**，以及 **export SVG as PNG**，只需幾行程式碼。

在本教學中，我們將逐步說明完整流程：安裝套件、建立簡易 SVG、將其寫入磁碟，最後使用 **convert SVG to PNG** 功能。完成後，你將擁有一個可重複使用的腳本，能直接套用於任何專案——無論是產生圖表、圖示，或即時動態圖形。

## 前置條件 – 開始前你需要的項目

- Python 3.8 或更新版本（程式碼亦支援 3.9‑3.11）  
- 可透過 pip 安裝的 **aspose.html**（免費試用版適用於大多數使用情境）  
- 具備寫入 SVG 與 PNG 所在資料夾的權限  

如果你已經有虛擬環境，太好了——立即啟動它。否則，請建立一個：

```bash
python -m venv venv
source venv/bin/activate   # on Windows use `venv\Scripts\activate`
```

接著安裝 Aspose.HTML 套件：

```bash
pip install aspose-html
```

> **專業提示：** `aspose-html` wheel 會自動包含所有原生二進位檔案，無需額外安裝系統函式庫。

## 步驟 1：在 Python 中建立 SVG 文件

我們首先使用 `SVGDocument` 類別 **create SVG document**。可以將此物件視為一張空白畫布，能在上面加入任何有效的 SVG 標記。

```python
from aspose.html import SVGDocument

# Initialize a new, empty SVG document
svg = SVGDocument()

# Append a simple green circle as raw SVG markup
svg.root.append_child("<circle cx='50' cy='50' r='40' fill='green'/>")
```

為什麼要使用字串搭配 `append_child`？它允許你直接將原始 SVG 片段插入 DOM，對於快速原型或從其他來源（例如 API）產生標記時相當便利。`root` 屬性指向 `<svg>` 元素，等同於說「在 SVG 內加入此子節點」。

## 步驟 2：儲存 SVG 檔案（可選但很實用）

在轉換之前，你可能想 **save SVG file** 以檢視輸出或交給設計師。此步驟為可選，但對除錯非常有幫助。

```python
# Choose a folder you have write access to
output_dir = "output"
import os
os.makedirs(output_dir, exist_ok=True)

# Persist the SVG to disk
svg_path = os.path.join(output_dir, "circle.svg")
svg.save(svg_path)
print(f"SVG saved to {svg_path}")
```

執行此程式碼會產生如下檔案：

```xml
<?xml version="1.0" encoding="utf-8"?>
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <circle cx="50" cy="50" r="40" fill="green"/>
</svg>
```

在瀏覽器中開啟它，你會看到位於 100 × 100 viewbox 中心的清晰綠色圓形。若形狀不是預期的樣子，請調整標記後重新執行腳本。這種反覆迭代的流程說明了 **saving the SVG file** 為驗證向量邏輯最快的方法。

## 步驟 3：設定 PNG 轉換選項

現在進入有趣的部分：將向量轉為點陣圖。`PNGSaveOptions` 類別讓你微調輸出——解析度、背景色、壓縮等級等。大多數情況下預設值已足夠，但我們仍設定自訂寬度與高度，以示範 API 用法。

```python
from aspose.html import PNGSaveOptions

png_options = PNGSaveOptions()
png_options.width = 200   # pixels
png_options.height = 200  # pixels
# Optional: set a transparent background
png_options.background_color = None
```

`width` 與 `height` 屬性控制點陣圖尺寸，與 SVG 本身的內在尺寸無關。當需要從同一 SVG 產生縮圖或高解析度列印時，這非常方便。

## 步驟 4：將 SVG 轉為 PNG – 一行程式碼的魔法

文件已備妥且選項設定完成後，實際的 **convert SVG to PNG** 呼叫只需一行程式碼。`Converter.convert_svg` 方法在底層負責解析、點陣化以及寫入檔案。

```python
from aspose.html import Converter

png_path = os.path.join(output_dir, "circle.png")
Converter.convert_svg(svg, png_options, png_path)
print(f"PNG exported to {png_path}")
```

開啟 `circle.png` 後，你會看到 200 × 200 像素的綠色圓形，具備完美的抗鋸齒效果。轉換保留了 SVG 的向量特性，放大時不會產生模糊——這是單純位圖轉位圖無法保證的。

### 預期輸出

| File | Description |
|------|-------------|
| `circle.svg` | 以文字形式呈現的 SVG，包含單一 `<circle>` 元素。 |
| `circle.png` | 200 × 200 PNG，綠色圓形位於透明背景上。 |

若比較兩者，當以相同尺寸呈現時 PNG 與 SVG 看起來相同，但你現在擁有可攜帶的點陣格式，適用於僅接受 PNG 的 API（例如電子郵件附件、舊版報表工具）。

## 步驟 5：封裝成可重複使用的函式

大多數實務專案不會只轉換單一硬編碼圖形。讓我們將邏輯封裝成接受任意 SVG 標記並回傳 PNG 路徑的函式。這展示了 **export SVG as PNG** 的乾淨且可重用的做法。

```python
def svg_to_png(svg_markup: str, png_path: str, width: int = 200, height: int = 200) -> None:
    """
    Converts a string containing SVG markup into a PNG file.

    Parameters
    ----------
    svg_markup : str
        Raw SVG XML to be rendered.
    png_path : str
        Destination file path for the PNG image.
    width, height : int, optional
        Desired dimensions of the output PNG (default 200×200).
    """
    # Create the SVG document and inject markup
    doc = SVGDocument()
    doc.root.append_child(svg_markup)

    # Prepare PNG options
    opts = PNGSaveOptions()
    opts.width = width
    opts.height = height
    opts.background_color = None

    # Perform the conversion
    Converter.convert_svg(doc, opts, png_path)

# Example usage
example_svg = "<rect x='10' y='10' width='80' height='80' fill='orange'/>"
svg_to_png(example_svg, os.path.join(output_dir, "rect.png"))
print("Custom rectangle PNG created.")
```

使用任意有效的 SVG 字串呼叫此函式，即可 **create SVG document**、**save SVG file**（若在函式內加入 `doc.save`）以及 **export SVG as PNG**，一次完成。可自行調整 `width`、`height`，或加入背景色以符合專案品牌需求。

## 常見問題與邊緣案例

| Question | Answer |
|----------|--------|
| *這在 Linux/macOS 上能運作嗎？* | 絕對可以——Aspose.HTML 支援跨平台。只要確保為你的作業系統下載正確的 wheel（`manylinux` wheel 已涵蓋大多數 Linux 發行版）。 |
| *如果 SVG 參考外部字型呢？* | 轉換器會自動嵌入系統字型。若使用自訂字型，請將 `.ttf`/`.otf` 檔案放在同一資料夾，並在 SVG 內以 `<style>` 區塊引用它們。 |
| *我可以批次轉換多個 SVG 嗎？* | 可以——遍歷 SVG 字串或檔案路徑清單，對每個呼叫 `svg_to_png`。此函式庫是執行緒安全的，甚至可使用 `concurrent.futures` 進行平行處理。 |
| *如何控制 PNG 壓縮？* | `PNGSaveOptions` 提供 `compression_level` 屬性（0‑9）。較低的數值會產生較大檔案但寫入速度較快；較高的數值則可減小檔案大小，但會增加 CPU 時間。 |
| *有沒有辦法保留原始 SVG 的 viewbox？* | 在 `PNGSaveOptions` 中省略 `width`/`height` 設定。轉換器將使用 SVG 本身的內在尺寸。 |

## 結論

我們已完整說明如何在 Python 中 **create SVG document**、**save SVG file**，以及使用 Aspose.HTML **convert SVG to PNG**。一步步的說明展示了每個環節的重要性，從初始化 DOM 到微調點陣選項，最後提供可重複使用的輔助函式，讓你只需一次呼叫即可 **export SVG as PNG**。

接下來，你可以探索更進階的功能，例如加入文字層、嵌入影像，或從 SVG 產生多頁 PDF。也可參考其他相關關鍵字——**SVG to PNG Python** 教學常會探討效能基準測試，而 **convert SVG to PNG** 指南則可能比較 CairoSVG、Pillow 等替代函式庫。

遇到奇怪的 SVG 無法處理嗎？留下評論，我們一起來排除問題。祝開發愉快，盡情將向量轉換成清晰的 PNG！

![顯示建立 SVG 文件工作流程的圖示](https://example.com/images/svg-to-png-workflow.png "顯示建立 SVG 文件工作流程的圖示")

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在此處示範的技巧之上。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索替代實作方式。

- [在 Aspose.HTML for Java 中儲存 SVG 文件](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – 使用 Aspose.HTML for Java 將 SVG 轉為影像](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [在 .NET 中使用 Aspose.HTML 將 SVG 文件渲染為 PNG](/html/english/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}