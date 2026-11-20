---
category: general
date: 2026-09-07
description: 學習如何使用 Aspose.HTML 在 C# 中從 HTML 建立圖片。此一步一步的指南亦示範如何將 HTML 渲染成圖片以及將 HTML
  轉換為 PNG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create image from html
- render html to image
- convert html to png
- save html as png
- set image width height
language: zh-hant
lastmod: 2026-09-07
og_description: 使用 Aspose.HTML 在 C# 中將 HTML 轉換為圖像。依照本指南渲染 HTML 為圖像、轉換 HTML 為 PNG，並設定圖像寬度與高度，獲得完美效果。
og_image_alt: Screenshot of a rendered PNG image generated from an HTML file using
  Aspose.HTML
og_title: 在 C# 中從 HTML 建立圖像 – 完整 Aspose.HTML 指南
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: Learn how to create image from HTML with Aspose.HTML in C#. This step‑by‑step
    guide also shows how to render HTML to image and convert HTML to PNG.
  headline: How to create image from HTML using Aspose.HTML in C#
  type: TechArticle
tags:
- Aspose.HTML
- C#
- image rendering
title: 如何在 C# 中使用 Aspose.HTML 從 HTML 產生圖片
url: /zh-hant/net/generate-jpg-and-png-images/how-to-create-image-from-html-using-aspose-html-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.HTML 在 C# 中從 HTML 建立圖像

如果您需要在 .NET 應用程式中 **從 HTML 建立圖像**，本指南將示範使用 Aspose.HTML 的完整步驟。您將學習如何 **將 HTML 渲染為圖像**、選擇 PNG 作為輸出格式，並控制輸出尺寸，使圖像呈現如您所預期的樣子。

本教學涵蓋您所需的一切：必要的 NuGet 套件、完整的程式碼範例、各選項說明，以及常見陷阱的提示。完成後，您將能夠以程式方式 **將 HTML 轉換為 PNG**、**將 HTML 儲存為 PNG**，以及 **設定圖像寬度與高度**。

## 前置條件

* .NET 6.0 或更新版本已安裝（此程式碼亦相容於 .NET 5 與 .NET Framework 4.7+）。
* Visual Studio 2022（或任何支援 C# 的 IDE）。
* Aspose.HTML for .NET 授權或免費評估金鑰。透過 NuGet 安裝套件：

```bash
dotnet add package Aspose.HTML
```

* 一個您想要轉換為圖像的 HTML 檔案（`input.html`）。請將其放置於可從專案參考的資料夾中。

## 步驟 1：載入您想要渲染的 HTML 文件

第一步是建立指向來源檔案的 `HTMLDocument` 實例。Aspose.HTML 會自動讀取標記、CSS 以及外部資源（圖像、字型）。

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;

// Load the HTML file from disk
var document = new HTMLDocument(@"C:\MyProject\Resources\input.html");
```

*為什麼這很重要：* 載入文件將解析與渲染分離，讓您可以重複使用相同的 `HTMLDocument` 物件進行多次渲染（例如不同的圖像尺寸）。

## 步驟 2：設定圖像渲染選項（設定圖像寬度與高度、格式、品質）

`ImageRenderingOptions` 讓您微調輸出。此處我們啟用抗鋸齒、設定粗體 Arial 字型、開啟文字 hinting，並明確 **設定圖像寬度與高度** 為 800 × 600 px。`ImageFormat` 設為 PNG，屬於無損且廣受支援的格式。

```csharp
var renderingOptions = new ImageRenderingOptions
{
    // Smooth graphics with anti‑aliasing
    UseAntialiasing = true,

    // Font used when the HTML references a generic family (e.g., sans‑serif)
    Font = new Font("Arial", 12, WebFontStyle.Bold),

    // Improves the clarity of rendered text
    TextOptions = new TextOptions { UseHinting = true },

    // Explicitly set the output dimensions – this is the “set image width height” part
    Width = 800,
    Height = 600,

    // Choose PNG as the output format – “convert HTML to PNG”
    ImageFormat = ImageFormat.Png
};
```

**提示：** 若省略 `Width` 與 `Height`，Aspose.HTML 會使用 HTML 本身的尺寸，可能產生過大或過小的圖像。當需要可預測的結果時，務必明確定義尺寸。

## 步驟 3：使用已設定的選項建立渲染器

`ImageRenderer` 類別執行實際的轉換。傳入剛剛建立的 `renderingOptions` 可確保渲染器遵循您的設定。

```csharp
var renderer = new ImageRenderer(renderingOptions);
```

*為什麼這很重要：* 將渲染器與選項分離，可讓您在不同文件間重複使用同一渲染器，同時維持單一設定。

## 步驟 4：將 HTML 文件渲染為 PNG 檔案 – 「將 HTML 儲存為 PNG」

現在呼叫 `Render`，提供來源文件與目標檔案路徑。此方法會阻塞，直至圖像寫入磁碟。

```csharp
// Render the HTML to a PNG file – “save HTML as PNG”
renderer.Render(document, @"C:\MyProject\Resources\output.png");
```

呼叫完成後，`output.png` 會包含 `input.html` 的光柵化快照。您可以使用任何圖像檢視器開啟該檔案以驗證結果。

### 預期輸出

執行完整程式會產生具備以下屬性的 PNG 檔案：

* **尺寸：** 800 × 600 px（依 `Width`/`Height` 設定）。
* **格式：** PNG（無損，支援透明度）。
* **視覺品質：** 抗鋸齒圖形與 hinting 文字，與現代瀏覽器中原始 HTML 的外觀相符。

## 完整、可執行的範例

以下為完整程式碼，您可將其複製到主控台應用程式（`Program.cs`）中。請依您的環境調整檔案路徑。

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Drawing;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the HTML document
            var htmlPath = @"C:\MyProject\Resources\input.html";
            var document = new HTMLDocument(htmlPath);

            // 2️⃣ Set rendering options – width, height, format, quality
            var renderingOptions = new ImageRenderingOptions
            {
                UseAntialiasing = true,
                Font = new Font("Arial", 12, WebFontStyle.Bold),
                TextOptions = new TextOptions { UseHinting = true },
                Width = 800,          // set image width
                Height = 600,         // set image height
                ImageFormat = ImageFormat.Png
            };

            // 3️⃣ Create the renderer
            var renderer = new ImageRenderer(renderingOptions);

            // 4️⃣ Render and save the PNG file
            var outputPath = @"C:\MyProject\Resources\output.png";
            renderer.Render(document, outputPath);

            Console.WriteLine($"HTML has been rendered to image: {outputPath}");
        }
    }
}
```

執行程式（`dotnet run` 或在 Visual Studio 按 **F5**）。執行完畢後，開啟 `output.png`——您將看到與 HTML 與 CSS 定義完全相同的渲染頁面。

## 常見問題與特殊情況

| Question | Answer |
|----------|--------|
| **如果我的 HTML 參考外部圖像或 CSS，該怎麼辦？** | Aspose.HTML 會依照 HTML 檔案所在位置的相對路徑尋找資源。請確保這些資源可被存取，或改用絕對 URL。 |
| **我可以渲染成 JPEG 而不是 PNG 嗎？** | 可以。將 `ImageFormat = ImageFormat.Jpeg`，並可選擇在 `ImageRenderingOptions` 中設定 `JpegQuality`。 |
| **如何從單一 HTML 檔案渲染多頁？** | 使用 `Document` 的分頁功能（`document.Pages`），並對每一頁呼叫 `renderer.Render(page, ...)`。 |
| **如果需要較高的 DPI 以供列印呢？** | 在建立渲染器之前，設定 `renderingOptions.DpiX` 與 `renderingOptions.DpiY`（例如 300）。 |
| **向量圖形是否必須使用抗鋸齒？** | 抗鋸齒可提升線條與曲線的平滑度，但若在大量批次處理時需要更快速度，可將其關閉（`UseAntialiasing = false`）。 |

## 效能提示 – 重複使用渲染器

若需在批次中轉換大量 HTML 檔案，請建立單一 `ImageRenderer` 實例並重複使用：

```csharp
var renderer = new ImageRenderer(renderingOptions);
foreach (var htmlFile in Directory.GetFiles(inputFolder, "*.html"))
{
    var doc = new HTMLDocument(htmlFile);
    var outFile = Path.ChangeExtension(htmlFile, ".png");
    renderer.Render(doc, outFile);
}
```

重複使用渲染器可避免重複分配內部資源，降低 CPU 與記憶體開銷。

## 結論

現在您已了解如何在 C# 中使用 Aspose.HTML **從 HTML 建立圖像**。透過以下四個步驟——載入文件、設定渲染選項（包含 **設定圖像寬度與高度**）、建立渲染器，最後 **將 HTML 渲染為圖像**——您即可可靠地 **將 HTML 轉換為 PNG**，並 **將 HTML 儲存為 PNG**，適用於縮圖、電子郵件預覽或 PDF 產生流程。

接下來，您可以探索：

* 使用不同格式（JPEG、BMP、GIF）**將 HTML 渲染為圖像**。
* 渲染後使用 `Graphics` 加入浮水印或覆蓋層。
* 將此轉換整合至 ASP.NET Core API，以提供即時圖像產生服務。

歡迎自行嘗試各種選項，讓 Aspose.HTML 的彈性為您處理繁重工作。祝開發愉快！

## 接下來您可以學習什麼？

以下教學涵蓋與本指南技術密切相關的主題，並以完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [HTML to Image Tutorial – Render HTML to PNG in C#](/html/english/net/generate-jpg-and-png-images/html-to-image-tutorial-render-html-to-png-in-c/)
- [Create PNG from HTML with Aspose.Html – Step‑by‑Step Guide](/html/english/net/generate-jpg-and-png-images/create-png-from-html-with-aspose-html-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}