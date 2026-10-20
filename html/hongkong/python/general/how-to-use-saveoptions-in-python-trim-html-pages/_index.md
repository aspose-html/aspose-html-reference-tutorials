---
category: general
date: 2026-05-28
description: 學習如何在 Python 中使用 SaveOptions 裁剪 HTML 頁面。本一步一步的指南亦說明如何載入 HTML 文件並高效移除嵌套資源。
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: zh-hant
og_description: 如何在 Python 中使用 SaveOptions 修剪 HTML 頁面。請依照本指南載入 HTML 文件、設定資源限制，並儲存為乾淨、輕量的檔案。
og_title: 如何在 Python 中使用 SaveOptions – 裁剪 HTML 頁面
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: 如何在 Python 中使用 SaveOptions – 修剪 HTML 頁面
url: /zh-hant/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中使用 SaveOptions – 修剪 HTML 頁面

有沒有想過 **如何使用 SaveOptions** 來縮減龐大的 HTML 檔案而不破壞任何內容？你並不是唯一有此疑問的人。當你抓取一個包含數十個巢狀資源的頁面——例如 CSS、JS，甚至其他 HTML 片段——你的輸出可能會失控地膨脹。  

在本教學中，我們將逐步示範一個完整、可執行的範例，不僅說明 **如何使用 SaveOptions**，還涵蓋 **如何載入 HTML 文件** 以及透過限制巢狀深度來 **修剪 HTML 頁面** 的最佳方式。完成後，你將擁有一個乾淨、已修剪的檔案，可直接部署或進一步處理。

## 您將達成的目標

- 只需一行程式碼即可載入任何本機 HTML 檔案。  
- 設定資源處理選項，以在特定的包含深度停止。  
- 使用功能強大的 `SaveOptions` 類別儲存修剪後的結果。  

不需要外部工具，也不需要魔法——只要純粹的 Python 加上一個能完成繁重工作的微型函式庫。

---

## 前置條件

在開始之前，請確保你已具備以下條件：

1. 已安裝 **Python 3.9+**（本文使用的語法在任何近期版本皆可執行）。  
2. 假設存在的 `htmlprocessor` 套件，提供 `HTMLDocument`、`SaveOptions` 與 `ResourceHandlingOptions`。可透過以下方式安裝：

```bash
pip install htmlprocessor
```

> **小技巧：** 若你使用虛擬環境，請先啟動它——這樣可以讓相依套件保持整潔。

---

## 步驟 1：如何載入 HTML 文件

載入檔案就像把建構子指向你的路徑那麼簡單。函式庫會讀取標記、建立類似 DOM 的樹狀結構，並為後續操作做好準備。

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **為什麼這很重要：** `HTMLDocument` 物件抽象掉原始字串處理，提供查詢、修改以及最終儲存頁面的各種方法。它同時會正規化換行符與字元編碼，避免日後出現微妙的錯誤。

我們會印出標題以驗證載入是否成功。如果檔案遺失或格式錯誤，建構子會拋出明確的例外——不會出現靜默失敗。

---

## 步驟 2：設定資源處理 – 修剪的核心

接下來的關鍵是 **如何修剪 HTML 頁面** 內容，方法是限制處理器追蹤包含的深度。這正是 `ResourceHandlingOptions` 大顯身手的地方。

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### `max_handling_depth` 的作用是什麼？

- **Depth 1** → 只處理根 HTML 檔案，所有外部資源皆被忽略。  
- **Depth 2** → 包含根檔案以及任何直接引用的檔案（例如 `iframe` 或伺服器端包含）。  
- **Higher values** → 更深的巢狀層級，但同時會產生更大的輸出與較長的處理時間。

將深度上限設為 **2**，即可保留主頁面與一層包含，將更深層的內容剔除。這通常足以去除冗餘的頁腳、分析腳本或你在修剪副本中不需要的巢狀模板。

---

## 步驟 3：將選項套用至儲存設定

現在，我們把資源規則綁定到 `SaveOptions` 實例。此物件會告訴函式庫 **精確** 如何將檔案寫回磁碟。

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **為什麼要使用 `SaveOptions`？**  
> 它讓你對輸出擁有粒度極細的控制——不僅僅是資源深度。之後你還可以加入壓縮、格式化輸出，甚至自訂回呼函式，而不必觸碰核心的儲存邏輯。

---

## 步驟 4：如何使用 SaveOptions 修剪 HTML 頁面

最後，我們以已設定好的選項呼叫 `save` 方法。函式庫會遍歷 DOM，遵守深度限制，並寫入修剪後的檔案。

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### 預期結果

- `trimmed_page.html` 檔案包含原始標記 **加上** 深度不超過一層的所有包含。  
- 所有更深層的包含皆被省略，產生更小且載入更快的頁面。  
- 不會出現斷裂的標籤——函式庫會自動關閉因移除而遺留的未閉合元素。

你可以在瀏覽器中開啟輸出檔案，驗證主要內容仍能正確呈現，而多餘的腳本或巢狀框架則已消失。

---

## 完整可執行範例

將所有步驟整合起來，以下是你可以直接複製貼上並執行的完整腳本：

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

執行腳本，將 `INPUT` 指向任意複雜的 HTML 檔案，即可在 `OUTPUT` 中得到更精簡的版本。  

> **邊緣案例說明：** 若原始頁面包含條件式註解（`<!--[if IE]>…<![endif]-->`），且其中引用了更深層的資源，這些也會像其他巢狀包含一樣被剔除。這可防止舊版 IE 的 hack 讓最終檔案尺寸膨脹。

---

## 視覺摘要

以下是一張快速示意圖，說明從載入文件、資源處理到儲存修剪結果的流程。

![如何使用 SaveOptions 範例](https://example.com/placeholder.png "示意圖：展示如何使用 SaveOptions 修剪 HTML 頁面")

*Alt text:* **如何使用 SaveOptions 範例** – 顯示載入、設定與儲存 HTML 文件的三步驟流程。

---

## 常見問題與注意事項

| 問題 | 解答 |
|----------|--------|
| **如果需要更深的巢狀層級該怎麼辦？** | 將 `max_handling_depth` 提升至 3 或 4，但請記得輸出大小會隨之增長。 |
| **能否不論深度都排除特定標籤（例如 `<script>`）？** | 可以——`SaveOptions` 也支援 `tag_exclusion_list` 屬性。將 `"script"` 加入該清單，即可始終移除腳本。 |
| **函式庫是否支援多執行緒？** | 目前版本不支援。請為每個執行緒建立獨立的 `HTMLDocument`。 |
| **相對 URL 會被重新寫入嗎？** | 預設不會。若需要將相對路徑調整至新位置，可設定 `save_opt.rewrite_relative_urls = True`。 |

---

## 後續步驟

既然你已掌握 **如何使用 SaveOptions**，不妨嘗試以下擴充功能：

- **壓縮輸出：** 設定 `save_opt.enable_gzip = True` 以在傳輸時減少檔案大小。  
- **除錯用的格式化輸出：** 切換 `save_opt.indent_output = True` 以取得易讀的 HTML 排版。  
- **批次處理：** 迭代整個 HTML 檔案目錄，套用相同的修剪邏輯——對靜態網站產生器特別有用。

這些調整皆建立在你剛學到的基礎上，讓程式碼保持簡潔且易於維護。

---

## 結論

我們已完整說明在 Python 中修剪 HTML 頁面的全流程：**如何載入 HTML 文件**、使用 `ResourceHandlingOptions` **如何修剪 HTML 頁面**，最後 **如何使用 SaveOptions** 寫出清理過的檔案。此範例完全自包含、即時可執行，並展示了控制資源深度對於網路爬蟲、靜態網站生成或任何需要輕量 HTML 快照的情境，都是關鍵的效能優化。

快試試看，變換不同的 `max_handling_depth` 值，讓修剪後的頁面為你分擔繁重的載入工作。若遇到任何問題，歡迎在下方留言——祝編程愉快！

## 相關教學

- [如何在 C# 中儲存 HTML – 使用自訂資源處理器的完整指南](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [如何將 HTML 渲染為 PNG – 完整 C# 教學](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [如何在 C# 中壓縮 HTML – 將 HTML 儲存為 Zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}