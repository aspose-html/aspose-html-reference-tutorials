---
category: general
date: 2026-11-14
description: 使用 Aspose.HTML 在 C# 中將 HTML 轉換為 PNG – 逐步指南，將 HTML 渲染為 PNG、將 HTML 轉換為圖像，並將
  HTML 儲存為 PNG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PNG from HTML
- render HTML to PNG
- convert HTML to image
- save HTML as PNG
- render HTML to image
language: zh-hant
lastmod: 2026-11-14
og_description: 使用 Aspose.HTML 在 C# 中將 HTML 轉換為 PNG。了解如何將 HTML 渲染成 PNG、將 HTML 轉為圖像，以及在簡單的幾個步驟中將
  HTML 儲存為 PNG。
og_image_alt: Diagram illustrating create PNG from HTML workflow using Aspose.HTML
  in C#
og_title: 在 C# 中從 HTML 產生 PNG – 完整 Aspose.HTML 教學
schemas:
- author: Aspose
  dateModified: '2026-11-14'
  description: Create PNG from HTML in C# using Aspose.HTML – a step‑by‑step guide
    to render HTML to PNG, convert HTML to image, and save HTML as PNG.
  headline: How to create PNG from HTML in C# with Aspose.HTML
  type: TechArticle
- description: Create PNG from HTML in C# using Aspose.HTML – a step‑by‑step guide
    to render HTML to PNG, convert HTML to image, and save HTML as PNG.
  name: How to create PNG from HTML in C# with Aspose.HTML
  steps:
  - name: Prerequisites
    text: '* .NET 6.0 SDK or later (the code also works with .NET Core 3.1 and .NET
      Framework 4.7+). * Visual Studio 2022 or any IDE that supports C#. * Basic familiarity
      with C# async/await is helpful but not required.'
  - name: Install Aspose.HTML
    text: 'Open a terminal in your project folder and run:'
  - name: Create a custom resource handler (optional but recommended)
    text: 'When the HTML references external assets (e.g., `logo.png`, CSS files,
      web fonts), Aspose.HTML asks a `ResourceHandler` for a stream. By providing
      our own handler we can:'
  - name: Build the HTML document
    text: You can load HTML from a string, a URL, or a file. For simplicity the tutorial
      uses an inline string that contains an image placeholder.
  - name: Configure image save options
    text: '`ImageSaveOptions` tells Aspose.HTML what raster format to produce and
      which `ResourceHandler` to use.'
  - name: Render the HTML to PNG
    text: The `RenderToImage` method performs the actual conversion. It takes a file
      path and the options defined above.
  - name: Verify the result
    text: Open the generated PNG with any image viewer. You should see the heading
      “Hello, Aspose.HTML!” and a blank placeholder where `logo.png` would appear
      (because our handler returns an empty stream). To **convert HTML to image**
      with the real logo, replace `MyHandler` with a version that loads the actua
  - name: Extending the solution (optional)
    text: Extending the solution (optional)
  type: HowTo
tags:
- Aspose.HTML
- C#
- Image rendering
title: 如何在 C# 中使用 Aspose.HTML 從 HTML 產生 PNG
url: /zh-hant/net/generate-jpg-and-png-images/how-to-create-png-from-html-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.HTML 從 HTML 建立 PNG

如果您需要在 .NET 應用程式中 **從 HTML 建立 PNG**，本指南將向您展示完整步驟。您將學習如何 **將 HTML 渲染為 PNG**、處理外部資源，以及 **在 C# 環境中直接將 HTML 儲存為 PNG**。

此範例使用 Aspose.HTML 5.x，這是一個完全受管理的函式庫，可將 HTML、CSS 與 SVG 渲染為點陣圖像。無需外部瀏覽器或原生相依性，使此解決方案非常適合伺服器端影像產生、電子郵件縮圖建立或 PDF 前置處理。

## 您將完成的工作

* 使用 Aspose.HTML NuGet 套件建立 C# 專案。  
* 實作自訂的 `ResourceHandler` 以控制圖像、CSS 與字型的取得方式。  
* 使用 `ImageSaveOptions` **將 HTML 渲染為 PNG**。  
* 驗證輸出檔案，並了解如何在其他格式中 **將 HTML 轉換為影像**。

### 前置條件

* .NET 6.0 SDK 或更新版本（程式碼亦相容於 .NET Core 3.1 與 .NET Framework 4.7+）。  
* Visual Studio 2022 或任何支援 C# 的 IDE。  
* 具備基本的 C# async/await 知識會有幫助，但非必須。

> **專業提示：** Aspose.HTML 依開發人員或伺服器授權。評估時可使用臨時授權金鑰；函式庫在試用模式下會在渲染的影像上加上浮水印。

## 如何使用 Aspose.HTML 從 HTML 建立 PNG

此解決方案的核心包含三個小類別：自訂的 `ResourceHandler`、建立 `HTMLDocument` 的方法，以及執行 **將 HTML 儲存為 PNG** 的渲染呼叫。以下各節將逐一說明。

### 步驟 1：安裝 Aspose.HTML

在專案資料夾中開啟終端機並執行以下指令：

```bash
dotnet add package Aspose.Html
```

此套件包含 `Aspose.Html`、`Aspose.Html.Rendering` 與 `Aspose.Html.Rendering.Image`，這些是產生影像所必需的。

### 步驟 2：建立自訂資源處理程式（可選但建議）

當 HTML 參照外部資源（例如 `logo.png`、CSS 檔案、網路字型）時，Aspose.HTML 會向 `ResourceHandler` 請求串流。透過提供自訂的處理程式，我們可以：

* 記錄每個請求的 URL。  
* 將資源重新導向至 CDN 或記憶體快取。  
* 防止在受限環境中發出網路請求。

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

/// <summary>
/// Supplies a stream for each external resource referenced by the HTML.
/// </summary>
class MyHandler : ResourceHandler
{
    /// <summary>
    /// Returns a <see cref="Stream"/> that Aspose.HTML will read from.
    /// </summary>
    /// <param name="info">Information about the requested resource.</param>
    /// <returns>A writable <see cref="MemoryStream"/>.</returns>
    public override Stream HandleResource(ResourceInfo info)
    {
        // For demonstration we return an empty MemoryStream.
        // In production you could download the resource, read it from disk,
        // or generate it on the fly.
        return new MemoryStream();
    }
}
```

**為何使用自訂處理程式？**  
若 HTML 包含 `<img src="logo.png">`，預設處理程式會嘗試從相對於目前工作目錄的檔案系統讀取 `logo.png`。在雲端原生服務中，檔案系統可能為唯讀，使用自訂處理程式即可自行控制每個資源的來源。

### 步驟 3：建立 HTML 文件

您可以從字串、URL 或檔案載入 HTML。為了簡化說明，本教學使用內嵌字串，其中包含影像佔位符。

```csharp
// Build a simple HTML document with an image reference.
string markup = @"
<html>
  <head>
    <style>
      body { font-family: Arial, sans-serif; background:#f8f8f8; }
      img { width:150px; height:auto; }
    </style>
  </head>
  <body>
    <h1>Hello, Aspose.HTML!</h1>
    <img src='logo.png' alt='Company logo'>
  </body>
</html>";

HTMLDocument html = new HTMLDocument(markup);
```

如果您已有 HTML 檔案，請將建構子改為 `new HTMLDocument("path/to/file.html")`。

### 步驟 4：設定影像儲存選項

`ImageSaveOptions` 告訴 Aspose.HTML 要產生哪種點陣格式以及使用哪個 `ResourceHandler`。

```csharp
// Choose PNG as the output format.
ImageSaveOptions options = new ImageSaveOptions(SaveFormat.Png)
{
    // Attach the custom handler defined in Step 2.
    ResourceHandler = new MyHandler(),

    // Optional: control the image size and background.
    Width = 1024,               // Width in pixels.
    Height = 768,               // Height in pixels.
    BackgroundColor = System.Drawing.Color.White
};
```

您也可以設定 `Resolution`、`PageNumber` 或 `PageCount`，以在來源為多框架 HTML 文件時渲染特定頁面。

### 步驟 5：將 HTML 渲染為 PNG

`RenderToImage` 方法執行實際的轉換。它接受檔案路徑以及上述定義的選項。

```csharp
// Render the HTML document to a PNG file.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");
html.RenderToImage(outputPath, options);

// Inform the user.
Console.WriteLine($"HTML has been rendered to PNG at: {outputPath}");
```

方法執行完畢後，`output.png` 會包含標記的點陣快照，亦包括 `MyHandler` 所提供的任何影像。

### 步驟 6：驗證結果

使用任何影像檢視器開啟產生的 PNG。您應該會看到標題「Hello, Aspose.HTML!」以及 `logo.png` 原本應出現的位置呈現空白佔位（因為我們的處理程式回傳空串流）。若要 **將 HTML 轉換為影像** 並顯示真實的標誌，請將 `MyHandler` 換成載入實際檔案的版本：

```csharp
public override Stream HandleResource(ResourceInfo info)
{
    if (info.Uri.EndsWith("logo.png", StringComparison.OrdinalIgnoreCase))
    {
        // Load the real logo from disk.
        return File.OpenRead(@"C:\Images\logo.png");
    }
    // Fallback for other resources.
    return base.HandleResource(info);
}
```

重新執行程式，即可在輸出 PNG 中看到標誌。

### 步驟 7：擴充解決方案（可選）

#### 將 HTML 渲染為其他影像格式

若要 **將 HTML 渲染為影像**（如 JPEG、BMP 或 TIFF），只需更改 `SaveFormat`：

```csharp
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.Jpeg);
html.RenderToImage("output.jpg", jpegOptions);
```

#### 產生多頁

如果您的 HTML 包含分頁符號（`<div style="page-break-after:always;">`），您可以分別渲染每一頁：

```csharp
for (int i = 0; i < html.PageCount; i++)
{
    options.PageNumber = i + 1; // 1‑based index
    string pagePath = $"output_page_{i + 1}.png";
    html.RenderToImage(pagePath, options);
}
```

#### 為高吞吐服務使用非同步渲染

Aspose.HTML 亦提供非同步 API：

```csharp
await html.RenderToImageAsync(outputPath, options);
```

當渲染在必須保持回應的 ASP.NET Core 端點內執行時，此功能相當有用。

## 完整、可執行的範例

以下是一個自包含的主控台應用程式，將所有部件整合在一起。將程式碼複製到新的 .NET 主控台專案中並執行。

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;

namespace HtmlToPngDemo
{
    /// <summary>
    /// Supplies a stream for each external resource referenced by the HTML.
    /// </summary>
    class MyHandler : ResourceHandler
    {
        public override Stream HandleResource(ResourceInfo info)
        {
            // Load the real logo if the request is for "logo.png".
            if (info.Uri.EndsWith("logo.png", StringComparison.OrdinalIgnoreCase))
            {
                // Adjust the path to where your logo actually lives.
                string logoPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "logo.png");
                return File.OpenRead(logoPath);
            }

            // For any other resource return an empty stream.
            return new MemoryStream();
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Build the HTML markup.
            string markup = @"
            <html>
              <head>
                <style>
                  body { font-family: Arial, sans-serif; background:#f8f8f8; }
                  img { width:150px; height:auto; }
                </style>
              </head>
              <body>
                <h1>Hello, Aspose.HTML!</h1>
                <img src='logo.png' alt='Company logo'>
              </body>
            </html>";

            // 2️⃣ Create the HTML document object.
            HTMLDocument html = new HTMLDocument(markup);

            // 3️⃣ Configure PNG output options.
            ImageSaveOptions options = new ImageSaveOptions(SaveFormat.Png)
            {
                Width = 1024,
                Height = 768,
                BackgroundColor = System.Drawing.Color.White,
                ResourceHandler = new MyHandler()
            };

            // 4️⃣ Render the document to a PNG file.
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");
            html.RenderToImage(outputPath, options);

            Console.WriteLine($"✅ HTML successfully rendered to PNG at: {outputPath}");
        }
    }
}
```

**預期輸出：**  
在程式的工作目錄中會出現名為 `output.png`（≈ 1024 × 768 px）的檔案。影像包含標題以及

## 接下來您應該學習什麼？

以下教學涵蓋與本指南技術密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.HTML 從 HTML 建立 PNG – 完整步驟指南](/html/english/net/generate-jpg-and-png-images/create-png-from-html-with-aspose-html-full-step-by-step-guid/)
- [建立 HTML 文件並將 HTML 渲染為 PNG – 完整 C# 指南](/html/english/net/rendering-html-documents/create-html-document-and-render-html-to-png-full-c-guide/)
- [如何使用 Aspose 將 HTML 渲染為 PNG – 步驟指南](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}