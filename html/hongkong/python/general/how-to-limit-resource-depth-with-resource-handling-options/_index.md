---
category: general
date: 2026-10-25
description: 學習如何在使用 Python 儲存大型 HTML 檔案時限制資源深度並套用資源處理。請遵循此一步一步的指南，以獲得可靠的結果。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit resource depth
- apply resource handling
- HTML document processing
- save options Python
- resource handling options
language: zh-hant
lastmod: 2026-10-25
og_description: 限制資源深度並在使用 Python 儲存 HTML 時套用資源處理。本教學展示完整且可執行的解決方案。
og_image_alt: Screenshot illustrating limit resource depth in a Python script
og_title: 在套用資源處理時限制資源深度 – Python 指南
schemas:
- author: GroupDocs
  dateModified: '2026-10-25'
  description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  headline: How to limit resource depth with resource handling options
  type: TechArticle
- description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  name: How to limit resource depth with resource handling options
  steps:
  - name: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
    text: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
  - name: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
    text: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
  - name: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
    text: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
  type: HowTo
tags:
- Python
- HTML
- File handling
title: 如何使用資源處理選項限制資源深度
url: /zh-hant/python/general/how-to-limit-resource-depth-with-resource-handling-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何限制資源深度與 resource handling options

如果您需要在處理大型 HTML 檔案時 **限制資源深度**，本指南將會精確說明如何操作。完成本教學後，您亦會了解如何 **套用 resource handling**，使儲存動作遵守深度限制，避免無止境的處理。

大型 HTML 頁面常會嵌入許多外部資源——圖片、腳本、樣式表以及巢狀的 iframe。若未設定深度限制，解析器可能會追蹤每一個連結，導致記憶體使用量與處理時間急劇上升。此處所述的技巧可讓操作保持快速且可預測。

## 前置條件

在開始之前，請確保您已具備：

* 已安裝 Python 3.9 以上版本。
* 透過 `pip install groupdocs-viewer` 取得 `groupdocs-viewer`（或其他類似的 HTML 處理函式庫）。
* 在已知目錄中放置範例 HTML 檔案（`big_page.html`）。
* 具備輸出目錄的寫入權限。

上述項目可確保程式碼在不需額外設定的情況下順利執行。

## 步驟 1：載入來源 HTML 文件

第一步是建立指向原始檔案的 `HTMLDocument` 實例。此物件代表整個 HTML 結構，並在稍後提供存檔選項的存取。

```python
# Step 1: Load the source HTML document
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

*Why this matters*: 只載入一次檔案可讓函式庫擁有單一入口點供後續所有操作使用。它同時會驗證檔案是否存在，若路徑錯誤會提前拋出錯誤。

## 步驟 2：建立 resource handling options 並限制處理深度

`ResourceHandlingOptions` 讓您控制函式庫在遍歷連結資源時的深度。將 `max_handling_depth` 設為較低的數值（例如 5）即告訴引擎在超過五層巢狀後停止追蹤連結。

```python
# Step 2: Create resource handling options and limit the processing depth
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 5  # Restricts handling to 5 levels deep
```

*Why this matters*: 透過 **限制資源深度**，您可防止解析器下載每一張間接引用的圖片、腳本或 iframe，從而減少網路流量與記憶體壓力，特別是對於嵌入第三方內容的頁面。

## 步驟 3：將資源選項附加至 save options

`SaveOptions` 彙總所有會影響輸出檔案的設定。將 `resource_handling_options` 指派給它，即可 **套用 resource handling** 至即將執行的存檔操作。

```python
# Step 3: Attach the resource options to the save options
save_opts = SaveOptions()
save_opts.resource_handling_options = resource_opts
```

*Why this matters*: `save_opts` 物件充當多項旗標（壓縮、格式等）的容器。加入 `resource_handling_options` 可確保寫入階段遵守深度限制。

## 步驟 4：以套用限制資源處理的方式儲存文件

最後，使用已配置好的 `save_opts` 呼叫 `doc.save()`。輸出檔案將僅包含位於設定深度內的資源。

```python
# Step 4: Save the document with the limited resource handling applied
doc.save("YOUR_DIRECTORY/big_page_limited.html", save_opts)
```

**Expected result**:  
一個新檔案 `big_page_limited.html` 會出現在 `YOUR_DIRECTORY` 中。以瀏覽器開啟後，您會看到原始版面配置，但超過五層巢狀的資源將被省略。頁面載入更快，且佔用的記憶體大幅減少。

## 驗證已儲存的 HTML

儲存完成後，建議檢查是否確實遵守了深度限制。

```python
# Verify that the saved file exists and its size is reasonable
import os

output_path = "YOUR_DIRECTORY/big_page_limited.html"
if os.path.isfile(output_path):
    size_kb = os.path.getsize(output_path) / 1024
    print(f"Saved file size: {size_kb:.2f} KB")
else:
    raise FileNotFoundError("The limited HTML file was not created.")
```

若檔案大小相較原始檔案（可能高達數百 KB）顯著縮小，則 **限制資源深度** 的設定已如預期運作。

## 常見陷阱與避免方法

| 症狀 | 原因 | 解決方式 |
|------|------|----------|
| 檔案大小未變化 | `max_handling_depth` 保持預設（無限制） | 明確將 `resource_opts.max_handling_depth` 設為小於 ∞ 的數值 |
| 頁面缺少圖片 | 資源位於深度限制之外 | 提升深度或將關鍵資源移至較淺層級 |
| 儲存時出現 `PermissionError` | 輸出目錄為唯讀 | 改用可寫入的目錄或調整作業系統權限 |
| 出現 `ResourceHandlingException` | 函式庫版本不相容 | 升級至最新的 `groupdocs-viewer` 版本（`pip install --upgrade groupdocs-viewer`） |

**Pro tip**: 對於極大型頁面，可先以深度 3 為起點，逐步提升，直至視覺完整度符合需求。

## 可能遇到的邊緣情況

1. **透過 JavaScript 動態載入的內容** – 解析器僅能看到靜態 HTML。若頁面依賴腳本注入更多資源，這些資源不會計入深度限制。建議先以無頭瀏覽器預先渲染頁面，再套用限制。
2. **循環參照** – 某些頁面會嵌入指回同一頁面的 iframe。深度計數器可防止無限迴圈，但仍可能出現部分渲染的區段。可調整 `max_handling_depth` 或手動排除有問題的框架。
3. **混合協定（http/https）** – 若資源使用不同協定，函式庫可能將其視為不同網域。深度限制仍會跨協定套用，但網路權限可能有所差異。請確保環境同時允許兩種協定的存取。

## 往後步驟：進階 resource handling

既然您已能 **限制資源深度** 並 **套用 resource handling**，接下來可以探索：

* **自訂過濾器** – 使用 `resource_opts.resource_filter` 來跳過特定檔案類型（例如大型影片）。
* **壓縮設定** – 結合 `SaveOptions` 的 `compression_level` 進一步縮小輸出。
* **批次處理** – 迭代目錄中的多個 HTML 檔案，對每個檔案套用相同的深度限制。

透過這些擴充，您可以為大型文件工作流程建構完整的 HTML 最佳化管線。

## 結論

您已學會在使用 Python 儲存大型 HTML 文件時，如何 **限制資源深度** 與 **套用 resource handling**。透過設定 `ResourceHandlingOptions` 並將其附加至 `SaveOptions`，即可精細控制處理多少層巢狀資源，從而加速儲存並減少輸出檔案大小。請自行嘗試不同的深度值與其他 `SaveOptions`，以符合專案需求。

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題，並提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 Aspose.HTML Python 中設定 max_handling_depth – 完整指南](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [在 Python 中建立 resource handling options 並載入 HTML 文件](/html/english/python/general/create-resource-handling-options-and-load-an-html-document-i/)
- [如何以受控深度儲存 HTML – 步驟式 Python 教學](/html/english/python/general/how-to-save-html-with-controlled-depth-step-by-step-python-g/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}