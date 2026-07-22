---
category: general
date: 2026-07-21
description: 在 Python 中建立資源處理選項，並學習如何設定 HTML 解析的最大處理深度。遵循此逐步教學，以實現可靠的資源管理。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: zh-hant
lastmod: 2026-07-21
og_description: 在 Python 中建立資源處理選項，即時查看如何設定最大處理深度以安全載入 HTML 文件。只需數分鐘即可掌握此技巧。
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: 在 Python 中建立資源處理選項 – 完整逐步指南
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: 在 Python 中創建資源處理選項 – 完整指南
url: /zh-hant/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中建立資源處理選項 – 完整指南

有沒有想過要 **建立資源處理選項** 來處理巨大的 HTML 頁面而不會耗盡記憶體？你並不是唯一有此困擾的人。當你把龐大的文件餵給解析器時，像是 frames、iframes 或是外部 CSS 等巢狀資源很快就會失控。  

好消息是？你可以告訴解析器在達到特定的巢狀層級後停止。在本教學中，我們將示範 **如何設定最大處理深度**，讓你的應用程式保持回應。準備好了嗎？讓我們一起深入探討。

## 你將學到什麼

- 為什麼限制巢狀深度對效能與安全性很重要。  
- 使用 `ResourceHandlingOptions` 類別 **建立資源處理選項** 的完整程式碼。  
- 如何設定 `max_handling_depth`，讓解析器在三層後停止。  
- 處理邊緣案例的技巧，例如文件中出現循環參照或缺少資源的情況。  

不需要事先熟悉此函式庫——只要有可執行的 Python 3 環境以及基本的檔案 I/O 概念即可。

## 前置條件

- Python 3.8+（此函式庫相容於所有近期版本）。  
- 提供 `HTMLDocument` 與 `ResourceHandlingOptions` 的 `htmlparser` 套件。  
- 一個範例 HTML 檔案（`big_page.html`），放在可供參照的資料夾內。  

如果尚未安裝套件，請執行：

```bash
pip install htmlparser
```

基礎工作完成後，讓我們進入正題。

## 建立資源處理選項 – 步驟 1

首先，你需要一個 `ResourceHandlingOptions` 的實例。把它想成一個工具箱，裡面可以設定解析器應遵守的限制與政策。

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**為什麼這很重要：**  
當解析器在 `<iframe>` 內再次遇到 `<iframe>` 時，預設會無止盡地追蹤下去。將深度上限設為 `3` 後，就能防止遞迴失控，避免耗盡記憶體或產生堆疊溢位。  

> **專業提示：** 若你在解析不可信的內容（例如使用者上傳的 HTML），建議將深度降低至 `1` 或 `2`，以減少潛在攻擊風險。

## 載入 HTML 文件 – 步驟 2

準備好選項物件後，將它傳入 `HTMLDocument`。建構子會遵守你剛設定的 `max_handling_depth`。

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**背後發生了什麼？**  
`HTMLDocument` 會讀取檔案、建立 DOM 樹，然後遍歷每一個外部資源（樣式表、腳本、圖片）。每當遇到巢狀資源時，會檢查 `resource_options.max_handling_depth`。若已達上限，解析器會記錄警告並跳過更深的巢狀。  

這表示你可以取得前三層的完整 DOM，剩餘的部分則安全地被忽略。

## 驗證設定 – 步驟 3

確認設定是否生效總是好主意。`resource_options` 物件會公開目前狀態，你可以將它印出或在測試中斷言。

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

如果斷言通過，你就可以放心，解析器在整個執行過程中都會遵守此上限。

## 處理邊緣案例

### 循環參照

某些舊版網站會嵌入指向原始頁面的 iframe，形成迴圈。設定 `max_handling_depth` 後，迴圈會在第三次迭代自動中斷。但你仍可能在日誌中看到警告。若要靜音這類訊息，可調整 logger 等級：

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### 缺少資源

如果巢狀資源載入失敗（404 或網路逾時），預設會拋出例外。將載入呼叫包在 `try/except` 區塊中，以免程式當掉：

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### 動態調整深度

有時不同的管線階段需要不同的深度。因為 `resource_options` 是可變物件，你可以在執行時即時修改 `max_handling_depth`：

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

只要記得在另一個執行緒重新使用同一個選項實例前，先將值重設回原本的設定。

## 完整範例程式

以下是一個可直接複製、調整檔案路徑後立即執行的完整腳本。

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**預期輸出（當檔案存在且格式正確時）：**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

若檔案無法讀取，系統會顯示錯誤訊息而不是直接崩潰。

![Create resource handling options in Python](/images/resource-options.png){alt="在 Python 中建立資源處理選項"}

## 重點回顧 – 為什麼這個方法很讚

- **安全第一：** 限制巢狀深度可防止遞迴失控與記憶體膨脹。  
- **彈性高：** 可在執行時調整 `max_handling_depth`，因應不同情境。  
- **簡單易用：** 幾行程式碼即可 **建立資源處理選項** 並立即套用。  

總之，你現在掌握了一套穩健的模式，能控制解析器追蹤外部資源的深度。

## 接下來可以做什麼？

- 深入探索 `ResourceHandlingOptions` 類別——它還提供快取、逾時處理與 MIME‑type 過濾等旗標。  
- 結合深度限制與自訂 `UserAgent` 字串，避免被嚴格的伺服器封鎖。  
- 若你使用非同步 I/O，可參考 `aiohtmlparser` 變體，它遵守相同選項且相容 `asyncio`。  

歡迎自行實驗：將深度設為 `0`，觀察解析器如何忽略所有外部參照。這在只需要原始 HTML 標記時非常方便。

有任何問題或遇到仍會卡住的頁面嗎？在下方留言，我會樂於協助你微調設定。祝你解析愉快！

## 接下來該學什麼？

以下教學與本指南的技巧密切相關，能幫助你在自己的專案中進一步掌握 API 功能與替代實作方式，每篇都附有完整可執行的程式碼範例與逐步說明。

- [在 C# 中從字串建立 HTML – 自訂資源處理器指南](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [如何在 C# 中儲存 HTML – 使用自訂資源處理器的完整指南](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [在 Java 中為 HTML 建立沙盒 – 步驟說明指南](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}