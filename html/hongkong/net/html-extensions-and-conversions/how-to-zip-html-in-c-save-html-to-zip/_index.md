---
category: general
date: 2025-12-29
description: 如何在 C# 中快速使用 Aspose.HTML 壓縮 HTML – 透過自訂 ZipResourceHandler 將 HTML 儲存為
  zip。一步一步學習。
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: zh-hant
og_description: 如何使用 Aspose.HTML 在 C# 中快速將 HTML 壓縮為 zip。請參考本指南，將 HTML 保存為 zip 並使用自訂資源處理建立
  zip 壓縮檔。
og_title: 如何在 C# 中壓縮 HTML – 將 HTML 儲存為 Zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: 如何在 C# 中壓縮 HTML – 將 HTML 儲存為 Zip
url: /zh-hant/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中壓縮 HTML 為 Zip – 將 HTML 儲存至 Zip

在 C# 中壓縮 HTML 為 Zip 是當你想將網頁打包供離線使用時的常見需求。無論是將單一頁面連同其圖片一起打包，或是匯出整個網站，**將 HTML 儲存至 Zip** 都能讓所有檔案保持整齊且可攜帶。本教學將一步步示範完整、可直接執行的解決方案，除了壓縮 HTML 標記外，還會將每個參考的資源直接串流寫入壓縮檔。

你將學會：

* 使用 .NET 的 `System.IO.Compression` 程式化建立 Zip 壓縮檔。
* 在 Aspose.HTML 中插入自訂的 `ResourceHandler`，讓資源直接寫入 Zip。
* 處理如已存在的 Zip 檔案與大型二進位資產等邊緣情況。

不需要任何外部工具——只要 C#、Aspose.HTML 以及少量程式碼即可。

## 需求條件

在開始之前，請確保你已具備：

* **.NET 6+**（此程式碼同樣支援 .NET Framework 4.6.2 及以上版本）。
* **Aspose.HTML for .NET** – 可從 Aspose 官方網站取得免費試用版，或使用已授權的版本。
* 開發環境（Visual Studio、VS Code、Rider… 任一你慣用的工具）。

就這些。除 `System.IO.Compression`（隨 .NET 捆綁）與 `Aspose.HTML` 之外，無需額外的 NuGet 套件。

## 第一步：建立專案與引用

建立一個新的 Console 專案（或將程式碼放入既有專案）。在檔案頂部加入必要的 `using` 指令：

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **小技巧：** 若你使用 Visual Studio，IDE 會提示你安裝缺少的 `Aspose.Html` NuGet 套件。接受安裝後即可開始開發。

## 第二步：實作自訂的 ZipResourceHandler

Aspose.HTML 在需要寫入資源（如圖片、CSS 或腳本）時會呼叫 `ResourceHandler`。透過覆寫 `HandleResource`，我們可以自行決定每個資源的寫入位置。以下的處理器會建立一個對應資源邏輯路徑的 Zip 條目，並回傳指向該條目的可寫入串流。

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**為什麼這很重要：**  
此方式避免先寫入暫存資料夾再壓縮的步驟，直接在寫入時即串流至 Zip，減少磁碟 I/O 且降低記憶體使用量。同時確保 Zip 內的資料夾結構與 HTML 的相對路徑一致，瀏覽器在解壓後開啟頁面時即可正確載入資源。

## 第三步：準備 Zip 壓縮檔

接下來開啟（或建立）目標 Zip 檔案。`FileMode.Create` 旗標會覆寫任何已存在的檔案——非常適合可重複執行的建置流程。若你想保留既有的壓縮檔，可改用 `FileMode.OpenOrCreate`，並自行處理重複條目。

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **邊緣情況：** 若程式在 `using` 區塊結束前發生例外，可能會留下損毀的 Zip。將程式碼包在 try/catch 中，失敗時刪除未完成的檔案，是簡單且有效的防護措施。

## 第四步：建立內嵌資源的 HTML 文件

為示範，我們會建立一個簡易的 HTML 頁面，內含一張名為 `image.png` 的圖片。實務上，你可能會從檔案或資料庫的字串載入 HTML。

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

如果磁碟上已有實際的圖片檔案，你可以在儲存 HTML 前手動將它加入 Zip，或讓 Aspose.HTML 透過自訂處理器自動抓取（例如從 URL）。我們的處理器同時支援本機路徑與遠端 URL。

## 第五步：設定儲存選項以使用 ZipResourceHandler

現在告訴 Aspose.HTML 在寫入資源時使用我們自訂的處理器。`HTMLSaveOptions` 類別同時允許你指定 Zip 內的輸出檔名，預設為 `index.html`。

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## 第六步：儲存文件 – 所有資料皆串流至 Zip

最後呼叫 `Save`。Aspose.HTML 會解析標記、定位 `<img>` 標籤、呼叫 `HandleResource` 取得 `image.png`，並將 HTML 與圖片同時寫入同一個 Zip 壓縮檔。

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

當 `using` 區塊結束時，`ZipArchive` 會完成檔案的最終寫入，讓它可以直接供外部使用。

### 完整範例

以下是完整的程式碼，直接貼到 `Program.cs` 後執行即可，無需額外修改。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**預期結果：** 執行完畢後，`output.zip` 內會有兩個條目：

```
index.html
image.png
```

若將檔案解壓並在瀏覽器開啟 `index.html`，圖片會正確顯示，因為相對路徑已被保留。

## 常見問題

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}