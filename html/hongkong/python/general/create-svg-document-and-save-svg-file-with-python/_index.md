---
category: general
date: 2026-11-27
description: 使用 Python 建立 SVG 文件並儲存 SVG 檔案。學習將向量匯出為 SVG，快速產生 SVG 圖像。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: zh-hant
lastmod: 2026-11-27
og_description: 使用 Python 建立 SVG 文件並儲存 SVG 檔案。本指南將示範如何將向量匯出為 SVG，並在數分鐘內產生 SVG 圖像。
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: 使用 Python 建立 SVG 文件並儲存 SVG 檔案
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: 使用 Python 建立 SVG 文件並儲存 SVG 檔案
url: /zh-hant/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 建立 SVG 文件並儲存 SVG 檔案

如果您需要從頭**create SVG document**，本指南將帶您完成整個流程。您將看到如何在磁碟上**save SVG file**，將向量匯出為 SVG，並僅用幾行程式碼即可得到可直接使用的 SVG 圖像。

以程式方式產生可伸縮的圖形對於報告、使用者介面圖示，或任何需要解析度獨立圖像的情況都很有用。完成本教學後，您將能夠回答「**how to create SVG**？」這類關於簡單形狀的問題，並將此模式延伸至複雜的向量藝術作品。

## 您需要的條件

- Python 3.8 或更新版本  
- `svgwrite` 套件（可透過 `pip` 安裝）  
- 可寫入的目錄以儲存輸出檔案  

不需要外部圖形編輯器；所有操作皆可在命令列執行。

## 步驟 1：安裝 `svgwrite` 函式庫

`svgwrite` 提供乾淨、具 Python 風格的 API 來建立 SVG 標記。只需執行以下指令安裝一次：

```bash
pip install svgwrite
```

> **專業提示：** 使用虛擬環境（`python -m venv .venv`）以保持相依套件的隔離。

## 步驟 2：建立 SVG 文件

現在我們真的會**create SVG document**物件。`Drawing` 類別代表根 `<svg>` 元素，並會自動處理命名空間。

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

`Drawing` 實例是所有後續 SVG 操作的入口點。透過指定 `size` 我們設定畫布尺寸，這會影響瀏覽器渲染圖像的方式。

## 步驟 3：加入紅色圓形元素

加入形狀相當簡單。`circle` 方法會建立 `<circle>` 元素；接著我們將它附加到根節點。

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

為何選擇圓形：圓形是向量基元，能展示可伸縮性且不會失真，使其成為測試 **export vector as SVG** 工作流程的理想輸出。

## 步驟 4：儲存 SVG 檔案

最後，將標記寫入磁碟。此步驟滿足 **save SVG file** 的需求，並產生可在任何瀏覽器或向量編輯器中開啟的檔案。

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

執行腳本時，您會在主控台看到確認產生檔案位置的訊息。

### 預期輸出

產生的 `circle.svg` 內容如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

在瀏覽器中開啟此檔案會顯示清晰的紅色圓形，且因為它是向量基礎，您可以無限放大而不會出現像素化。

## 步驟 5：常見變化與邊緣情況

### 匯出更複雜的向量

如果您需要為多形狀插圖**export vector as SVG**，只要使用其他基元（`rect`、`line`、`path` 等）重複 `dwg.add()` 模式即可。例如：

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### 處理 Unicode 與文字

SVG 支援完整 Unicode 的文字元素。使用 `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` 以嵌入多語言標籤。

### 儲存至不同位置

當 **save SVG image** 至使用者指定的資料夾時，請驗證路徑以避免權限錯誤：

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### 壓縮輸出

在生產流程中，您可能希望檔案更小。將 `pretty=False` 傳遞給 `dwg.tostring()`，然後手動寫入結果：

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## 使用其他函式庫建立 SVG（可選）

雖然 `svgwrite` 輕量且純 Python，仍有其他生態系統可供選擇：

- **cairosvg** – 將 PNG、PDF 或 HTML 轉換為 SVG。  
- **lxml** – 讓您使用 XML API 手動建立 SVG 標記。  

選擇哪個函式庫取決於您專案的複雜度與現有相依性。

## 結論

您現在已了解如何使用 Python **create SVG document**、加入向量形狀，並 **save SVG file**。完整的解決方案示範了 **export vector as SVG** 的步驟、產生 **SVG image**，以及以程式方式回答常見的 **how to create SVG** 問題。

從這裡您可以：

- 使用迴圈擴充腳本，以自動產生圖表或圖示。  
- 將 SVG 輸出整合至 Web 應用程式或電子郵件範本。  
- 透過 `svgwrite` 加入 `<animate>` 元素，探索動畫效果。

嘗試不同的形狀、顏色與漸層，以充分發揮可伸縮向量圖形在 Python 專案中的威力。祝程式開發愉快！

## 接下來您可以學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [建立 SVG 文件 – 加入圓形並儲存為 SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [在 Python 中建立 SVG 文件 – SVG 轉 PNG 指南](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [載入 SVG 檔案 Python – 完整的匯出、嵌入與轉換指南](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}