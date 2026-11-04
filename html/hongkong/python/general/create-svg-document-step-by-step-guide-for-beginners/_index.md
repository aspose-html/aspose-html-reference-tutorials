---
category: general
date: 2026-07-02
description: 使用 Python 快速建立 SVG 文件。學習儲存 SVG 檔案、產生基本 SVG 圖像，並僅用幾行程式碼匯出 SVG。
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: zh-hant
og_description: 輕鬆建立 SVG 文件。本指南示範如何產生 SVG、儲存 SVG 檔案，以及使用乾淨的 Python 範例從程式碼匯出 SVG。
og_title: 建立 SVG 文件 – 快速 Python 教學
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: 建立 SVG 文件 – 初學者一步一步指引
url: /zh-hant/python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 SVG 文件 – 初學者逐步指南

有沒有想過如何在不打開圖形編輯器的情況下 **create SVG document**？你並不是唯一有此疑問的人。無論你需要為網頁製作小圖示，或是即時產生的動態圖表，能以程式方式 **create SVG document** 都能節省時間，並讓所有內容都能版本控制。

在本教學中，我們將逐步示範一個完整且可執行的範例，向你展示如何 **create SVG document**、**save SVG file**，以及解答在自動化圖形時常見的 “**how to generate SVG**” 問題。完成後，你將在磁碟上得到一個紅色方形，並且了解如何 **export SVG from code** 以應用於未來的任何專案。

## 你需要的條件

* Python 3.9 或更新版本（標準函式庫已能完成所有繁重工作）
* 你喜歡的文字編輯器或 IDE，如 VS Code、PyCharm，甚至 Notepad 都可
* 對將要 **save SVG file** 的資料夾具有寫入權限（我們將使用 `output/` 目錄）

不需要任何外部套件，設定時間實際上只需幾分鐘。

## 步驟 1：設定 SVG 輔助函式（建立文件）

首先，我們需要一個小型輔助程式來建立 SVG 背後的 XML 結構。可以把它想像成之後我們會 **create basic SVG image** 元素的畫布。

```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**此步驟的重要性：** `SVGDocument` 類別抽象化了低階的 XML 操作。將其封裝於類別中可讓其餘程式碼保持整潔，這在大型應用程式中 **export SVG from code** 時是一項最佳實踐。

## 步驟 2：加入矩形 – **Create Basic SVG Image** 範例的核心

既然我們已有文件物件，現在加入一個紅色方形。這是本教學中 **create basic SVG image** 部分的核心。

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**說明：**  
* 矩形的 `x` 與 `y` 座標設定為 10 像素的邊距，避免緊貼邊緣。  
* 使用字典來存放屬性讓程式碼更易讀，且與在任何基於 XML 的格式中 **save SVG file** 屬性的寫法相呼應。  
* 若需要 **how to generate SVG** 其他形狀，只要把標籤改為 `"circle"` 或 `"path"`，並相應調整屬性字典即可。

## 步驟 3：持久化 SVG – 最終 **Save SVG File** 至磁碟

我們已在記憶體中建立文件；現在將其寫入磁碟。此時抽象的 **create SVG document** 變成可在瀏覽器開啟的實體檔案。

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**你會看到的結果：** 在 Chrome、Firefox 或任何支援 SVG 的檢視器中開啟 `output/square.svg`，會顯示一個帶有細白色邊框的簡單紅色方形（即 SVG 畫布的背景）。這證明我們已成功 **exported SVG from code**。

## 完整腳本 – 單檔解決方案

以下為完整腳本，可直接複製貼上至 `create_svg.py`。執行 `python create_svg.py` 即會產生上述檔案。

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### 預期輸出

執行腳本會輸出：

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

而產生的 `square.svg` 如下（簡化示意）：

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

開啟檔案會呈現清晰的紅色方形——正是我們想要 **create basic SVG image** 的結果。

## 擴充範例 – 常見問題解答

### 如何加入文字或其他形狀？

只要呼叫 `svg.create_element("text", {...})` 或 `svg.create_element("circle", {...})`，並像矩形一樣將其加入即可。相同的 **how to generate SVG** 邏輯同樣適用。

### 若需要 **export SVG from code** 且背景透明該怎麼做？

從根 `<svg>` 元素移除所有 `fill` 屬性，或對應需要透明的形狀設定 `fill="none"`。XML 仍然有效，瀏覽器會自動呈現透明效果。

### 我可以 **save SVG file** 為易讀的格式嗎？

`ElementTree` writes compact XML by default. For a human‑readable version, you can use `xml.dom.minidom` to re‑format:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

將 `svg.save(output_path)` 改為 `pretty_save(svg, output_path)` 即可。

### 大型 SVG 的效能如何？

在產生上千個元素時，建議先建立 `ET.Element` 物件的清單，然後一次性將其加入根節點。這樣可減少樹的變更次數，提升 **save SVG file** 的執行速度。

## 專業技巧與常見陷阱

* **專業提示：** 在 **saving SVG file** 時始終使用絕對路徑（或 `pathlib.Path`）；相對路徑在腳本於不同工作目錄執行時可能失效。  
* **注意：** 忘記註冊 SVG 命名空間。若未呼叫 `ET.register_namespace("", SVGDocument.SVG_NS)`，輸出會包含多餘的 `ns0` 前綴，部分瀏覽器會誤解。  
* **常見錯誤：** 在屬性值中混用整數與字串。XML 需要字串，我們會使用 `str()` 進行轉換——輔助類別已為你處理，但若自行繞過，可能會拋出 `TypeError`。  

## 結論

我們剛剛完整示範了一個端對端的範例，說明如何 **create SVG document**、**save SVG file**，以及回答

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎延伸技術。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}