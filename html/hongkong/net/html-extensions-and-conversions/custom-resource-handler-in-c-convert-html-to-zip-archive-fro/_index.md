---
category: general
date: 2026-02-13
description: 學習如何在 C# 中建立自訂資源處理程式，將 HTML 轉換為 ZIP 壓縮檔，使用 Aspose.HTML 從記憶體產生 ZIP – 步驟教學
draft: false
keywords:
- custom resource handler
- convert html zip archive
- create zip from memory
- Aspose HTML
- in‑memory streaming
- C# zip compression
language: zh-hant
og_description: 發現完整的 C# 解決方案，使用自訂資源處理程式將 HTML 直接於記憶體中轉換為 ZIP 壓縮檔。
og_title: 自訂資源處理程式 – 從記憶體將 HTML 轉換為 ZIP
tags:
- C#
- Aspose.HTML
- ZipArchive
- MemoryStream
title: C# 自訂資源處理程式 – 從記憶體將 HTML 轉換為 ZIP 壓縮檔
url: /zh-hant/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-archive-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 自訂資源處理程式 – 從記憶體將 HTML 轉換為 ZIP 壓縮檔

是否曾需要一個 **custom resource handler** 來抓取 HTML 頁面所載入的每張圖片、CSS 檔案或腳本，然後在不寫入磁碟的情況下將所有內容壓縮？您並非唯一有此需求的人。在許多網頁自動化或電子郵件範本的情境中，您希望將整個頁面打包成單一、可攜帶的檔案，且為了效能與安全性，更願意將所有資料保留在 RAM 中。

在本教學中，我們將逐步說明一個完整且可執行的範例，展示如何使用 **custom resource handler** 來 **convert HTML zip archive**，以及如何使用 .NET 的 `System.IO.Compression` **create zip from memory**。完成後，您將擁有一個可自行嵌入任何使用 Aspose.HTML 的 C# 專案的獨立方法。

## 您需要的環境

- .NET 6+（或 .NET Framework 4.7.2+）  
- Aspose.HTML for .NET（NuGet 套件 `Aspose.HTML`）  
- 具備基本的串流與 `ZipArchive` 類別概念  

不需任何外部工具或暫存檔案，純粹在記憶體中處理。

## 步驟 1：定義 Custom Resource Handler

此解決方案的核心是一個繼承自 `Aspose.Html.ResourceHandler` 的類別。它的工作是為 HTML 引擎請求的每個外部資源提供一個全新的 `Stream`。每次回傳新的 `MemoryStream`，即可將資料隔離，並在之後打包時使用。

```csharp
using System.IO;
using Aspose.Html;

// Step 1 – Custom handler that stores resources in memory
class MemoryResourceHandler : ResourceHandler
{
    // The framework calls this method for every external resource (images, CSS, etc.)
    public override Stream HandleResource(Resource resource)
    {
        // We give the engine an empty stream; later we’ll fill it with the actual bytes.
        // Using MemoryStream means everything stays in RAM.
        return new MemoryStream();
    }
}
```

**為什麼這很重要：**  
如果讓 Aspose.HTML 將資源寫入磁碟，之後就必須自行清理。使用記憶體內的處理程式可消除 I/O 開銷，並使程式在沙箱環境（例如 Azure Functions）中更安全。

## 步驟 2：載入 HTML 文件

接著，將 Aspose.HTML 指向您想要打包的 HTML 檔案。文件可以位於磁碟、URL，甚至是原始字串。此處為了簡化示範，我們使用檔案路徑。

```csharp
using Aspose.Html;

// Step 2 – Load the source HTML
HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/input.html");
```

> **小技巧：** 若您的 HTML 參照相對資源，請確保 `input.html` 與那些資產位於同一資料夾，否則 handler 無法找到它們。

## 步驟 3：設定 Handler 並儲存至 MemoryStream

現在我們建立 handler 實例，並透過 `HtmlSaveOptions.OutputStorage` 告訴 Aspose.HTML 使用它。最終產生的 HTML（包含重新寫入的資源 URL）會寫入 `MemoryStream`。

```csharp
using Aspose.Html.Saving;
using System.IO;

// Step 3 – Prepare the handler and an in‑memory buffer for the final HTML
var resourceHandler = new MemoryResourceHandler();

using (MemoryStream htmlMemoryStream = new MemoryStream())
{
    document.Save(htmlMemoryStream, new HtmlSaveOptions
    {
        OutputStorage = resourceHandler // redirects all resources to the handler
    });

    // At this point htmlMemoryStream contains the full HTML file,
    // while each external resource resides in the streams returned by the handler.
```

**背後發生了什麼？**  
當執行 `document.Save` 時，Aspose.HTML 會向 `MemoryResourceHandler` 索取每個資源的串流。因為我們回傳的是空的 `MemoryStream`，引擎會直接將原始位元組寫入記憶體。不會產生暫存檔案。

## 步驟 4：在記憶體中完整組裝 ZIP 壓縮檔

現在進入有趣的部分：我們將建立一個位於另一個 `MemoryStream` 內的 `ZipArchive`。這讓我們能 **create zip from memory**，且完全不觸及檔案系統。

```csharp
    // Step 4 – Build the ZIP archive in memory
    using (MemoryStream zipMemoryStream = new MemoryStream())
    using (var zipArchive = new ZipArchive(zipMemoryStream, ZipArchiveMode.Create, leaveOpen: true))
    {
        // 4a – Add the main HTML file
        var htmlEntry = zipArchive.CreateEntry("index.html");
        using (var entryStream = htmlEntry.Open())
        {
            // Reset the position of the HTML stream before copying
            htmlMemoryStream.Position = 0;
            htmlMemoryStream.CopyTo(entryStream);
        }

        // 4b – Add each resource that the handler captured
        // The handler stored each resource in a fresh MemoryStream, which we can enumerate.
        // For demonstration, assume we kept a list of those streams (you could store them in a dictionary).
        // Example placeholder – replace with your actual collection:
        // foreach (var kvp in capturedResources)
        // {
        //     var resourceEntry = zipArchive.CreateEntry(kvp.Key); // kvp.Key = relative path
        //     using var entry = resourceEntry.Open();
        //     kvp.Value.Position = 0;
        //     kvp.Value.CopyTo(entry);
        // }

        // When we’re done, flush everything
        zipArchive.Dispose(); // optional because of using, but makes intent clear
    }

    // At this stage zipMemoryStream holds the complete ZIP file.
    // You can return it, write it to a response stream, or save it to disk if you wish.
}
```

> **注意：** 註解掉的程式碼段示範了如何在 `MemoryResourceHandler` 內收集串流。在正式環境中，您會將每個 `MemoryStream` 依原始資源 URL 作為鍵存入字典，然後在此迭代加入壓縮檔。

**為什麼要將 ZIP 保留在記憶體中？**  
將壓縮檔存放於 `MemoryStream`，可輕鬆直接傳送給 HTTP 用戶端（如 ASP.NET Core 的 `FileResult`）或上傳至雲端儲存，而不需中間檔案。

## 步驟 5：（可選）將 ZIP 寫入磁碟

如果仍需要實體檔案（例如除錯用），只要將 `zipMemoryStream` 寫入磁碟即可：

```csharp
// Optional: write the in‑memory ZIP to a file for inspection
File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipMemoryStream.ToArray());
```

## 完整範例程式

將上述所有步驟整合起來，以下是一個可直接複製貼上的程式，能 **converts HTML to a ZIP archive** 完全在記憶體中執行。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class MemoryResourceHandler : ResourceHandler
{
    // Capture each resource in a dictionary for later retrieval
    public static readonly System.Collections.Generic.Dictionary<string, MemoryStream> Captured = new();

    public override Stream HandleResource(Resource resource)
    {
        var ms = new MemoryStream();
        // Store the stream using the resource's absolute URL as the key
        Captured[resource.Uri.AbsoluteUri] = ms;
        return ms;
    }
}

class Program
{
    static void Main()
    {
        // Load the HTML file
        HtmlDocument doc = new HtmlDocument("YOUR_DIRECTORY/input.html");

        // Attach the custom handler
        var handler = new MemoryResourceHandler();

        // Save HTML + resources to memory
        using var htmlStream = new MemoryStream();
        doc.Save(htmlStream, new HtmlSaveOptions { OutputStorage = handler });

        // Create the ZIP archive in memory
        using var zipStream = new MemoryStream();
        using (var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, true))
        {
            // Add the HTML file
            var htmlEntry = zip.CreateEntry("index.html");
            using (var entry = htmlEntry.Open())
            {
                htmlStream.Position = 0;
                htmlStream.CopyTo(entry);
            }

            // Add each captured resource
            foreach (var kvp in MemoryResourceHandler.Captured)
            {
                // Derive a sane relative path from the URL
                var uri = new Uri(kvp.Key);
                var relativePath = uri.AbsolutePath.TrimStart('/');
                var resEntry = zip.CreateEntry(relativePath);
                using var entry = resEntry.Open();
                kvp.Value.Position = 0;
                kvp.Value.CopyTo(entry);
            }
        }

        // The ZIP is ready – write it out or return it from a web API
        File.WriteAllBytes("YOUR_DIRECTORY/output.zip", zipStream.ToArray());

        Console.WriteLine("HTML successfully packaged into output.zip");
    }
}
```

### 預期結果

執行程式會產生 `output.zip`，內容包括：

- `index.html` – 重新寫入的 HTML，指向已打包的資源。  
- 原始頁面引用的所有圖片、CSS 與 JavaScript 檔案，依其原始相對路徑儲存。

從 ZIP 中取出 `index.html` 並在任何瀏覽器開啟，即可看到頁面呈現與檔案系統上時完全相同。

## 常見問題與邊緣案例

| 問題 | 答案 |
|----------|--------|
| **如果資源很大（例如影片）會怎樣？** | 因為所有資料都存於記憶體，過大的檔案可能導致 `OutOfMemoryException`。此時可直接串流至暫存檔，或限制可接受的檔案大小。 |
| **需要處理重複的資源 URL 嗎？** | handler 的字典會覆寫重複項目。若只想保留一份，可在加入前檢查 `Captured.ContainsKey`。 |
| **可以在 ASP.NET Core 控制器中使用嗎？** | 當然可以。於動作方法中回傳 `File(zipStream.ToArray(), "application/zip", "page.zip")`。 |
| **HTTPS 資源怎麼處理？** | 只要執行環境信任 SSL 憑證，Aspose.HTML 會自動下載 HTTPS 資源。若為自簽憑證，需設定 `ServicePointManager.ServerCertificateValidationCallback`。 |
| **自訂 handler 是執行緒安全的嗎？** | 此範例使用 static 字典，*不是*執行緒安全的。若需同時處理多個文件，請將存取包在 lock 中，或改用 `ConcurrentDictionary`。 |

## 生產環境使用的專業建議

- **重複使用 handler** 僅限單一文件；每個請求都建立新實例，以避免使用者之間的交叉影響。  
- **盡快釋放串流**。雖然 `using` 區塊已處理大多數情況，但字典中儲存的串流仍需在 ZIP 建立完成後釋放。  
- **在處理前驗證 HTML**，以捕捉可能導致 handler 請求非預期資源的錯誤標記。  
- **積極壓縮**：若檔案大小重要，請將 `ZipArchiveEntry.CompressionLevel = CompressionLevel.Optimal` 設為最佳壓縮等級。  

## 結論

我們已說明如何使用 **custom resource handler** 逐步處理 HTML 頁面、捕獲所有相關資源，並 **create zip from memory**，全程不觸及磁碟。此模式具彈性，可應用於 Web 服務、背景工作，甚至需要發佈自包含 HTML 包的桌面工具。

不妨試試看——將 `YOUR_DIRECTORY/input.html` 換成任意頁面，調整 handler 以使用 `ConcurrentDictionary` 儲存資源，即可擁有一條穩健的記憶體內 HTML‑to‑ZIP 流程，隨時投入生產環境。

---

*想更上一層樓嗎？* 接下來，可探索如何使用 Aspose.HTML **convert HTML to PDF**，或嘗試加密 ZIP 以提升安全性。掌握 C# 記憶體串流後，無所不能。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}