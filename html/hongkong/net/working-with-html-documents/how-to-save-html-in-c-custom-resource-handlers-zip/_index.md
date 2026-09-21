---
category: general
date: 2026-01-07
description: 學習如何在 C# 中使用自訂資源處理程式儲存 HTML，以及如何建立 ZIP 壓縮檔——一步一步的完整程式碼指南。
draft: false
keywords:
- how to save html
- how to create zip
- custom resource handler
- c# zip archive example
- save html to zip
language: zh-hant
og_description: 探索如何在 C# 中儲存 HTML 並使用自訂資源處理程式建立 ZIP 檔案。提供完整程式碼、說明與最佳實踐技巧。
og_title: 如何在 C# 中儲存 HTML – 完整指南
tags:
- C#
- Aspose.Html
- ZIP
- ResourceHandler
title: 如何在 C# 中儲存 HTML – 自訂資源處理程式與 ZIP
url: /zh-hant/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中儲存 HTML – 自訂資源處理程式與 ZIP

有沒有想過 **如何在 C# 中儲存 HTML** 而不觸及檔案系統？也許你需要這段標記作為電子郵件範本，或是想直接將它串流到瀏覽器。無論哪種情況，問題都是相同的：你擁有一個 `HTMLDocument` 物件，但不知道輸出該放到哪裡。

事實上，Aspose.Html 讓這件事變得非常簡單，但你仍需決定如何處理每個產生的資源（樣式表、圖片等）。在本指南中，我們將逐步說明一個完整的解決方案，不僅展示 **如何在記憶體中儲存 HTML**，還示範如何使用自訂的 `ResourceHandler` **建立 ZIP** 壓縮檔。完成後，你將擁有一個可重複使用的模式，適用於任何 HTML 轉 ZIP 的情境。

我們將涵蓋：

* 使用 `MemoryResourceHandler` 儲存 HTML 的基礎。
* 建構 `ZipResourceHandler`，將每個資源串流至 `ZipArchive`。
* 完整、可執行的 C# 範例，可直接放入 Console 應用程式。
* 提示、邊緣案例以及你可能遇到的常見陷阱。

不需要外部文件說明——所有你需要的資訊就在此。

---

## 前置條件

在深入之前，請確保你已具備：

* .NET 6 或更新版本（程式碼在 .NET Core 與 .NET Framework 上皆可執行）。
* **Aspose.HTML for .NET** NuGet 套件（`Aspose.Html`）。
* 基本的 C# 串流與 `System.IO.Compression` 命名空間的認識。

就這樣——不需要額外工具，也沒有隱藏的設定。

## 步驟 1：在記憶體中建立簡易 HTML 文件

首先，我們需要一個 `HTMLDocument` 實例。可將其視為頁面的記憶體內部表示。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

// Step 1 – Build a tiny HTML document
var html = new HTMLDocument("<html><body>Hello, world!</body></html>");
```

> **為何重要：** 透過程式碼建構文件，我們避免了任何檔案系統的依賴，這正是 **如何儲存 HTML** 以供後續處理的核心。

## 步驟 2：實作基於記憶體的資源處理程式

Aspose.HTML 會為每個需要寫入的資源（主 HTML 檔、CSS、圖片等）呼叫 `ResourceHandler`。我們的第一個處理程式每次都回傳一個全新的 `MemoryStream`——非常適合在不持久化的情況下捕獲 HTML。

```csharp
// Step 2 – MemoryResourceHandler returns a new MemoryStream for each resource
class MemoryResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Each call gets its own stream, so resources don’t collide.
        return new MemoryStream();
    }
}
```

> **專業提示：** 若你只在乎主要的 HTML 輸出，可忽略其他串流。它們會在 `using` 區塊結束時自動釋放。

現在我們真的可以將 **HTML 儲存** 到記憶體中：

```csharp
// Step 3 – Save the document using the memory handler
using var memoryHandler = new MemoryResourceHandler();
html.Save(memoryHandler, SaveFormat.Html);
```

此時 HTML 已存在於記憶體串流中，隨時可用於接下來的任何操作——透過 HTTP 傳送、嵌入 PDF，或壓縮成 ZIP。

## 步驟 3：建構支援 ZIP 的資源處理程式（如何建立 ZIP）

如果你需要將 HTML 及其所有相關檔案打包成單一壓縮檔，就需要一個直接寫入 `ZipArchive` 的處理程式。這裡我們將示範 **如何程式化建立 zip**。

```csharp
// Step 4 – ZipResourceHandler streams each resource into a ZipArchive entry
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(Stream zipStream)
    {
        // leaveOpen:true so the outer FileStream stays alive after disposing the archive
        _zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        // Create a zip entry that mirrors the resource's name (e.g., "index.html")
        var entry = _zip.CreateEntry(info.Name);
        return entry.Open(); // Returns a stream that writes directly into the zip entry
    }

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zip.Dispose();
        base.Dispose(disposing);
    }
}
```

> **為何使用自訂處理程式？** 預設的檔案系統處理程式會寫入磁碟，這在雲原生情境下可能不想要。透過插入 `ZipResourceHandler`，你可以將所有內容保留在記憶體中，產生乾淨且可攜帶的壓縮檔。

現在我們將所有元件結合起來：

```csharp
// Step 5 – Write HTML + resources into a ZIP file on disk
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
using var zipFile = new FileStream(outputPath, FileMode.Create);
using var zipHandler = new ZipResourceHandler(zipFile);

// Save the same HTML document, but this time everything streams into the ZIP.
html.Save(zipHandler, SaveFormat.Html);
```

當 `using` 區塊結束時，你會得到 `output.zip`，其中包含 `index.html`（或 Aspose 所選的任何名稱）以及所有相關的 CSS 或圖片檔案。

## 完整可執行範例

以下是完整程式碼，你可以直接貼到新的 Console 專案中。它示範了 **如何儲存 HTML**、**如何建立 ZIP**，並展示了一個 **自訂資源處理程式**，可於其他地方重複使用。

```csharp
// ---------------------------------------------------------------
// Full C# example: Save HTML to memory and package it into a ZIP
// ---------------------------------------------------------------
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a simple HTML document
        var html = new HTMLDocument("<html><body>Hello, world!</body></html>");

        // 2️⃣ Save HTML to a MemoryStream (how to save html in memory)
        using var memoryHandler = new MemoryResourceHandler();
        html.Save(memoryHandler, SaveFormat.Html);
        Console.WriteLine("HTML saved to memory successfully.");

        // 3️⃣ Package HTML + resources into a ZIP file (how to create zip)
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        using var zipStream = new FileStream(zipPath, FileMode.Create);
        using var zipHandler = new ZipResourceHandler(zipStream);
        html.Save(zipHandler, SaveFormat.Html);
        Console.WriteLine($"ZIP archive created at: {zipPath}");
    }
}

// --------------------
// MemoryResourceHandler – captures each resource in a fresh MemoryStream
// --------------------
class MemoryResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info) => new MemoryStream();
}

// --------------------
// ZipResourceHandler – streams resources into a ZipArchive entry
// --------------------
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(Stream zipStream)
    {
        _zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(ResourceInfo info)
    {
        var entry = _zip.CreateEntry(info.Name);
        return entry.Open();
    }

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zip.Dispose();
        base.Dispose(disposing);
    }
}
```

**預期輸出**

```
HTML saved to memory successfully.
ZIP archive created at: C:\YourProject\output.zip
```

開啟 `output.zip` 後，你會看到一個 `index.html` 檔案（名稱可能會不同），其中包含字串 *Hello, world!*。

## 常見問題與邊緣案例

### 如果我的 HTML 參考外部圖片或 CSS 檔案呢？

`ResourceHandler` 會為每個外部資產收到一個 `ResourceInfo` 物件。我們的 `ZipResourceHandler` 會自動建立相對應的條目，只要在儲存時路徑可達，ZIP 就會包含這些檔案。若資源無法載入，Aspose 會跳過並記錄警告——不會導致程式崩潰。

### 我可以直接將 ZIP 串流至 HTTP 回應嗎？

絕對可以。不要寫入 `FileStream`，而是將 `HttpResponse.Body`（或 ASP.NET 中的 `Response.OutputStream`）傳給 `ZipResourceHandler`。由於處理程式直接寫入提供的串流，壓縮檔會即時產生，且不會觸及磁碟。

```csharp
using var zipHandler = new ZipResourceHandler(HttpContext.Response.Body);
html.Save(zipHandler, SaveFormat.Html);
HttpContext.Response.ContentType = "application/zip";
HttpContext.Response.Headers.Add("Content-Disposition", "attachment; filename=\"page.zip\"");
```

### 我如何控制 ZIP 中主 HTML 檔案的名稱？

實作一個小型的 `ResourceInfo` 包裝器：

```csharp
public override Stream HandleResource(ResourceInfo info)
{
    // Force the main HTML to be called "index.html"
    string entryName = info.IsMainDocument ? "index.html" : info.Name;
    var entry = _zip.CreateEntry(entryName);
    return entry.Open();
}
```

### 大型文件會怎樣？記憶體使用量會不會爆炸？

使用 `MemoryResourceHandler` 時，所有資料都存於記憶體，對於一般頁面而言沒問題。若是大型報表，請改用 `FileResourceHandler`（寫入暫存檔）或如前所示直接串流至 ZIP。這樣可降低記憶體佔用。

## 專業提示與最佳實踐

* **負責任地釋放** – `MemoryResourceHandler` 與 `ZipResourceHandler` 都實作 `IDisposable`。請使用 `using` 區塊包住，以確保清理。
* **保持串流開啟** – 建立 `ZipArchive` 時留意 `leaveOpen:true`。它可防止底層的 `FileStream` 被過早關閉，避免破壞外層的 `using` 區塊。
* **設定正確的 MIME 類型** – 若直接提供 HTML，使用 `text/html`。ZIP 則使用 `application/zip`。
* **版本相容性** – 此程式碼相容於 Aspose.HTML 22.10 以上；較新版本可能加入額外的 `SaveFormat` 選項（例如 `SaveFormat.Mhtml`）。

## 結論

現在你已了解如何在 C# 中使用自訂的 `MemoryResourceHandler` **儲存 HTML**，以及看到一個具體的實作，說明 **如何建立 ZIP** 壓縮檔，使用 `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}