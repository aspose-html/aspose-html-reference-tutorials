---
category: general
date: 2026-07-27
description: 如何在 Aspose.HTML（Python）中使用 SaveOptions 轉換大型 HTML 頁面並有效地處理資源。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: zh-hant
lastmod: 2026-07-27
og_description: 使用 Aspose.HTML (Python) 的 SaveOptions 可讓您在轉換大型 HTML 頁面時套用資源處理，達致乾淨且快速的結果。
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: 如何在 Aspose.HTML 中使用 SaveOptions – Python 指南
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: 如何在 Aspose.HTML（Python）中使用 SaveOptions
url: /zh-hant/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose.HTML (Python) 中使用 SaveOptions

如何在 Aspose.HTML for Python 中使用 SaveOptions 是許多開發者在處理大型 HTML 檔案時常問的問題。如果你需要 **轉換大型 HTML 頁面** 同時緊密控制 **套用資源處理**，你來對地方了。  

在本教學中，我們將示範一個真實情境：取得一個龐大的 HTML 頁面、限制資源的嵌套深度，最後以清晰的方式儲存（或轉換）結果。沒有模糊的說明，只有完整、可直接執行的範例，今天就可以直接複製貼上到你的專案中。

> **小技巧：** Aspose.HTML 的 `SaveOptions` 不僅可用於儲存回 HTML，還可用於轉換成 PDF、PNG，甚至 DOCX。下方示範的模式同樣適用於所有這些格式。

---

## 需要的環境

- **Python 3.8+**（程式碼使用型別提示，但在任何近期版本皆可執行）  
- **Aspose.HTML for Python via .NET** – 使用 `pip install aspose-html` 安裝  
- 一個 **大型 HTML 檔案**（範例使用 `big_page.html`）  
- 足夠的磁碟空間以存放輸出檔案  

就這些——不需要額外的函式庫，也不需要大型建置工具。

---

## 如何使用 SaveOptions 搭配資源處理選項

這是重點。我們會建立一個 `SaveOptions` 實例，附加一個 `ResourceHandlingOptions` 物件，告訴 Aspose.HTML 要追蹤多少層的連結資源，然後把所有設定交給文件的 `save` 方法。

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**為什麼這樣可行：**  
- `HTMLDocument` 會載入原始檔案，解析每個 `<img>`、`<link>`、`<script>` 等標籤。  
- `ResourceHandlingOptions.max_handling_depth` 告訴引擎在三層嵌套後停止追蹤資源——這對避免在嵌入其他頁面的情況下產生無限迴圈非常有效。  
- `SaveOptions` 是承載輸出格式（預設為 HTML）以及資源處理規則的容器。  
- 最後，`doc.save` 會寫入新檔案，套用我們剛設定的規則。

執行腳本後，你會在 `big_page_processed.html` 看到新檔案。用瀏覽器開啟它，你會發現所有深度不超過三層的圖片、樣式與腳本仍然存在，而更深層的引用則被剔除。這大幅減少檔案大小，同時不會破壞頁面的核心版面——正是 **轉換大型 HTML 頁面** 用於離線或電子郵件傳送時所需要的效果。

---

## 高效轉換大型 HTML 頁面

如果你的目標是 *將大型 HTML 頁面* 轉換成較小的版本，上面的程式碼已完成大部分工作。不過，你可能想要改變輸出格式。Aspose.HTML 只需要一行程式碼即可完成：

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

只要把 `format` 屬性改成 `"PNG"`、`"JPEG"` 或 `"DOCX"`，就能建立完整的轉換管線。相同的 **套用資源處理** 規則仍然有效，因此產生的 PDF 不會嵌入原始網站的每一個外部 CSS 檔案——只會包含你設定的三層深度內的資源。

---

## 對巢狀資源套用資源處理

讓我們更深入探討 **套用資源處理** 的實作。假設你的 HTML 包含一個樣式表，而該樣式表又匯入其他樣式表，進而載入圖片。若不設深度限制，Aspose.HTML 可能會無止盡地追蹤鏈結，導致記憶體與 CPU 使用量暴增。

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Depth 0** – 不會抓取任何外部資源；只得到一個極簡的 HTML 骨架。  
- **Depth 1** – 只包含第一層資源（直接的 `<img>` 標籤、即時的 CSS 檔案）。  
- **Depth 2+** – 會尊重更深層的巢狀結構，適合樣式相互依賴的複雜網站。

依照你的 **轉換大型 HTML 頁面** 情境選擇適當的深度。對於電子報而言，Depth 1 通常已足夠；若是本地存檔，Depth 3（如主範例所示）則提供了不錯的平衡。

---

## 完整範例 – 從頭到尾

以下是一個可自行執行的腳本，請存成 `process_html.py`。它包含錯誤處理、日誌記錄，以及一個小幫手，用來顯示你減少了多少檔案大小。

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**預期的主控台輸出：**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

開啟處理後的檔案，你會看到一個仍保留原始外觀的精簡頁面。如果你把 `fmt` 改成 `"PDF"`，主控台會顯示 PDF 檔案大小，你可以用任何 PDF 閱讀器開啟它。

---

## 常見問題與邊緣案例

- **如果頁面引用的 HTTPS 資源需要驗證該怎麼辦？**  
  Aspose.HTML 會遵循重新導向，但不會自動傳送憑證。你可以先自行下載這些資產，或使用自訂的 `WebRequest` 處理器（超出本指南範圍）。

- **我可以保留內嵌 CSS 同時剔除外部檔案嗎？**  
  可以——將 `resource_options.max_handling_depth = 0`。這樣會跳過外部檔案，但保留所有 `<style>` 區塊。

- **如果仍有非常大的圖片導致輸出檔案過大怎麼辦？**  
  儲存後，你可以使用 Pillow 再次壓縮圖片，或利用 Aspose.HTML 內建的影像壓縮選項（使用 `save_options.image_quality`）。

- **深度限制是針對每種資源類型分別套用的嗎？**  
  限制是全域的，適用於所有資源類型（圖片、腳本、樣式）。若需要更細緻的控制，必須在載入文件後自行過濾資源。

---

## 結論

現在你已掌握 **如何在 Aspose.HTML 中使用 SaveOptions** 的完整技巧。

## 接下來該學什麼？

以下教學與本指南緊密相關，會在此基礎上延伸更多 API 功能與替代實作方式，每篇皆提供完整可執行的程式碼範例與逐步說明，協助你在自己的專案中更進一步。

- [如何使用 Aspose.HTML for Java 轉換 HTML 為 PDF](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [如何使用 Aspose.HTML for Java 轉換 HTML 為 MHTML](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [如何使用 Aspose 渲染 HTML 為 PNG – 步驟說明](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}