---
category: general
date: 2026-10-02
description: 學習如何在 Python 中建立 SVG 文件、將 SVG 儲存至檔案，並使用簡短完整的腳本匯出 SVG 圖像。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: zh-hant
lastmod: 2026-10-02
og_description: 使用 Python 建立 SVG 文件，並透過本實用教學匯出 SVG 圖像。跟隨腳本，將 SVG 儲存至檔案，即可立即重用向量圖形。
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: 在 Python 中建立 SVG 文件 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: 如何在 Python 中建立 SVG 文件並匯出為圖像
url: /zh-hant/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中建立 SVG 文件並匯出為影像

如果你需要以程式方式 **create SVG document**，本教學將會示範如何使用 Python 完成。你將看到一個完整的腳本，建立一個簡單的圓形、將 SVG 儲存至檔案，並產生可在任何地方嵌入的可匯出 SVG 影像。

從程式碼產生可縮放向量圖形，可省去在 GUI 編輯器中手動繪製形狀的工作。於本指南結束時，你可以將 SVG 建立整合至資料視覺化管線、自動化報告產生器，或任何需要清晰、解析度獨立圖形的專案中。

## 前置條件

在開始之前，請確保你已具備：

- 已安裝 Python 3.8 或更新版本
- `svgwrite` 函式庫（使用 `pip install svgwrite` 安裝）
- 對 SVG 將被儲存的目錄具有寫入權限

這些需求確保範例輕量且相容於大多數環境。

## 步驟 1：安裝並匯入 SVG 函式庫

第一步是加入提供便利 API 用於 SVG 建立的第三方函式庫。

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` 抽象化 SVG 檔案的 XML 結構，讓你專注於幾何形狀而非原始標記。

## 步驟 2：建立 SVG 文件物件

現在你可以透過實例化 `svgwrite.Drawing` 來 **create SVG document**。此物件代表根 `<svg>` 元素，並容納所有後續的形狀。

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

`size` 參數定義渲染的像素尺寸，而 `viewBox` 則建立與稍後定義的幾何相匹配的座標系統。

## 步驟 3：加入圓形元素

圓形由其中心 (`cx`, `cy`) 與半徑 (`r`) 定義。使用 `circle` 輔助函式來設定這些屬性。

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

此圓形位於 100 × 100 畫布的中央，四側留有 10 像素的邊距。可調整 `fill` 與 `stroke` 以符合你的設計語言。

## 步驟 4：將 SVG 儲存至檔案

圖形組合完成後，你可以使用 `save` 方法 **save SVG to file**。此操作會寫入符合規範的 XML，讓瀏覽器與向量編輯器皆能辨識。

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

`circle.svg` 檔案現在位於目前工作目錄。你可以在網頁瀏覽器、Inkscape 或任何支援 SVG 格式的工具中開啟它。

## 步驟 5：驗證匯出的 SVG 影像

在瀏覽器中開啟已儲存的檔案以確認輸出。你應該會看到一個置中的圓形，顏色如指定。原始 XML 如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

由於 SVG 為向量基礎，你可以在不失真的情況下縮放影像，這使其非常適合響應式網頁設計或高解析度列印。

## 小技巧：將 SVG 匯出為 PNG 或 JPEG

如果需要點陣圖版本，可將 SVG 檔案與轉換工具（例如 **CairoSVG**）結合使用：

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

此步驟示範 **export SVG image** 為點陣圖格式，當下游系統無法直接渲染 SVG 時相當有用。

## 常見變化與邊緣情況

| 變化 | 處理方式 |
|-----------|---------------|
| 多個形狀 | 對每個新元素（rect、line、path）呼叫 `dwg.add()`。 |
| 動態尺寸 | 在建立 `Drawing` 前，根據資料計算 `size` 與 `viewBox`。 |
| 文字標籤 | 使用 `dwg.text("Label", insert=("10", "20"))`，並以 `font_size` 與 `fill` 進行樣式設定。 |
| 重複使用文件 | 將 `Drawing` 物件保留於記憶體，並在需要更新檔案時呼叫 `save()`。 |
| 大型檔案 | 使用 `dwg.tostring()` 串流輸出，並手動寫入檔案物件，以避免記憶體激增。 |

處理這些情境可確保你的 **how to generate SVG** 腳本能從簡單圖示擴展至複雜圖表。

## 完整腳本回顧

以下是完整且可執行的範例，結合所有步驟與可選的轉換：

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

## 結論

你現在已了解如何在 Python 中 **create SVG document**、**save SVG to file**，以及 **export SVG image** 以供更廣泛的使用。此範例涵蓋了必要的 API 呼叫，說明每個步驟的重要性，並提供更複雜圖形的擴充方式。

接下來，可探索其他 **SVG Python tutorial** 主題，例如繪製路徑、套用漸層與動畫元素。整合這些技巧將讓你直接從 Python 應用程式產生動態、資料驅動的向量圖形。祝程式開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立於所示技巧之上。每個資源皆包含完整可運作的程式碼範例與逐步說明，協助你精通額外的 API 功能，並在自己的專案中探索替代實作方式。

- [在 Aspose.HTML for Java 中建立與管理 SVG 文件](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [在 Aspose.HTML for Java 中儲存 SVG 文件](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – 使用 Aspose.HTML for Java 將 SVG 轉換為影像](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}