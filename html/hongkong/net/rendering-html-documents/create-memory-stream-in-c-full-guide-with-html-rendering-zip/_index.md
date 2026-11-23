---
category: general
date: 2026-03-31
description: 在 C# 中建立記憶體串流，學習將 HTML 轉換為 PNG、使用自訂資源處理程式、將 HTML 儲存為 ZIP，並以程式方式設定字型樣式——一次教學完整呈現。
draft: false
keywords:
- create memory stream
- render html to png
- custom resource handler
- save html to zip
- set font style programmatically
language: zh-hant
og_description: 在 C# 中建立記憶體串流，立即將 HTML 轉換為 PNG，使用自訂資源處理程式，將 HTML 儲存為 ZIP，並以程式方式設定字型樣式。
og_title: 在 C# 中建立記憶體串流 – 完整程式設計指南
tags:
- C#
- HTML rendering
- Streams
- ZIP archives
- Image processing
title: 在 C# 中建立記憶體串流 – 完整指南，含 HTML 呈現與 ZIP 匯出
url: /zh-hant/net/rendering-html-documents/create-memory-stream-in-c-full-guide-with-html-rendering-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立 Memory Stream – 完整指南：HTML 渲染與 ZIP 匯出

有冇諗過點樣喺 C# 入面 **create memory stream**，然後將 HTML 文件轉成 PNG 圖片、ZIP 檔，甚至即時改變字型樣式？你唔係唯一有呢個疑問嘅人。好多開發者喺需要文件嘅記憶體表示，但又唔想觸及檔案系統時，會卡住。  

喺呢篇教學入面，我哋會一步一步示範完整嘅端對端解決方案：建立自訂資源處理程式、將 HTML 輸入 `MemoryStream`、將相同文件壓縮成 ZIP，最後以抗鋸齒方式渲染成圖片。完成後，你就可以 **render HTML to PNG**、**save HTML to ZIP**，以及 **set font style programmatically**，全程都唔需要寫入暫存檔到磁碟。

## 前置條件

- .NET 6.0 或更新版本（API 介面在近期版本中保持穩定）。  
- 參考一個提供 `HTMLDocument`、`ImageRenderer` 以及相關型別的 HTML‑to‑image 函式庫，例如 **HtmlRenderer.Core**（請換成你實際使用的套件）。  
- 具備對串流、`using` 陳述式以及 C# 物件導向模式的基本了解。

> **Pro tip:** 如果你使用 Visual Studio，請啟用 **nullable reference types** (`<Nullable>enable</Nullable>`) 以便及早捕捉細微錯誤。

## 步驟 1：使用自訂資源處理程式建立 Memory Stream

我哋首先需要一個處理程式，告訴 HTML 引擎 *將* 每個資源（圖片、CSS 等）寫入到哪裡。繼承自 `ResourceHandler` 後，我哋可以將所有輸出導向同一個 `MemoryStream`。

```csharp
using System;
using System.IO;

// Step 1: Define a handler that writes resources to an in‑memory stream
class MemoryResourceHandler : ResourceHandler
{
    // The stream lives for the whole lifetime of the handler
    public MemoryStream OutputStream = new MemoryStream();

    // The engine calls this for every resource it needs to write
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}
```

**為什麼這很重要：**  
`MemoryStream` 完全存在於記憶體中，意味著不會產生磁碟 I/O，對於 Web 服務或單元測試等高效能情境非常適合。此處理程式亦符合 API 要求，因為引擎期望每個資源都有一個 `Stream`。

## 步驟 2：載入 HTML Document 並儲存至 Memory Stream

而家我哋載入既有的 HTML 檔案（或字串），並指示使用我們的 `MemoryResourceHandler`。在呼叫 `Save` 後，`OutputStream` 會包含完整的 HTML 資料。

```csharp
using System.IO;

// Assume the HTML file lives under YOUR_DIRECTORY
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

// Instantiate the memory handler
MemoryResourceHandler memoryHandler = new MemoryResourceHandler();

// Save the document – all resources flow into the same MemoryStream
htmlDoc.Save(memoryHandler);
```

此時串流的位置已在結尾，所以在讀取內容之前需要將其倒回。

```csharp
// Reset the stream position to the beginning
memoryHandler.OutputStream.Position = 0;

// Quick verification (optional)
// string htmlContent = new StreamReader(memoryHandler.OutputStream).ReadToEnd();
// Console.WriteLine(htmlContent);
```

> **Note:** 上面嘅 `ReadToEnd` 行已被註解，因為在正式環境下，你可能會將串流傳遞給其他元件，而唔係直接印出。

## 步驟 3：使用自訂 ZIP 資源處理程式壓縮相同的 HTML

有時你需要將 HTML 連同其資產一起打包。第二個自訂處理程式可以即時為每個資源建立 ZIP 條目。

```csharp
using System.IO.Compression;

// Step 4: Define a handler that writes each resource into a ZIP archive
class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(string zipPath)
    {
        // Open (or create) the archive in write mode
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);
    }

    // The engine calls this for each resource; we create a ZIP entry with the same name
    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    // Proper disposal of the underlying ZipArchive
    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}
```

而家我們重新使用相同的 `htmlDoc` 實例，將其寫入 ZIP 檔案。

```csharp
// Step 5: Save the HTML document into a ZIP file
using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
{
    htmlDoc.Save(zipHandler);
}
```

**Edge case tip:** 如果 HTML 多次引用相同的圖片，ZIP 處理程式會產生重複的條目。為避免此情況，你可以保留一個已加入名稱的 `HashSet<string>`，並返回已存在條目的串流。

## 步驟 4：以程式方式設定預設樣式表的字型樣式

在不修改原始 HTML 的情況下改變文件外觀常常很方便——例如在產生帶有粗體標題的 PDF 預覽時。此函式庫提供可調整的 `DefaultViewStyleSheet`。

```csharp
// Step 6: Apply bold and italic styling to the default view stylesheet
htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

你可以結合 `WebFontStyle` 中定義的任何旗標。變更會立即生效，並影響後續的渲染或儲存。

## 步驟 5：將 HTML Document 渲染為 PNG 圖片

最後，將 HTML 轉換為點陣圖。啟用抗鋸齒與 hinting 後，我哋可以得到清晰的文字與平滑的邊緣。

```csharp
using System.Drawing; // For ImageRenderingOptions if needed

// Step 7: Render the document to an image with antialiasing and hinting
var renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    UseHinting = true
};

new ImageRenderer(renderingOptions).Render(htmlDoc, "YOUR_DIRECTORY/out.png");
```

**你會看到的結果：** 在 `YOUR_DIRECTORY` 下產生名為 `out.png` 的 PNG 檔案，外觀與瀏覽器渲染的 HTML 完全相同，但套用了先前設定的粗斜體樣式。

![create memory stream output 的螢幕截圖](placeholder-image.png "create memory stream 範例")

*圖片的 alt 文字包含主要關鍵字，以符合 SEO 要求。*

## 常見問題與注意事項

| Question | Answer |
|----------|--------|
| **我可以在儲存至 ZIP 後再次使用相同的 `HTMLDocument` 嗎？** | 可以。文件物件仍保留在記憶體中，你可以使用不同的處理程式多次呼叫 `Save`。 |
| **如果 HTML 包含大型二進位資產會怎樣？** | `MemoryStream` 會相應增長。對於非常大的檔案，建議直接串流至檔案或使用 `BufferedStream`。 |
| **我需要對 `MemoryResourceHandler` 呼叫 `Dispose` 嗎？** | 不一定必須，因為它只持有一個 `MemoryStream`，該串流會在處理程式被垃圾回收時釋放。但養成呼叫 `Dispose` 的習慣仍然不錯。 |
| **我要如何變更圖片格式（例如改成 JPEG 而非 PNG）？** | 將不同的副檔名傳遞給 `ImageRenderer.Render`，或使用 `ImageRenderer.RenderToBitmap`，再以 `bitmap.Save("out.jpg", ImageFormat.Jpeg)` 儲存。 |
| **ZIP 處理程式是執行緒安全的嗎？** | 不是。`ZipArchive` 並非執行緒安全，因此需序列化存取或為每個執行緒建立獨立的處理程式。 |

## 完整範例程式

以下是一個可直接複製貼上的完整程式，示範所有步驟。請將 `YOUR_DIRECTORY` 替換為你機器上的實際路徑。

```csharp
// FullExample.cs
using System;
using System.IO;
using System.IO.Compression;

// Assume these types come from your HTML rendering library
using HtmlRendering; // placeholder namespace

class MemoryResourceHandler : ResourceHandler
{
    public MemoryStream OutputStream = new MemoryStream();
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}

class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(string zipPath) =>
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);

    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // 2️⃣ Write to a memory stream
        var memHandler = new MemoryResourceHandler();
        htmlDoc.Save(memHandler);
        memHandler.OutputStream.Position = 0;
        // Optional: verify content
        // Console.WriteLine(new StreamReader(memHandler.OutputStream).ReadToEnd());

        // 3️⃣ Zip the same document
        using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
        {
            htmlDoc.Save(zipHandler);
        }

        // 4️⃣ Change font style programmatically
        htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 5️⃣ Render to PNG with antialiasing & hinting
        var renderOpts = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            UseHinting = true
        };
        new ImageRenderer(renderOpts).Render(htmlDoc, "YOUR_DIRECTORY/out.png");

        Console.WriteLine("All operations completed successfully.");
    }
}
```

執行此程式後，你會得到三個產出：

1. **In‑memory HTML** 儲存在 `memHandler.OutputStream` 中。  
2. **`output.zip`** 包含 HTML 及所有相關資源。  
3. **`out.png`** – 一張遵循粗斜體樣式的渲染圖像。

## 結論

我們示範了如何在 C# 中 **create memory stream**，並無縫結合 HTML 渲染、ZIP 壓縮與圖片產生。關鍵在於，同一個 `HTMLDocument` 可以以多種方式儲存——寫入 `MemoryStream`、ZIP 壓縮檔或 PNG 圖片——只要替換 `ResourceHandler` 即可。  

如果你想更進一步，可以嘗試：

- **Render to PDF**：使用接受 `Stream` 的 PDF 渲染器。  
- **Compress the memory stream**：在傳輸至網路前壓縮記憶體串流（例如 `GZipStream`）。  
- **Combine multiple HTML pages**：將多個 HTML 頁面合併成一個 ZIP 以進行批量匯出。  

歡迎自行實驗，如有任何問題，請隨時留言。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}