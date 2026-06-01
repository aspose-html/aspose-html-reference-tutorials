---
category: general
date: 2026-05-31
description: 建立 ResourceHandlingOptions 實例以控制 HTML 資源載入。了解如何限制資源深度，並使用自訂選項載入 HTMLDocument。
draft: false
keywords:
- create resourcehandlingoptions instance
- limit resource depth
- HTMLDocument options
- resource loading configuration
- python html parsing
language: zh-hant
og_description: 建立 ResourceHandlingOptions 實例以控制 HTML 資源載入。本指南說明如何設定最大處理深度以及使用自訂選項載入
  HTMLDocument。
og_title: 為 HTML 載入建立 ResourceHandlingOptions 實例
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create ResourceHandlingOptions instance to control HTML resource loading.
    Learn how to limit resource depth and load an HTMLDocument with custom options.
  headline: Create ResourceHandlingOptions Instance for HTML Loading
  type: TechArticle
tags:
- Python
- HTML parsing
- Resource handling
title: 建立 ResourceHandlingOptions 實例以載入 HTML
url: /zh-hant/python/general/create-resourcehandlingoptions-instance-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 ResourceHandlingOptions 實例以載入 HTML

有沒有想過要 **建立 ResourceHandlingOptions 實例**，才能防止巨大的 HTML 頁面把你的解析器炸掉？你不是唯一有此困擾的人——大型文件若包含多層腳本、框架或 include，會很快把簡單的爬取變成噩夢。

在本教學中，我們將一步步示範如何建立 `ResourceHandlingOptions` 物件、限制巢狀層級，並將其傳入 `HTMLDocument`。完成後，你將擁有一套乾淨、可重複使用的 **資源載入設定**，適用於任何規模的 HTML 檔案。

## 你將學到

- 為何在解析龐大頁面時 `ResourceHandlingOptions` 實例如此重要。  
- 如何 **限制資源深度**，避免無止盡的遞迴。  
- 使用自訂選項載入 `HTMLDocument` 的完整語法。  
- 一個完整、可直接執行的範例，讓你今天就能放入專案中使用。  

**先備條件：** Python 3.8+、提供 `HTMLDocument` 與 `ResourceHandlingOptions` 的 `htmlparser` 套件。除此之外不需其他相依。

---

## 步驟 1：建立 ResourceHandlingOptions 實例

首先，你需要一個全新的 `ResourceHandlingOptions` 物件。它就像是解析器在遇到外部資源（腳本、圖片、iframe 等）時的控制面板。

```python
# Step 1: Initialize the options object
options = ResourceHandlingOptions()
```

> **為什麼重要：** 若未明確建立實例，解析器會退回預設設定，通常會「載入全部」資源。對於巨大的頁面而言，這預設會消耗數 GB 記憶體，甚至卡住腳本。

---

## 步驟 2：限制資源深度

接著，我們告訴選項我們願意深入多少層。將 `max_handling_depth` 設為 5，表示解析器在超過五層巢狀資源時就會停止。依需求自行調整此數值。

```python
# Step 2: Cap the nesting depth (e.g., stop after 5 levels)
options.max_handling_depth = 5
```

> **小技巧：** 若你只關心最上層內容，深度設為 1 或 2 通常已足夠，且能大幅提升速度。

---

## 步驟 3：使用選項載入 HTML 文件

現在把已設定好的 `options` 傳給 `HTMLDocument`。建構子接受檔案路徑（或 URL）以及選項物件，讓你能精細控制哪些資源會被載入。

```python
# Step 3: Parse the HTML file using the configured options
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
```

> **執行結果會是：** 解析器會讀取 `big_page.html`，但任何會使深度超過 5 的資源都會被靜默忽略。如此可防止遞迴失控，並讓記憶體使用保持可預測。

---

## 步驟 4：驗證結果（可選但有幫助）

檢查文件是否如預期載入是一個好習慣。以下提供一個簡易的 sanity check，會印出成功處理的資源數量。

```python
# Step 4: Quick verification
print(f"Handled resources: {len(doc.resources)}")
print(f"Document title: {doc.title}")
```

**預期輸出**（實際數字會依輸入檔案而異）：

```
Handled resources: 12
Document title: Example Large Page
```

如果計數遠低於預期，可能需要提升 `max_handling_depth` 或調整其他 `ResourceHandlingOptions` 屬性。

---

## 常見變化與邊緣案例

| 情境 | 調整方式 |
|-----------|------------|
| **只想忽略圖片** | 設定 `options.ignore_images = True`。 |
| **腳本導致逾時** | 使用 `options.max_script_execution_time = 2`（秒）。 |
| **解析遠端 URL 而非本機檔案** | 像檔案路徑一樣直接將 URL 字串傳給 `HTMLDocument`。 |
| **想使用自訂 logger** | 在載入前將 `options.logger = my_logger` 指派給選項。 |

以上調整皆屬於 **HTMLDocument options** 工具箱的一部份，讓你在不重寫解析器的前提下，微調 **資源載入設定**。

---

## 完整可執行範例

將以下程式碼全部結合，即成一個可直接執行的腳本。存為 `parse_big_page.py`，然後以 `python parse_big_page.py` 執行。

```python
# parse_big_page.py
from htmlparser import HTMLDocument, ResourceHandlingOptions

def main():
    # 1️⃣ Create the options instance
    options = ResourceHandlingOptions()
    
    # 2️⃣ Limit how deep we go into nested resources
    options.max_handling_depth = 5
    
    # Optional: ignore images to speed things up
    # options.ignore_images = True
    
    # 3️⃣ Load the document with our custom options
    doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
    
    # 4️⃣ Verify the load
    print(f"Handled resources: {len(doc.resources)}")
    print(f"Document title: {doc.title}")

if __name__ == "__main__":
    main()
```

執行後，你應該會看到資源計數與標題被印出，證明已成功 **建立 ResourceHandlingOptions 實例** 並套用於解析。

---

## 結論

我們剛剛示範了如何 **建立 ResourceHandlingOptions 實例**、限制巢狀層級，並將其傳入 `HTMLDocument`。這套模式為任何大型 HTML 檔案提供可靠的 **資源載入設定**，讓 Python 的 HTML 解析既快速又省記憶體。

準備好進一步探索了嗎？試著調整深度限制、切換 `ignore_images`，或整合自訂 logger——每一次微調都能讓你更了解 **HTMLDocument options** 與資料管線的互動。

如果你覺得本指南對你有幫助，歡迎分享、為 repo 加星，或留下你的使用心得。祝你解析順利！

## 接下來該學什麼？

- [在 C# 中從字串建立 HTML – 自訂資源處理器指南](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [在 C# 中儲存 HTML – 使用自訂資源處理器的完整指南](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [在 .NET 中使用 Aspose.HTML 建立 Stream Provider](/html/english/net/advanced-features/create-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}