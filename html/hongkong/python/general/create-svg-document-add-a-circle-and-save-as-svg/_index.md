---
category: general
date: 2026-07-31
description: 學習如何建立 SVG 文件、加入圓形，並快速儲存 SVG 檔案。只需幾行 Python 程式碼，即可將圖形匯出為 SVG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: zh-hant
lastmod: 2026-07-31
og_description: 在幾秒鐘內建立 SVG 文件、加入圓形並儲存 SVG 檔案。本指南示範如何以清晰且可直接執行的程式碼將圖形匯出為 SVG。
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: 建立 SVG 文件 – 加入圓形並儲存為 SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: 建立 SVG 文件 – 新增圓形並儲存為 SVG
url: /zh-hant/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 SVG 文件 – 新增圓形並儲存為 SVG

有沒有曾經需要從程式碼 **create SVG document** 但不知從何開始？你並不孤單；許多開發者在首次接觸向量圖形時都會卡在這裡。在本教學中，我們將示範一個小型、獨立的範例，教你如何 **add circle to SVG**，然後 **save SVG file**，讓你可以 **export graphic as SVG** 用於網站或設計工具。

我們會保持簡潔：只需幾行 Python、一本流行的 SVG 輔助函式庫，以及少量說明。完成後，你將在資料夾中得到一個可直接使用的 `circle.svg`，並且了解每一步的意義——不會有模糊的「請參考文件」捷徑。

## 需要的工具

- Python 3.8+（任何較新版本皆可）
- `svgwrite` 套件 – 使用 `pip install svgwrite` 安裝
- 文字編輯器或 IDE（VS Code、PyCharm，甚至 Notepad 都行）
- 需要對欲儲存檔案的目錄具有寫入權限

就這樣。沒有大型相依套件，也不需要外部服務。

## 步驟 1：設定 SVG 文件

建立 SVG 文件就像從 `svgwrite` 中實例化一個 `Drawing` 物件一樣簡單。把這個物件想像成所有形狀的空白畫布。

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Why this matters:** `Drawing` 類別會為你處理所有 XML 樣板——命名空間、標頭，以及根 `<svg>` 元素。提前指定檔名後，我們已經知道檔案最終會存放在哪裡，這讓之後的 **save svg file** 步驟變得簡單。

### 小技巧
如果你打算在迴圈中產生大量檔案，請為每個 `Drawing` 指定唯一名稱，或使用 `io.BytesIO` 將所有內容保留在記憶體中，直到準備寫入為止。

## 步驟 2：在 SVG 中新增圓形

既然文件已建立，讓我們 **add circle to SVG**。`add()` 方法接受任何形狀物件；`Circle` 非常適合在中心放置一個簡單的紅點。

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Why we use `center` and `radius` variables:** 為什麼使用 `center` 與 `radius` 變數：硬編碼數字會讓程式碼難以閱讀與維護。透過為值命名，我們能清楚表達意圖——此圓形正好位於 200 × 200 畫布的正中心，且大小足以顯眼。

### 邊緣情況 – 透明背景
如果需要透明背景（SVG 的預設），可以不在根元素設定 `fill`。若想要白色背景，請加入以下程式碼：

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

將此程式碼放在新增圓形之前，讓矩形位於底層。

## 步驟 3：儲存 SVG 檔案

形狀已就位，最後一步是 **save SVG file**。`save()` 方法會將 XML 寫入磁碟，因為我們已為 `Drawing` 指定檔名，只需一次呼叫即可完成。

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **What happens under the hood?** `svgwrite` 會將元素樹序列化為字串，加入 XML 宣告，並以 UTF‑8 編碼寫入。如果目標目錄不存在，Python 會拋出 `FileNotFoundError`；請確保路徑有效，或使用 `os.makedirs()` 建立目錄。

### 加分項：以程式方式匯出 SVG 圖形
如果需要將 SVG 內容作為字串取得——例如嵌入 HTML 電子郵件中——可以呼叫 `dwg.tostring()` 取代 `save()`：

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## 完整範例

將上述步驟整合起來，以下是一個完整、可直接執行的腳本：

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Expected output:** 執行腳本後，你會在同一資料夾看到 `circle.svg` 檔案。用瀏覽器或任何向量編輯器開啟，會看到一個位於白色方形中心的紅色圓形——正是我們程式碼所產生的結果。

## 常見問題與注意事項

- **What if I want a different shape?** 將 `dwg.circle` 換成 `dwg.rect`、`dwg.ellipse`，或自訂的 `<path>` 字串。API 在各種形狀間保持一致。
- **Can I embed the SVG directly in HTML?** 當然可以。剛建立的檔案可以使用 `<img src="circle.svg" alt="Red circle">` 來引用，或直接內嵌於 `<svg>` 標籤中。
- **Why not write raw XML?** 雖然可以自行撰寫 XML，但像 `svgwrite` 這類函式庫會處理命名空間的細節，讓程式碼更易維護——尤其在加入漸層或動畫時。

## 結論

現在你已掌握如何 **create SVG document**、**add circle to SVG**，以及 **save SVG file**，只需幾行 Python 就能 **export graphic as SVG**。此模式具備可擴充性：將圓形換成任何向量形狀、對資料迴圈產生圖表，或批次處理設計系統的資產。

下一步？試著加入文字標籤、實驗漸層，或在單一腳本中產生整個圖示庫。如果想了解更進階的功能，請參閱 `svgwrite` 文件中關於群組（`<g>`）、變形與動畫支援的說明。

祝程式開發愉快，願你的向量圖永遠保持銳利！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在本教學示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}