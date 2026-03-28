---
category: general
date: 2026-02-22
description: 自訂資源處理程式可讓您擷取 HTML 輸出。了解如何載入 HTML 文件、使用 Aspose HTML 儲存，以及透過簡單的 C# 範例將
  HTML 儲存至串流。
draft: false
keywords:
- custom resource handler
- load html document
- aspose html save
- save html to stream
- capture html output
language: zh-hant
og_description: 了解如何使用 Aspose HTML 在 C# 中，透過自訂資源處理程式擷取 HTML 輸出、載入 HTML 文件，並將 HTML
  儲存至串流。
og_title: Aspose HTML 中的自訂資源處理程式 – 儲存至串流指南
tags:
- aspose-html
- csharp
- streaming
- resource-handler
title: Aspose HTML 中的自訂資源處理程式 – 儲存至串流指南
url: /zh-hant/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 自訂資源處理程式 – 捕獲 HTML 輸出（使用 Aspose HTML）

有沒有曾經需要一個 **custom resource handler** 來攔截 Aspose HTML 在轉換過程中寫入的每一個檔案？或許你想把 HTML、圖片或 CSS 直接導入記憶體而不是寫入磁碟。這在建構必須保持無狀態的 Web 服務，或是僅想 **save HTML to stream** 以便之後處理時，是非常常見的情境。

在本教學中，我們將逐步示範一個完整、可直接執行的範例，說明如何 **load HTML document**、掛載 **custom resource handler**，以及使用 **Aspose HTML save** 來將每一個輸出項目捕獲至 `MemoryStream`。完成後，你不僅會了解每一行程式碼的「什麼」與「為什麼」，還能取得一個可在任何 C# 專案中直接使用的可重用模式。

> **Why care?**  
> 在記憶體中捕獲 HTML 輸出可避免檔案系統 I/O、降低雲端函式的延遲，並讓你完全掌控檔名、壓縮，甚至即時的轉換。

---

## 需要的環境

- **.NET 6** 或更新版本（此程式碼亦相容 .NET Framework 4.7+）。  
- **Aspose.HTML for .NET** NuGet 套件 (`Aspose.Html`)。  
- 一個簡單的 HTML 檔案（`input.html`），放在可供參考的資料夾中。  
- 任意你喜歡的 IDE——Visual Studio、Rider，或是安裝 C# 擴充功能的 VS Code。

不需要額外設定；API 會自行處理所有繁重工作。

## 步驟 1 – 建立自訂資源處理程式

此技巧的核心在於繼承 `Aspose.Html.Rendering.ResourceHandler`。透過覆寫 `HandleResource`，你可以決定每個資源串流的 **存放位置**。在本例中，我們為每個請求回傳一個全新的 `MemoryStream`，也就是說每個 CSS、圖片或子 HTML 片段皆僅存在於記憶體中。

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Custom handler that writes every resource to a new MemoryStream.
/// </summary>
class MemoryStreamHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // The ResourceInfo gives you the original URL and MIME type.
        // You could inspect it here to decide whether to skip certain files.
        // For this tutorial we just allocate a fresh stream.
        return new MemoryStream();
    }
}
```

**Pro tip:** 若需要追蹤這些串流（例如稍後寫入 ZIP 壓縮檔），可將它們存放在以 `resourceInfo.Uri` 為鍵的 `Dictionary<string, MemoryStream>` 中。

## 步驟 2 – 載入 HTML 文件

在儲存任何內容之前，你必須先 **load HTML document** 至 `HTMLDocument` 實例。Aspose HTML 能從檔案路徑、URL，甚至字串讀取。此處為了簡化，我們使用本機檔案。

```csharp
// Adjust the path to point at your real HTML file.
string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Load the source HTML document.
HTMLDocument htmlDocument = new HTMLDocument(htmlPath);
```

如果你的 HTML 參考了外部資源（圖片、字型等），請確保 base URI 正確；否則處理程式將無法找到這些資源。

## 步驟 3 – 建立自訂處理程式實例

現在我們建立先前定義的處理程式實例。沒有特別的操作——只是一個普通的 `new`。此物件將在下一步傳遞給 `Save` 方法。

```csharp
// Step 3: Instantiate the custom handler.
MemoryStreamHandler resourceHandler = new MemoryStreamHandler();
```

由於處理程式僅存在於記憶體中，你不必擔心檔案權限或磁碟清理問題。

## 步驟 4 – 使用 Aspose HTML Save 儲存文件

**Aspose HTML save** 操作接受一個 `ResourceHandler`。當引擎遍歷 DOM 並解析每個連結資源時，會呼叫 `HandleResource`。我們的實作回傳 `MemoryStream`，因此每個項目都會存於記憶體中。

```csharp
// Step 4: Save the document.
// The handler's HandleResource method will be invoked for each output stream.
htmlDocument.Save(resourceHandler);
```

此時轉換已完成，但串流仍在記憶體中。你現在可以讀取它們、寫入資料庫，或在 API 回應中返回。

## 步驟 5 – 取得並驗證捕獲的串流

由於我們每次都回傳新的 `MemoryStream`，因此需要一種方式保留參考。以下是先前處理程式的快速擴充版，會將每個串流存入字典，以便在儲存後檢查。

```csharp
class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;   // Remember the stream by its URI.
        return ms;
    }
}

// Usage:
var trackingHandler = new TrackingMemoryStreamHandler();
htmlDocument.Save(trackingHandler);

// Example: write the main HTML output to console (as text)
if (trackingHandler.Streams.TryGetValue(htmlPath, out var mainStream))
{
    mainStream.Position = 0; // rewind
    using var reader = new StreamReader(mainStream);
    string html = reader.ReadToEnd();
    Console.WriteLine("=== Rendered HTML ===");
    Console.WriteLine(html);
}
```

執行此程式碼會印出 Aspose 產生的最終 HTML，證實 **capture html output** 如預期運作。

## 邊緣情況與常見問題

### 1. 如果文件非常大？

記憶體使用量可能迅速增加。對於大型 PDF 或包含大量高解析度圖片的 HTML，建議直接串流至 `FileStream` 或 **buffered network stream**，而非 `MemoryStream`。處理程式可依據 `resourceInfo.MimeType` 來決定。

### 2. 是否需要釋放串流？

需要。完成處理後，請對每個 `MemoryStream` 呼叫 `Dispose()`（或使用 `using` 區塊自動釋放）。在追蹤範例中，我們可以加入：

```csharp
foreach (var ms in trackingHandler.Streams.Values)
    ms.Dispose();
```

### 3. 是否可以在儲存前重新命名資源？

當然可以。在 `HandleResource` 內，你可以取得 `resourceInfo.Uri`。你可以重新寫入、加上前綴，甚至回傳 `null` 以略過特定檔案。

```csharp
if (resourceInfo.MimeType.StartsWith("image/"))
    return null; // Skip images completely.
```

### 4. 此方法是否具備執行緒安全性？

單一處理程式實例不應在多個同時的 `Save` 呼叫間共享。請為每次轉換建立新的處理程式，或在必須重複使用時以鎖定方式保護內部字典。

## 完整可執行範例

以下是完整程式碼，你可以貼到 Console 應用程式中。它示範了從載入 HTML 檔案到印出捕獲輸出的全部流程。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;

class TrackingMemoryStreamHandler : ResourceHandler
{
    public Dictionary<string, MemoryStream> Streams { get; } = new();

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var ms = new MemoryStream();
        Streams[resourceInfo.Uri] = ms;
        return ms;
    }
}

class SaveToStreamTutorial
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the HTML document you want to render.
        // -------------------------------------------------
        string htmlPath = Path.Combine(Environment.CurrentDirectory, "input.html");
        if (!File.Exists(htmlPath))
        {
            Console.WriteLine($"Cannot find {htmlPath}");
            return;
        }

        HTMLDocument htmlDocument = new HTMLDocument(htmlPath);

        // -------------------------------------------------
        // Step 2: Create the custom handler that captures streams.
        // -------------------------------------------------
        var handler = new TrackingMemoryStreamHandler();

        // -------------------------------------------------
        // Step 3: Save the document – Aspose will invoke our handler.
        // -------------------------------------------------
        htmlDocument.Save(handler);

        // -------------------------------------------------
        // Step 4: Retrieve the main HTML output and display it.
        // -------------------------------------------------
        if (handler.Streams.TryGetValue(htmlPath, out var mainStream))
        {
            mainStream.Position = 0; // rewind to start
            using var reader = new StreamReader(mainStream);
            string renderedHtml = reader.ReadToEnd();
            Console.WriteLine("=== Rendered HTML Output ===");
            Console.WriteLine(renderedHtml);
        }
        else
        {
            Console.WriteLine("Main HTML stream not found.");
        }

        // -------------------------------------------------
        // Step 5: Clean up.
        // -------------------------------------------------
        foreach (var ms in handler.Streams.Values)
            ms.Dispose();

        Console.WriteLine("All streams disposed. Done.");
    }
}
```

**預期輸出：** 控制台會印出完整渲染的 HTML（包含 Aspose 可能產生的內嵌 CSS），並顯示所有串流已被釋放的確認訊息。

## 結論

你剛剛學會了如何在 Aspose HTML 中實作 **custom resource handler**、**load an HTML document**，以及 **save HTML to stream**，同時 **capturing the HTML output** 以供後續處理。此模式輕量、具執行緒意識且完全可擴充——只需幾行程式碼即可將 `MemoryStream` 替換為檔案、網路 socket，或雲端儲存 API。

接下來，你可以探索：

- **Saving to a ZIP archive**（非常適合打包 HTML、CSS 與圖片）。  
- **Applying transformations**（例如即時壓縮 CSS）。  
- **Streaming directly to an HTTP response** in ASP.NET Core，以即時下載。

試試看這些功能，你會發現量身訂做的 **custom resource handler** 在實務情境中有多強大。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}