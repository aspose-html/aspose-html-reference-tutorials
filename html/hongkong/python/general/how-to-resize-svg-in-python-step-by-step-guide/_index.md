---
category: general
date: 2026-06-16
description: 快速在 Python 中調整 SVG 大小 – 載入 SVG 檔案、編輯 SVG 檔案，甚至使用小腳本批量調整 SVG 檔案大小。
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: zh-hant
og_description: 如何在 Python 中調整 SVG 大小？學習在 Python 載入 SVG 檔案、編輯 SVG 檔案，並使用清晰可執行的範例批量調整
  SVG 檔案大小。
og_title: 如何在 Python 中調整 SVG 大小 – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  headline: How to Resize SVG in Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  name: How to Resize SVG in Python – Step‑by‑Step Guide
  steps:
  - name: '**Collects** every `.svg` file in the source folder.'
    text: '**Collects** every `.svg` file in the source folder.'
  - name: '**Loads** each file using the same routine we used for a single SVG.'
    text: '**Loads** each file using the same routine we used for a single SVG.'
  - name: '**Resizes** to the desired width while keeping the aspect ratio.'
    text: '**Resizes** to the desired width while keeping the aspect ratio.'
  - name: '**Writes** the result to a new folder, leaving originals untouched.'
    text: '**Writes** the result to a new folder, leaving originals untouched.'
  type: HowTo
tags:
- Python
- SVG
- Automation
title: 如何在 Python 中調整 SVG 大小 – 步驟指南
url: /zh-hant/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中調整 SVG 大小 – 完整教學

有沒有想過 **如何在不開啟圖形編輯器的情況下調整 SVG 大小**？也許你有一個需要在網頁橫幅上顯示 200 px 寬的標誌，或是正在為手機應用程式準備數十個圖示。好消息是？你可以全部用 Python 完成——不需要 Photoshop、也不需要 Inkscape 的介面，只要幾行程式碼。

在本指南中，我們將逐步說明如何在 Python 中載入 SVG 檔案、編輯其尺寸，甚至一次性縮放整個資料夾的 SVG。完成後，你將能自信地 **load SVG file Python**、**edit SVG file Python**，以及 **batch resize SVG files**。

## 前置條件

- 已安裝 Python 3.8 以上（使用標準的 `python` 指令）
- `svgwrite` 或 `lxml` 函式庫 – 我們將使用 `lxml`，因為它提供直接的 DOM 存取。
- 一個想要調整大小的 SVG 資料夾（例如 `assets/icons/`）

你不需要任何 GUI 工具；所有操作皆在終端機執行。

---

## 步驟 1：安裝所需函式庫

首先，從 PyPI 取得 `lxml`。它體積小、速度快，且能直接操作 XML 屬性。

```bash
pip install lxml
```

> **小技巧：** 若你在虛擬環境中工作，請先啟動該環境再執行指令。這樣可以讓專案的相依性保持整潔。

## 步驟 2：在 Python 中載入 SVG 檔案

現在我們將以 **load SVG file Python** 方式——讀取 XML、取得根 `<svg>` 元素，並印出其目前的尺寸。

```python
from lxml import etree

def load_svg(path: str) -> etree._ElementTree:
    """
    Load an SVG document and return the parsed XML tree.
    """
    parser = etree.XMLParser(remove_blank_text=True)
    tree = etree.parse(path, parser)
    return tree

# Example usage
svg_path = "assets/logo.svg"
svg_tree = load_svg(svg_path)
root = svg_tree.getroot()
print(f"Original width: {root.get('width')}, height: {root.get('height')}")
```

**為什麼這很重要：** `lxml` 為我們提供真實的 DOM，讓我們能查詢或變更任何屬性——非常適合 **edit SVG file Python** 任務。

## 步驟 3：變更寬度（及高度） – 如何調整 SVG 大小

SVG 為向量圖形，你可以設定寬度、長度或兩者同時。若只變更寬度，viewBox 會保持長寬比，但許多工具也會遵守相對應的高度屬性。以下是一個在保留原始長寬比的情況下調整大小的輔助函式：

```python
def resize_svg(tree: etree._ElementTree, new_width: int) -> None:
    """
    Resize the root <svg> element to `new_width` while preserving aspect ratio.
    """
    root = tree.getroot()
    # Grab original dimensions (they may be in px, pt, or just numbers)
    orig_width = float(root.get("width").replace("px", ""))
    orig_height = float(root.get("height").replace("px", ""))

    # Compute scale factor and new height
    scale = new_width / orig_width
    new_height = round(orig_height * scale, 2)

    # Update attributes
    root.set("width", f"{new_width}px")
    root.set("height", f"{new_height}px")

    # Optional: ensure viewBox exists for better scaling in browsers
    if "viewBox" not in root.attrib:
        viewbox = f"0 0 {orig_width} {orig_height}"
        root.set("viewBox", viewbox)

# Resize to 200 px wide
resize_svg(svg_tree, 200)
```

上述函式即是 **how to resize SVG** 的核心。它會讀取目前尺寸、計算等比例的高度，並將新屬性寫回檔案。

## 步驟 4：儲存已修改的 SVG

編輯完成後，需要將變更寫回磁碟。這樣就完成了 **edit SVG file Python** 的循環。

```python
def save_svg(tree: etree._ElementTree, destination: str) -> None:
    """
    Write the modified SVG tree to `destination`.
    """
    tree.write(
        destination,
        pretty_print=True,
        xml_declaration=True,
        encoding="UTF-8"
    )
    print(f"Saved resized SVG to {destination}")

# Save as a new file so the original stays untouched
output_path = "assets/logo_resized.svg"
save_svg(svg_tree, output_path)
```

執行整個腳本後，你會看到一個全新的 `logo_resized.svg`，寬度正好為 200 px。

## 步驟 5：批次調整 SVG 檔案大小 – 縮放整個資料夾

既然我們已能 **load SVG file Python**、**edit SVG file Python** 並儲存，接下來就遍歷目錄，對每個檔案套用相同的轉換。這就是 **batch resize SVG files** 的解法。

```python
import pathlib

def batch_resize(source_dir: str, target_dir: str, width: int) -> None:
    """
    Resize every .svg file in `source_dir` to `width` pixels and store
    the results in `target_dir`.
    """
    src = pathlib.Path(source_dir)
    tgt = pathlib.Path(target_dir)
    tgt.mkdir(parents=True, exist_ok=True)

    svg_files = list(src.glob("*.svg"))
    if not svg_files:
        print("No SVG files found.")
        return

    for svg_path in svg_files:
        try:
            tree = load_svg(str(svg_path))
            resize_svg(tree, width)
            out_path = tgt / svg_path.name
            save_svg(tree, str(out_path))
        except Exception as e:
            print(f"Failed on {svg_path.name}: {e}")

# Example: resize everything in 'assets/icons' to 64 px wide
batch_resize("assets/icons", "assets/icons_resized", 64)
```

### 這段程式碼的作用：

1. **收集** 來源資料夾中的所有 `.svg` 檔案。
2. **載入** 每個檔案，使用與單一 SVG 相同的流程。
3. **調整大小** 為目標寬度，同時保持長寬比。
4. **寫入** 結果至新資料夾，保持原始檔案不變。

現在你已擁有可直接使用的 **batch resize SVG files** 工作流程。

## 步驟 6：邊緣情況與常見陷阱

| 問題 | 發生原因 | 解決方案 |
|------|----------|----------|
| 缺少 `width`/`height` 屬性 | 某些 SVG 僅依賴 `viewBox`。 | 若屬性不存在，改用 viewBox 尺寸作為備援 (`viewBox="0 0 w h"`)。 |
| 非 `px` 單位（例如 `pt`、`%`） | 腳本僅移除 `px`。 | 擴充 `replace` 呼叫或使用正則表達式捕捉任何單位。 |
| 複雜的 `<symbol>` 或 `<use>` 元素 | 調整根元素可能不會影響嵌套的 symbols。 | 對每個 `<symbol>` 標籤套用相同的屬性變更，或使用 CSS `transform: scale()`。 |
| 檔名中的 Unicode 或特殊字元 | `pathlib` 能處理大多數情況，但 Windows 可能無法接受某些字元。 | 確保檔名為 UTF‑8 安全，或在處理前重新命名。 |

## 步驟 7：驗證結果

可以使用一段簡短的 HTML 片段快速做 sanity check：

```html
<!DOCTYPE html>
<html>
<head><title>SVG Test</title></head>
<body>
  <h3>Original</h3>
  <img src="assets/logo.svg" alt="original logo">
  <h3>Resized</h3>
  <img src="assets/logo_resized.svg" alt="resized logo">
</body>
</html>
```

在瀏覽器中開啟該檔案——兩張圖應該看起來相同，但在開發者工具中，已調整大小的圖會顯示寬度為 **200 px**。

---

## 結論

現在你已掌握使用純 Python **how to resize SVG** 的方法，無論是單一檔案或整個目錄。此工作流程涵蓋 **load SVG file Python**、**edit SVG file Python**，以及 **batch resize SVG files**——只需少數函式即可完成。

試著跑跑看：嘗試不同的寬度、僅調整高度，或使用 `argparse` 加入命令列介面。可能性無窮，而此腳本足夠輕量，可嵌入建置流水線、CI 工作或桌面工具中。

對於處理漸層、內嵌字型，或將此整合至 Flask 應用有任何疑問嗎？留下評論，我們一起探討。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.HTML 在 .NET 中將 SVG 轉換為圖像](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [使用 Aspose.HTML 在 .NET 中將 SVG 轉換為 PDF](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [使用 Aspose.HTML 在 .NET 中將 SVG 文件呈現為 PNG](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}