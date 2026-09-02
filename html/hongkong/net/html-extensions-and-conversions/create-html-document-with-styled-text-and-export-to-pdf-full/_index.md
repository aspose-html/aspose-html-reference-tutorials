---
category: general
date: 2025-12-29
description: 在 C# 中建立 HTML 文件，學習如何設定字型、字型大小，然後使用 Aspose.HTML 將 HTML 儲存為 PDF 或將 HTML
  轉換為 PDF。
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: zh-hant
og_description: 在 C# 中建立 HTML 文件，即時查看如何設定字型、字型大小，然後使用 Aspose.HTML 將 HTML 儲存為 PDF 或將
  HTML 轉換為 PDF。
og_title: 建立 HTML 文件 – 文字樣式與 PDF 匯出
tags:
- aspnet
- csharp
- pdf-generation
title: 建立具樣式文字的 HTML 文件並匯出為 PDF – 完整指南
url: /zh-hant/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立帶樣式文字的 HTML 文件並匯出為 PDF

是否曾需要即時 **create HTML document** 並在不離開 C# 程式碼的情況下將其轉換為 PDF？也許您正在構建報表引擎、發票產生器，或僅僅為使用者提供快速預覽。好消息是，只需幾行程式碼即可使用 Aspose.HTML 完成，且您可以完整控制字體系列、字體大小，甚至粗斜體樣式。

在本教學中，我們將逐步說明整個流程——從建立記憶體中的 HTML 文件到將其儲存為 PDF 檔案。完成後，您將清楚知道如何 **set font family**、**set font size**，以及 **save HTML as PDF**（亦即 **convert HTML to PDF**），並提供乾淨、可投入生產的程式碼範例。

## 您需要的條件

- .NET 6+（此 API 同時支援 .NET Core 與 .NET Framework）  
- Aspose.HTML for .NET NuGet 套件 (`Aspose.Html`) – 透過 `dotnet add package Aspose.Html` 安裝  
- 一個磁碟上的資料夾，用於寫入產生的 PDF  

![create html document illustration](/images/create-html-document.png){alt="建立 HTML 文件範例"}

## Step 1: Create the HTML Document

首先，我們需要一個空的 HTML document 物件。可將其視為一張全新的畫布，稍後您將在其上繪製帶樣式的段落。

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Why this matters:** `HTMLDocument` 為您提供類似 DOM 的結構，可以程式方式操作。直到最後一步才需要處理原始字串或檔案 I/O。

## Step 2: Add a Paragraph and Set Font Family & Font Size

現在，我們將建立 `<p>` 元素，插入文字，並明確定義字體系列與大小。這正是 **set font family** 與 **set font size** 關鍵字發揮作用的地方。

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Pro tip:** 若需要網頁安全備援字體，可提供以逗號分隔的清單，例如 `"Arial, Helvetica, sans-serif"`；瀏覽器（或 Aspose）會選取第一個可用的字體。

## Step 3: Apply Bold and Italic Styling with WebFontStyle Flags

Aspose.HTML 提供便利的列舉 `WebFontStyle`，讓您可透過位元 OR 結合樣式。讓我們將文字同時設定為粗體 **and** 斜體。

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**What’s happening under the hood?** `FontStyle` 屬性會轉換為 CSS 的 `font-weight` 與 `font-style` 宣告。透過 OR 合併標誌，我們避免撰寫兩行獨立的 CSS。

## Step 4: Convert the HTML to PDF (Save HTML as PDF)

最後一步是實際的轉換。只要呼叫一次 `Save`，Aspose.HTML 即會渲染 DOM 並將 PDF 檔寫入磁碟。這同時滿足 **save html as pdf** 與 **convert html to pdf** 兩項需求。

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Expected result:** 開啟 `styled.pdf`，您會看到一段文字 “Bold & Italic text”，使用 18‑px Arial，呈現粗體與斜體。PDF 尺寸符合標準 A4，且文字可選取——得益於向量渲染。

## Full Working Example

將所有步驟整合，以下是完整、可直接執行的程式：

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### Running the code

1. 安裝 Aspose.HTML NuGet 套件：  
   ```bash
   dotnet add package Aspose.Html
   ```
2. 將 `C:\Temp\styled.pdf` 替換為您有寫入權限的資料夾。  
3. 建置並執行：`dotnet run`。  

您應會在主控台看到確認檔案位置的訊息，且 PDF 內將包含已套用樣式的段落。

## Common Questions & Edge Cases

- **What if I need a custom web font?**  
  在建立段落之前，使用 `HTMLFontFaceRule` 載入字體或參考遠端的 `@font-face` CSS 檔案。

- **Can I add images before converting?**  
  當然可以。使用 `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");`，並將 `img.Source` 設為本機路徑或 data URI。

- **What about multi‑page PDFs?**  
  新增更多元素（表格、div 等），當內容超過頁面高度時，Aspose.HTML 會自動分頁。

- **Is there a way to control PDF metadata?**  
  傳入 `PdfSaveOptions` 實例，並設定 `Author`、`Title` 或 `PdfAConformanceLevel` 等屬性。

## Recap

我們已說明如何在 C# 中 **create HTML document**、**set font family**、**set font size**，套用粗斜體樣式，最後 **save HTML as PDF**——即以 Aspose.HTML **convert HTML to PDF**。此程式碼片段足夠簡潔，可直接嵌入任何 .NET 專案，同時也足夠完整，作為更複雜報表情境的堅實基礎。

## Next Steps

- 嘗試使用 CSS 類別以實現可重複使用的樣式。  
- 結合多個段落、表格與圖片，打造更豐富的 PDF。  
- 若需保存等級的文件，可探索 PDF/A 相容性。  

隨意調整字體、大小或顏色——程式化產生的內容沒有任何限制。祝開發愉快，願您的 PDF 總能如您所想精確呈現！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}