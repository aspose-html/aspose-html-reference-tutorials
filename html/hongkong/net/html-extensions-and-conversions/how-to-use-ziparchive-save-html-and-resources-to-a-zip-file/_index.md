---
category: general
date: 2026-03-29
description: 學習如何在 C# 中使用 ZipArchive 將 HTML 轉換為 ZIP、將 HTML 儲存至 ZIP，並壓縮 HTML 圖片——一次完整清晰的教學。
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: zh-hant
og_description: 探索如何在 C# 中使用 ZipArchive 將 HTML 轉換為 ZIP、將 HTML 儲存為 ZIP，並壓縮 HTML 圖片，提供完整可執行的範例。
og_title: 如何使用 ZipArchive – 將 HTML 與資源儲存為 ZIP 檔案
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: 如何使用 ZipArchive – 將 HTML 與資源儲存至 ZIP 檔案
url: /zh-hant/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 ZipArchive – 將 HTML 與資源儲存為 ZIP 檔案

有沒有想過 **如何使用 ZipArchive** 把 HTML 頁面與其圖片、CSS 以及其他資源打包在一起？你並不孤單。許多開發者在需要發佈一個自包含的 HTML 套件時會卡關，尤其是當頁面引用外部資源時。好消息是，只要寫幾行 C# 程式碼結合 Aspose.HTML，就能 **將 HTML 轉成 ZIP**、**將 HTML 儲存至 ZIP**，甚至 **壓縮 HTML 圖片**，全程不離開 IDE。

在本教學中，我們將一步步示範完整流程——從建立簡單的 `HTMLDocument` 到透過自訂的 `ResourceHandler` 處理每一個連結資源。完成後，你將得到一個可直接放到任何 Web 伺服器或作為電郵附件的 ZIP 檔案。無需外部腳本、無需手動複製——純 .NET 解決方案。

## 前置條件

在開始之前，請確保你已具備：

- **.NET 6+**（或 .NET Framework 4.6+）。使用的 API 屬於 `System.IO.Compression`。
- 已安裝 **Aspose.HTML for .NET**（NuGet 套件 `Aspose.Html`）。
- 具備基本的 C# 語法概念。
- 使用 Visual Studio 或 VS Code 等 IDE。

就這些。無需額外工具、無需第三方壓縮程式。準備好了嗎？讓我們開始吧。

## 第一步：建立專案並加入相依性

建立一個新的 Console 專案：

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

`Aspose.Html` 套件提供 `HTMLDocument` 類別與我們稍後會擴充的 `ResourceHandler` 基底類別。內建的 `System.IO.Compression` 命名空間則提供 `ZipArchive` 與 `ZipArchiveEntry`。

> **小技巧：** 若目標是 .NET 6，可使用頂層語句（top‑level statements）讓 `Main` 方法更簡潔。以下程式碼採用傳統的 `Program` 類別以利說明。

## 第二步：建立自訂資源處理器

當 Aspose.HTML 儲存文件時，會呼叫 `ResourceHandler` 取得每個外部檔案（圖片、CSS、字型等）的 `Stream`。只要覆寫 `HandleResource`，就能把每個資源直接寫入 ZIP 條目。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**為什麼這很重要：** 不必先將資源寫到磁碟再壓縮，處理器會直接將資源串流至 ZIP，降低 I/O 負擔，且能確保 ZIP 與 HTML 內容同步。

## 第三步：建立 HTML 文件

為了示範，我們會嵌入一段小型 HTML 片段，裡面會引用名為 `logo.png` 的外部圖片。實務上，你可能會從檔案或資料庫載入 HTML。

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

如果需要 **壓縮 HTML 圖片**，只要確保圖片檔案與可執行檔同目錄（或以資源方式嵌入），`ZipResourceHandler` 會自動把圖片加入壓縮檔。

## 第四步：開啟（或建立）ZIP 檔並儲存

現在把所有步驟串起來。我們開啟一個 `FileStream` 作為輸出 ZIP，使用 *Update* 模式建立 `ZipArchive`，再把自訂處理器傳給 `HTMLDocument.Save`。

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

`using` 區塊結束時，ZIP 會自動完成並關閉。產生的 `output.zip` 內含：

- `index.html`（序列化後的 HTML 文件）
- `logo.png`（HTML 中引用的圖片）

你可以用任何檔案總管打開 ZIP 來驗證內容。

## 第五步：驗證結果（可選）

最好再次確認 ZIP 是否真的可用。以下程式碼可在前述程式執行完後列出所有條目：

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

執行後應該會看到類似以下的輸出：

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

將 `index.html` 從解壓縮的資料夾開啟，你會看到圖片正確顯示——證明 **將 HTML 儲存至 ZIP** 已成功。

## 常見變化與邊緣案例

### 1. 為 HTML 檔案使用自訂條目名稱

預設情況下 Aspose 會把 HTML 寫入 `index.html`。若需自訂名稱，可在儲存前設定 `htmlDocument.FileName`：

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. 手動加入額外檔案

有時你想把其他檔案（例如 README）一起打包。只要在呼叫 `htmlDocument.Save` 前，直接把檔案加入 `ZipArchive` 即可：

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. 高效處理大型圖片

若 HTML 參照的圖片非常大，建議先縮小尺寸以控制 ZIP 大小。`System.Drawing.Common` 套件可以協助：

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

然後在 HTML 中改為 `<img src='logo_resized.png'>`。

## 完整可執行範例

以下是完整程式碼，可直接貼到 `Program.cs`。只要已安裝 Aspose.HTML NuGet 套件，即可編譯執行。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**預期輸出：** 主控台會印出成功訊息，`output.zip` 會出現在專案資料夾，內含 `index.html` 與 `logo.png`。

## 常見問與答

- **這在 .NET Core 上能跑嗎？**  
  能。`System.IO.Compression.ZipArchive` 屬於 .NET Standard，相同程式碼可在 .NET 5、.NET 6、.NET 7 上執行。

- **如果想更積極地 **壓縮 HTML 圖片** 該怎麼做？**  
  可在加入 ZIP 前先對圖片做前置處理（縮放、轉成 WebP 等）。處理器本身只會串流它收到的資料。

- **可以加密 ZIP 嗎？**  
  `ZipArchive` 只支援基本的壓縮，若需 AES 加密需使用第三方庫（例如 `SharpZipLib`）。你可以先用該庫建立加密 ZIP，再把串流交給 Aspose 作為自訂 `ResourceHandler`。

- **要怎麼設定 ZIP 內的根目錄？**  
  在 `HandleResource` 中為 `resourceName` 加上資料夾前綴，例如 `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`。

## 結論

現在你已掌握 **如何在 C# 中使用 ZipArchive** 來 **將 HTML 轉成 ZIP**、**將 HTML 儲存至 ZIP**，以及 **壓縮 HTML 圖片**，全程只需一段乾淨的程式碼。透過擴充 `ResourceHandler`，我們避免了任何暫存檔，保持記憶體效能。此模式易於擴展：只要把產生的 ZIP 放到 Web 伺服器、寄給客戶或上傳至雲端儲存即可。

接下來可以探索的方向：

- **以程式方式建立整個網站資料夾的 ZIP 壓縮**（`create zip archive c#`）。
- **在壓縮前先將 PDF 或 DOCX 轉換**，打造更完整的文件套件。
- **與 ASP.NET Core 整合**，直接把 ZIP 串流回客戶端瀏覽器（`FileStreamResult`）。

對於 HTML 壓縮、字型處理或圖片最佳化還有其他問題嗎？歡迎在評論區留言或於 Stack Overflow 上找我。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}