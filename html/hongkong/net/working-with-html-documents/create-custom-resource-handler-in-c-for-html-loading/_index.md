---
category: general
date: 2026-08-15
description: 在 C# 中建立自訂資源處理程式，以管理 HTML 資源（如圖片與 CSS）。學習 HTMLLoadOptions、記憶體串流與 HTMLDocument
  載入。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: zh-hant
lastmod: 2026-08-15
og_description: 在 C# 中建立自訂資源處理程式，以控制 HTML 資源的串流方式。本教學示範 HTMLLoadOptions 的設定、記憶體串流處理，以及使用自訂邏輯載入
  HTMLDocument。
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: 在 C# 中建立自訂資源處理程式 – HTML 資源管理完整指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: 在 C# 中建立自訂資源處理程式以載入 HTML
url: /zh-hant/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立自訂資源處理程式以載入 HTML

如果你需要 **create custom resource handler** 來處理 HTML 檔案，本指南將會一步一步說明。你將學會在載入 HTML 文件時攔截圖片、CSS 以及其他資產，使用 `HTMLLoadOptions` 與基於記憶體的串流。

本教學涵蓋實作可重複使用的處理程式、設定載入選項，以及驗證資源是否正確被擷取的全部步驟。無需額外文件——只要以下程式碼與說明即可。

## 前置條件

- .NET 6.0 或更新版本
- 基本的 C# 使用經驗
- 參考提供 `HTMLDocument`、`HtmlLoadOptions` 與 `ResourceHandler` 的 HTML 處理函式庫（例如 GroupDocs.Viewer for .NET）

## 解決方案概觀

我們將會：

1. **建立自訂資源處理程式**，繼承 `ResourceHandler`。
2. 設定 `HTMLLoadOptions` 以使用此處理程式。
3. 使用 `HTMLDocument` 載入 HTML 檔案，讓處理程式為每個資源提供串流。
4. （可選）將取得的資源寫入磁碟以作驗證。

每個步驟皆附完整原始碼與背後的原理說明。

## 步驟 1：定義自訂資源處理程式類別

建立自訂處理程式即是覆寫 `HandleResource`，讓函式庫能將資源位元組寫入你自行控制的串流。使用 `MemoryStream` 可將資料保留在記憶體中，適合測試或後續處理。

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**為什麼重要：**  
覆寫 `HandleResource` 讓你完全掌控資源資料的去向。日後若需快取圖片、轉換 CSS，或記錄資源使用情況，只要把 `MemoryStream` 換成任何自訂的串流實作即可。

## 步驟 2：設定 `HTMLLoadOptions` 以使用處理程式

`HTMLLoadOptions` 允許你將處理程式插入載入流程。設定 `ResourceHandler` 屬性即可讓檢視器在遇到每個外部資產時呼叫 `MyHandler`。

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**為什麼重要：**  
若未指定 `ResourceHandler`，檢視器會將資源寫入預設位置（通常是暫存資料夾）。透過自訂處理程式，你 **create custom resource handler** 的行為即可符合應用程式的儲存策略。

## 步驟 3：使用已設定的選項載入 HTML 文件

現在載入 HTML 檔案。檢視器會對每個遇到的資源呼叫 `MyHandler.HandleResource`。

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

此時 HTML 內容已完成解析，所有外部資源皆已透過 `MyHandler` 提供的記憶體緩衝區串流。

## 步驟 4（可選）：存取擷取到的資源

若需要檢查或永久保存資源，可修改 `MyHandler`，將每個 `MemoryStream` 依資源名稱存入字典。

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

載入完成後，你可以遍歷 `handler.Resources`，將每個資源寫入磁碟：

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**為什麼重要：**  
保存資源可進行後續處理，例如影像優化、CSS 壓縮或歸檔。也能實際驗證 **create custom resource handler** 的邏輯是否如預期運作。

## 步驟 5：清理資源

`HTMLDocument` 與任何串流都應在使用完畢後釋放，以免佔用非受控資源。

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## 完整可執行範例

以下是一個獨立程式，示範從類別定義到資源抽取的全部步驟。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**預期輸出**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

主控台會列出每個由檢視器透過自訂處理程式串流的資源，證明 **create custom resource handler** 工作流程已成功。

## 常見問題與邊緣案例

| 問題 | 答案 |
|----------|--------|
| *如果資源很大（例如高解析度影像）怎麼辦？* | 改用指向暫存資料夾的 `FileStream` 取代 `MemoryStream`，可避免記憶體過度佔用。 |
| *我可以依類型過濾資源嗎？* | 在 `HandleResource` 內檢查 `info.MimeType` 或 `info.Extension`，對不需要的類型回傳 `null`。回傳 `null` 會讓檢視器跳過該資源。 |
| *需要考慮執行緒安全嗎？* | 若同一個處理程式實例會被多個併發載入共用，請使用 lock 保護 `Resources` 字典，或改用並行集合。 |
| *如何支援相對 URL？* | `ResourceInfo` 包含原始 URL，你可以在儲存前將其與 HTML 檔案的基礎路徑結合，以解析相對參照。 |

## 結論

現在你已掌握如何在 C# 中 **create custom resource handler** 以載入 HTML，設定 `HTMLLoadOptions`、擷取串流資產，並負責任地釋放資源。此模式讓你全面掌控資源管理，適用於即時影像處理、CSS 重寫或安全儲存等情境。

接下來，可探索相關主題，例如使用不同渲染選項的 **HTMLDocument loading**，或將處理程式擴充為直接寫入雲端儲存的 **C# resource handler** 實作。多加實驗 `HandleResource` 方法，讓它符合專案的特定資源工作流程。

## 接下來該學什麼？

以下教學與本指南技術緊密相關，能幫助你進一步掌握 API 功能並探索其他實作方式：

- [在 C# 中從字串建立 HTML – 自訂資源處理程式指南](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [C# 自訂資源處理程式 – 將 HTML 轉成 ZIP 教程](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [如何在 C# 中保存 HTML – 使用自訂資源處理程式的完整指南](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}