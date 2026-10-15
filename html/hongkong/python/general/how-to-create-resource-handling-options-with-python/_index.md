---
category: general
date: 2026-10-15
description: 學習如何建立資源處理選項以及如何在 Python 中設定 Markdown 儲存的最大處理深度，請跟隨一步一步的教學。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: zh-hant
lastmod: 2026-10-15
og_description: 在 Python 中建立資源處理選項，以控制巢狀資源的處理。此教學示範如何設定最大處理深度，確保 Markdown 匯出可靠。
og_image_alt: Screenshot showing Python code to create resource handling options and
  set max handling depth
og_title: 建立資源處理選項 – Python 指南
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Learn how to create resource handling options and how to set max handling
    depth for Markdown saving in Python. Follow a step‑by‑step guide.
  headline: How to create resource handling options with Python
  type: TechArticle
tags:
- resource handling
- Markdown
- Python
- options
title: 如何使用 Python 建立資源處理選項
url: /zh-hant/python/general/how-to-create-resource-handling-options-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 建立資源處理選項

如果您需要為 Markdown 匯出 **建立資源處理選項**，本指南將提供完整解決方案。您將會看到 **如何設定最大處理深度**，以便在達到指定層級後停止處理巢狀資源。

在從包含圖像、嵌入檔案或其他連結資產的複雜文件產生 Markdown 時，資源處理是必不可少的。未受控的遞迴可能導致效能問題或記憶體不足錯誤。透過設定處理深度，您可以讓流程保持可預測且高效。

在本教學中，您將會：

* 初始化 `ResourceHandlingOptions` 物件。
* 設定最大處理深度。
* 將此選項附加至 `MarkdownSaveOptions` 實例。
* 執行完整範例，您可直接複製到專案中。

不需要除標準 SDK 之外的外部函式庫，且程式碼相容於截至 2026 年 10 月的最新 Python 套件版本。

## 前置條件

在開始之前，請確保您已具備：

* 已安裝 Python 3.9 或更新版本。
* 提供 `ResourceHandlingOptions` 與 `MarkdownSaveOptions` 的 SDK（例如 `groupdocs-viewer` 或類似套件）。使用以下指令安裝：

```bash
pip install groupdocs-viewer
```

* 基本了解 Python 類別與物件屬性。

## 步驟 1：建立資源處理選項

第一步是 **建立資源處理選項**。此物件充當所有資源相關設定的容器。

```python
from groupdocs.viewer import ResourceHandlingOptions, MarkdownSaveOptions

# Step 1: Instantiate the options object
resource_options = ResourceHandlingOptions()
```

`ResourceHandlingOptions` 預設不會套用任何限制，這表示檢視器會追蹤它遇到的每一個連結資源。初始化此物件可讓您從乾淨的狀態開始，精確地套用控制。

## 步驟 2：設定最大處理深度

現在您將學習 **如何設定最大處理深度**。屬性 `max_handling_depth` 定義匯出器在停止前會處理的巢狀層級數量。

```python
# Step 2: Limit the handling depth to five levels
resource_options.max_handling_depth = 5
```

為何要限制深度？想像一個 Markdown 文件引用另一個 Markdown 檔案，而該檔案又引用第三個檔案，如此類推。若未設定深度限制，匯出器可能無限遞迴，耗盡記憶體與 CPU。將 `max_handling_depth` 設為 `5` 即告訴引擎在五層巢狀資源後停止，這是大多數專案的安全預設值。

### 邊緣案例：無限制深度

如果您刻意需要無限制遞迴（在正式環境中少見），可將值設為 `None`：

```python
resource_options.max_handling_depth = None  # No limit
```

請注意，無限制深度在極大型文件樹上可能導致效能下降。

## 步驟 3：將選項附加至 MarkdownSaveOptions

在設定資源處理後，您必須將選項附加至 `MarkdownSaveOptions` 實例。這會告訴匯出器在儲存時使用這些設定。

```python
# Step 3: Create MarkdownSaveOptions and attach the resource handling config
markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

`MarkdownSaveOptions` 彙總所有匯出相關設定。將 `resource_options` 指派給其 `resource_handling_options` 屬性，即可確保在轉換過程中套用深度限制。

## 步驟 4：執行完整轉換（示範）

以下程式碼示範如何使用剛剛建立的選項，將範例文件完整轉換為 Markdown。請依您的環境調整檔案路徑。

```python
from groupdocs.viewer import Viewer

# Path to the source document (e.g., a DOCX with embedded images)
source_path = "sample.docx"
# Path where the Markdown output will be saved
output_path = "output.md"

# Initialize the viewer with the source file
viewer = Viewer(source_path)

# Perform the conversion using the configured options
viewer.save(output_path, markdown_options)

print(f"Conversion complete. Markdown saved to {output_path}")
```

**預期輸出**

```
Conversion complete. Markdown saved to output.md
```

執行腳本後，開啟 `output.md`。您會看到圖像與其他資源的引用最多到五層深度；更深層的連結會被省略，避免遞迴失控。

## 專業提示：於執行時驗證處理深度

若需確認已套用深度限制，您可以檢查產生的 Markdown 是否缺少資源參照，或在 SDK 中啟用詳細日誌：

```python
viewer.set_logging(True)  # Enable detailed logs
```

日誌會顯示類似以下訊息：

```
[INFO] Resource handling stopped at depth 5 for file 'nested_image.png'
```

## 常見問題

**如果我的文件少於五層巢狀資源會怎樣？**  
匯出器會處理所有可用資源，因為深度限制高於實際層級，不會截斷任何資源。

**我可以針對不同檔案類型設定不同的限制嗎？**  
可以。為每種匯出格式建立獨立的 `ResourceHandlingOptions` 物件，並指派給相對應的 `SaveOptions` 實例。

**深度限制只影響圖像嗎？**  
不會。此限制適用於匯出器能追蹤的 *所有* 資源，包括嵌入檔案、超連結以及巢狀的 Markdown 包含。

## 結論

您現在已了解如何 **建立資源處理選項** 以及 **設定最大處理深度**，以在 Python 中執行可靠的 Markdown 匯出。透過限制遞迴，您可防止應用程式因記憶體使用過多而受影響，同時仍保留必要的內容層級結構。

接下來您可以探索以下方向：

* 調整其他 `ResourceHandlingOptions` 屬性，例如 `extract_images` 或 `preserve_links`。
* 結合資源處理與自訂的抽取檔案命名規則。
* 嘗試不同的深度值，以找出最適合您特定文件集合的最佳設定。

歡迎將程式碼片段套用到您的工作流程，並與社群分享您的發現。祝開發愉快！

## 接下來您可以學習什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上延伸技術。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Zip HTML in C# – Custom Resource Handler Tutorial](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-custom-resource-handler-tutorial/)
- [How to create custom schema handler with Aspose.HTML for Java](/html/english/java/custom-schema-message-handling/custom-schema-message-handler/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}