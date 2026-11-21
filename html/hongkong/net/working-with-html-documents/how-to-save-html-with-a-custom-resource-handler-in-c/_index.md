---
category: general
date: 2026-11-20
description: 學習如何在 C# 中使用自訂 ResourceHandler 儲存 HTML，並以簡潔、可投入生產的程式碼將 HTML 存入 zip 壓縮檔。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: zh-hant
lastmod: 2026-11-20
og_description: 如何在 C# 中使用自訂 ResourceHandler 儲存 HTML，並可選擇將 HTML 壓縮成 zip 檔案——完整可執行的
  .NET 開發者指南。
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: 如何在 C# 中使用自訂資源處理程式儲存 HTML
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: 如何在 C# 中使用自訂資源處理程式儲存 HTML
url: /zh-hant/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用自訂資源處理程式儲存 HTML

如果你想了解 **如何儲存 HTML**（無論是來自記憶體字串或已解析的文件），本指南提供完整解決方案。透過自訂的 `ResourceHandler` 你可以自行控制目的地串流，亦即能在不產生暫存檔的情況下 **將 HTML 儲存至 zip** 壓縮檔。

本教學會說明為何 `ResourceHandler` 比較適合取代舊版的 `IOutputStorage` 做法、如何設定，以及如何擴充以支援 zip 壓縮。完成後，你即可在任何 .NET 6+ 專案中嵌入此程式碼，並依需求調整儲存方式。

## 你將會建立的內容

* 一個最小的 `ResourceHandler`，回傳 `MemoryStream`。
* 使用 **HtmlAgilityPack** 建立的 `HtmlDocument`。
* 呼叫 `doc.Save`，將 HTML 寫入處理程式提供的串流。
* 可選的包裝器，將產生的 HTML 壓縮成 zip 檔。

前置條件：

* .NET 6 SDK 或更新版本。
* `HtmlAgilityPack` NuGet 套件（`dotnet add package HtmlAgilityPack`）。
* 基本的 C# 串流概念。

## 步驟 1：建立自訂資源處理程式（主要方式來 **how to save html**）

`ResourceHandler` 基底類別（自 viewer SDK 版本 24.2 起提供）定義唯一抽象方法 `HandleResource`。實作此方法即可完整掌控 HTML 寫入的目的地。

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**為什麼這很重要：** 透過回傳 `MemoryStream`，你可以避免磁碟 I/O、降低延遲，且讓單元測試保持可預測。此處理程式會在 `Save` 方法被呼叫時自動執行，無需手動傳遞串流。

## 步驟 2：載入或建立 HTML 文件

`HtmlAgilityPack` 提供便利的 `HtmlDocument` 類別，可解析字串、檔案或串流。此範例直接載入一段簡單的文字，實際上相同程式碼亦能處理任何 HTML 來源。

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**為什麼這很重要：** 將文件保留在記憶體中與自訂處理程式的串流導向相符，也讓你在儲存前能自由操作 DOM，例如注入腳本或修正不完整的標籤。

## 步驟 3：使用自訂處理程式儲存文件

以 `MyHandler` 的實例呼叫 `doc.Save`，即會觸發 `HandleResource` 方法。HTML 會直接寫入你回傳的串流。

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

`Save` 完成後，`MyHandler` 內的 `MemoryStream` 已包含序列化後的 HTML。你可以這樣取得內容：

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**結果：** 主控台會印出與 `LoadHtml` 時傳入的字串完全相同的 HTML，證明你已掌握 **如何使用自訂處理程式儲存 HTML**。

## 步驟 4：將處理程式擴充為 **save HTML to zip**

若想將 HTML 打包成壓縮檔，只需修改 `MyHandler`，讓它寫入 `ZipArchiveEntry`。.NET 的 `System.IO.Compression` 命名空間讓此工作相當簡單。

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

接著使用新的處理程式：

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**為什麼會這樣運作：** `HandleResource` 會建立名為 `document.html` 的 zip 條目。當 `doc.Save` 寫入回傳的串流時，資料會自動被壓縮。因為 zip 是在記憶體中建立，你可以直接從 Web API 回傳、附加於電子郵件，或存入資料庫，而不必觸碰檔案系統。

## 常見問題與邊緣案例

### 若需要在同一個 zip 中放入多個 HTML 檔案該怎麼做？
為每次呼叫 `HandleResource` 建立新的條目。`resourceName` 參數通常已包含檔名，可直接使用：

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### 如何處理大型文件而不耗盡記憶體？
將 `MemoryStream` 改為指向暫存檔的 `FileStream`。處理程式回傳檔案串流，完成 zip 後再自行刪除暫存檔。

### 此方式在 Linux 上的 .NET Core 可行嗎？
可行。所有使用的 API（`MemoryStream`、`ZipArchive`、`HtmlAgilityPack`）皆跨平台。請確保目標框架至少為 .NET 6，以取得最佳相容性。

### 能否對 zip 壓縮檔加密？
`ZipArchive` 本身僅支援第三方套件（例如 `SharpZipLib`）提供的密碼加密。如果需要加密，可在將輸出位元組傳給客戶端前，先使用支援 AES 加密的函式庫進行包裝。

## 專業小技巧

* **重複使用處理程式** 以批次處理多個文件；為每個檔案重新建立 `ZipArchive` 會產生不必要的開銷。
* 若需在壓縮檔仍開啟時讀取其位元組，請在 `ZipArchive` 建構子上設定 `LeaveOpen: true`。
* **在儲存前驗證 HTML**，可設定 `doc.OptionCheckSyntax = true;` 以提前捕捉不良標籤。
* **記錄產生的 zip 大小**；異常大的輸出往往代表資源重複或壓縮未生效。

## 完整範例程式

以下是一個可直接貼到 console 專案（`dotnet new console`）並執行的單一檔案。它示範了純 HTML 儲存與 zip 壓縮兩種情況。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using HtmlAgilityPack;

// ---------- Custom handlers ----------
class MyHandler : ResourceHandler
{
    public MemoryStream HtmlStream { get; } = new();

    public override Stream HandleResource(string resourceName) => HtmlStream;
}

class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open();
    }

    public byte[] GetZipBytes()
    {
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}

// ---------- Main program ----------
class Program
{
    static void Main()
    {
        // Build a simple HTML document.
        HtmlDocument doc = new HtmlDocument();
        doc.LoadHtml("<html><body>Hello World from HtmlAgilityPack</body></html>");

        // ---- Example 1: plain HTML save ----
        var plainHandler = new MyHandler();
        doc.Save(plainHandler);
        plainHandler.HtmlStream.Seek(0, SeekOrigin.Begin);
        using var reader = new StreamReader(plainHandler.HtmlStream);
        Console.WriteLine("Plain HTML output:");


## 接下來該學什麼？

以下教學與本指南緊密相關，能讓你在已掌握的技巧上再進一步。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你熟悉其他 API 功能，或在專案中探索替代實作方式。

- [How to Save HTML in C# with Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [How to Use ZipArchive – Save HTML and Resources to a ZIP File](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [save html as zip with a custom resource handler – step‑by‑step guide](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}