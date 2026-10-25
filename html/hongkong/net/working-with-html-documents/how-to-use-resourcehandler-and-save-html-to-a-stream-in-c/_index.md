---
category: general
date: 2026-10-25
description: 如何使用 ResourceHandler 來控制資源載入，以及如何使用 Aspose.HTML 在 C# 中將 HTML 儲存至串流。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use resourcehandler
- how to save html to stream
- Aspose.HTML ResourceHandler
- HTML to MemoryStream C#
- custom resource handling C#
language: zh-hant
lastmod: 2026-10-25
og_description: 如何使用 ResourceHandler 控制資源載入，以及如何使用 Aspose.HTML for .NET 將 HTML 儲存至串流。
og_image_alt: Screenshot of C# code using ResourceHandler to save HTML to a memory
  stream
og_title: 如何在 C# 中使用 ResourceHandler 並將 HTML 儲存至串流
schemas:
- author: Aspose
  dateModified: '2026-10-25'
  description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  headline: How to use ResourceHandler and save HTML to a stream in C#
  type: TechArticle
- description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  name: How to use ResourceHandler and save HTML to a stream in C#
  steps:
  - name: Expected output
    text: 'Running the code above prints:'
  - name: 1. Embedding real resources
    text: 'If you need to embed an image, modify `MyHandler` to return a stream that
      contains the image bytes:'
  - name: 2. Handling large documents
    text: For very large HTML files, consider using `BufferedStream` or writing directly
      to a file‑based `FileStream` if memory becomes a bottleneck. The pattern for
      **how to save HTML to a stream** stays the same; only the stream type changes.
  - name: 3. Thread safety
    text: '`ResourceHandler` instances are **not** guaranteed to be thread‑safe. If
      you plan to reuse a handler across parallel conversions, either:'
  - name: 4. Disposing resources
    text: Both `HTMLDocument` and any streams you create implement `IDisposable`.
      Wrapping them in `using` blocks, as shown in Step 4, guarantees clean release
      of unmanaged resources.
  - name: What’s next?
    text: '* **Embed real images or CSS** by extending `MyHandler` (see the “Embedding
      real resources” section). * **Convert the stream to PDF** with `HtmlConverter.ConvertHtml`
      if you need a printable version. * **Stream the result directly from a Web API**
      using `FileStreamResult` or `MemoryStream` in ASP.NE'
  type: HowTo
tags:
- Aspose.HTML
- C#
- Stream handling
title: 如何使用 ResourceHandler 並在 C# 中將 HTML 儲存至串流
url: /zh-hant/net/working-with-html-documents/how-to-use-resourcehandler-and-save-html-to-a-stream-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 ResourceHandler 並將 HTML 儲存至串流

如果您需要在使用 Aspose.HTML 渲染 HTML 時 **how to use ResourceHandler**，本指南將為您展示一個完整、可直接執行的解決方案。您還將學習 **how to save HTML to a stream**，以便在不觸及檔案系統的情況下傳輸輸出。

在記憶體中處理 HTML 是在即時產生電子郵件、API 回應或 PDF 時的常見做法。完成本教學後，您將擁有一個獨立的 C# 程式，能建立 `HTMLDocument`、提供自訂的 `ResourceHandler`，並將結果寫入 `MemoryStream`。

## 前置條件

* .NET 6.0 或更新版本（此程式碼亦相容於 .NET Core 3.1 與 .NET Framework 4.7+）
* **Aspose.HTML for .NET** NuGet 套件  
  ```bash
  dotnet add package Aspose.HTML
  ```
* 具備基本的 C# async/await 概念（非必須，但有助於理解）

## 本教學涵蓋內容

* 如何 **how to use ResourceHandler** 以攔截圖片、CSS 或腳本請求
* 如何使用自訂處理程式設定 `HtmlSaveOptions`
* 如何 **how to save HTML to a stream** 使用 `MemoryStream`
* 處理邊緣案例，例如資源缺失與串流釋放
* 延伸處理程式以後續嵌入真實資源的技巧

## 步驟 1：從字串建立簡易 HTML 文件

第一步是從原始 HTML 文字實例化 `HTMLDocument`。此物件代表 Aspose.HTML 會渲染的 DOM 樹。

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System.IO;

// Simple HTML markup – you can replace this with any valid HTML string.
string htmlContent = "<html><body>Hello World</body></html>";

// The HTMLDocument constructor parses the string into a DOM.
HTMLDocument document = new HTMLDocument(htmlContent);
```

> **為何重要：** 從字串建立文件可將整個工作流程保留在記憶體中，這在您之後 **how to save HTML to a stream** 而不觸及磁碟時尤為關鍵。

## 步驟 2：實作自訂 ResourceHandler

`ResourceHandler` 是 Aspose.HTML 在需要外部資源（圖片、CSS、字型等）時使用的掛鉤。透過覆寫 `HandleResource`，您可以決定對每個請求回傳哪個串流。

```csharp
// Define a handler that supplies an empty stream for every resource request.
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Returning an empty MemoryStream effectively disables external resources.
        // You could return a real image stream here if you need to embed assets.
        return new MemoryStream();
    }
}

// Instantiate the handler so it can be attached to the save options.
MyHandler customHandler = new MyHandler();
```

> **可能需要的原因：** 在為電子郵件或 API 回應產生 HTML 時，通常不希望發出外部呼叫。提供空的串流可避免 404 錯誤並加速渲染。此範例示範 **how to use ResourceHandler** 以產生「無資源」的輸出。

## 步驟 3：設定 HtmlSaveOptions 以使用自訂處理程式

`HtmlSaveOptions` 讓您掌控儲存過程。將 `ResourceHandler` 屬性指派為您自訂的實作即可。

```csharp
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Attach the handler so every resource request goes through MyHandler.
    ResourceHandler = customHandler
};
```

> **提示：** 若之後需要嵌入 CSS 或圖片，請將 `MyHandler` 換成根據 `resource.Uri` 回傳相應串流的版本。

## 步驟 4：將文件儲存至 MemoryStream

現在您已具備所有條件，可 **how to save HTML to a stream**。使用 `MemoryStream` 可將輸出保留在記憶體中，方便透過 HTTP 傳送、存入資料庫，或傳遞給其他 API。

```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    // The Save method writes the HTML (and any referenced resources) into the stream.
    document.Save(outputStream, saveOptions);

    // Reset the position so callers can read from the beginning.
    outputStream.Position = 0;

    // Example: Convert the stream to a string for debugging.
    using (StreamReader reader = new StreamReader(outputStream))
    {
        string resultHtml = reader.ReadToEnd();
        System.Console.WriteLine(resultHtml);
    }

    // At this point, outputStream can be returned from a web API, attached to an email,
    // or passed to another component without ever touching the file system.
}
```

### 預期輸出

執行上述程式碼會輸出：

```html
<html><head></head><body>Hello World</body></html>
```

由於自訂處理程式回傳空的串流，外部的 `<link>` 或 `<img>` 標籤不會被解析，HTML 仍保持乾淨。

## 常見變化與邊緣案例

### 1. 嵌入真實資源

若需嵌入圖片，請修改 `MyHandler`，使其回傳包含圖片位元組的串流：

```csharp
public override Stream HandleResource(Resource resource)
{
    if (resource.Uri.EndsWith(".png"))
    {
        // Load the PNG from embedded resources or a database.
        byte[] imageBytes = File.ReadAllBytes("logo.png");
        return new MemoryStream(imageBytes);
    }
    return new MemoryStream(); // Fallback for other resources.
}
```

### 2. 處理大型文件

對於非常大的 HTML 檔案，若記憶體成為瓶頸，可考慮使用 `BufferedStream` 或直接寫入基於檔案的 `FileStream`。**how to save HTML to a stream** 的模式保持不變，僅串流類型不同。

### 3. 執行緒安全性

`ResourceHandler` 實例 **不保證** 為執行緒安全。若打算在平行轉換中重複使用同一處理程式，請：

* 為每次轉換建立新處理程式，或
* 在 `HandleResource` 內使用鎖定保護共享狀態。

### 4. 釋放資源

`HTMLDocument` 與您建立的任何串流皆實作 `IDisposable`。如同步驟 4 所示，將它們包在 `using` 區塊中，可確保未受管理資源的乾淨釋放。

## 專業提示：重複使用同一 MemoryStream

若需將多個 HTML 輸出串接成單一串流，請在每次 `Save` 呼叫前重設位置：

```csharp
outputStream.Position = 0; // Clear previous content
document.Save(outputStream, saveOptions);
```

或者，為每次轉換建立全新的 `MemoryStream`，以避免意外的資料混合。

## 完整可執行範例

以下是完整程式碼，您可直接複製貼上至主控台應用程式。它可於 .NET 6.0 與 Aspose.HTML 23.9（或更新版本）編譯通過。

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System;
using System.IO;

namespace ResourceHandlerDemo
{
    // Custom handler that supplies empty streams for any requested resource.
    class MyHandler : ResourceHandler
    {
        public override Stream HandleResource(Resource resource)
        {
            // Return an empty stream to suppress external resources.
            return new MemoryStream();
        }
    }

    class Program
    {
        static void Main()
        {
            // Step 1: Create the HTML document.
            string htmlContent = "<html><body>Hello World</body></html>";
            HTMLDocument document = new HTMLDocument(htmlContent);

            // Step 2: Attach the custom ResourceHandler.
            MyHandler customHandler = new MyHandler();

            // Step 3: Configure save options.
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                ResourceHandler = customHandler
            };

            // Step 4: Save to a MemoryStream.
            using (MemoryStream outputStream = new MemoryStream())
            {
                document.Save(outputStream, saveOptions);
                outputStream.Position = 0;

                // Display the generated HTML for verification.
                using (StreamReader reader = new StreamReader(outputStream))
                {
                    string resultHtml = reader.ReadToEnd();
                    Console.WriteLine("Generated HTML:");
                    Console.WriteLine(resultHtml);
                }
            }
        }
    }
}
```

執行程式後，您會在主控台看到產生的 HTML，證實 **how to use ResourceHandler** 與 **how to save HTML to a stream** 能無縫協同運作。

## 結論

本教學示範了 **how to use ResourceHandler** 以控制外部資源載入，以及使用 Aspose.HTML 在 C# 中 **how to save HTML to a stream** 的完整步驟。您現在擁有一套可重複使用的記憶體內 HTML 產生模式，非常適合 Web API、電子郵件範本與 PDF 轉換流程。

### 接下來？

* 透過擴充 `MyHandler`（參見「嵌入真實資源」章節）**嵌入真實圖片或 CSS**。
* 若需可列印的版本，使用 `HtmlConverter.ConvertHtml` **將串流轉換為 PDF**。
* 在 Web API 中使用 `FileStreamResult` 或 ASP.NET 的 `MemoryStream` **直接串流結果**。

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [如何在 C# 中儲存 HTML – 使用自訂資源處理程式的完整指南](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [如何在 C# 中使用自訂資源處理程式儲存 HTML](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [如何在 Aspose.HTML 中使用處理程式 – 載入 HTML、儲存為 ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-handler-in-aspose-html-load-html-save-as-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}