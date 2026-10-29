---
category: general
date: 2026-04-06
description: 學習如何在 C# 中啟用抗鋸齒、設定影像寬度與高度，並將文件儲存為 PNG——快速指南，教你將文件匯出為影像。
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: zh-hant
og_description: 如何在匯出文件為圖像時啟用抗鋸齒。本指南示範如何設定圖像寬度、設定圖像高度，以及將文件儲存為 PNG。
og_title: 如何啟用抗鋸齒 – 將文件匯出為圖像
tags:
- C#
- ImageRendering
- Antialiasing
title: 如何啟用抗鋸齒 – 使用 C# 將文件匯出為圖像
url: /zh-hant/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何啟用抗鋸齒 – 在 C# 中將文件匯出為圖像

有沒有想過 **如何啟用抗鋸齒**，在把文件轉成圖片時保持平滑？也許您曾經只呼叫一次 `Save`，結果在對角線上看起來鋸齒分明。好消息是，您不需要圖形大師——只要幾行 C# 程式碼加上正確的選項即可。

在本教學中，我們將逐步說明設定圖像寬度、設定圖像高度，最後 **將文件儲存為 PNG**，讓您 **將文件匯出為圖像** 時擁有平滑的邊緣。完成後，您將得到一段可直接執行的程式碼，產生 800 × 600 的 PNG，且已開啟抗鋸齒。

## 前置條件

- .NET 6.0 或更新版本（此程式碼同樣適用於 .NET Framework 4.7 以上）  
- 參考支援 `ImageRenderingOptions` 的渲染函式庫（例如 Aspose.Words、Syncfusion，或任何提供類似屬性的 API）  
- 具備基本的 C# 語法概念  

不需要繁雜的設定——只要加入 NuGet 套件即可開始。

## 第一步：安裝渲染函式庫

首先，將套件加入您的專案。如果使用 Aspose.Words，執行：

```bash
dotnet add package Aspose.Words
```

> **專業提示：** 請保持函式庫版本為最新；截至 2026 年 4 月的最新發行版已加入抗鋸齒效能調整。

## 第二步：建立 Document 物件

載入或建立您想要渲染的文件。以下是一個最小範例，建立一個只有單一段落的單頁文件：

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

`Document` 類別是入口點，所有渲染皆由它產生。實務上您可能會載入既有的 .docx：

```csharp
// Document doc = new Document("input.docx");
```

## 第三步：定義渲染選項（寬度、高度、抗鋸齒）

現在來回答核心問題：**如何啟用抗鋸齒**。`ImageRenderingOptions` 物件讓您切換平滑化並控制尺寸。

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

請注意註解：它們明確說明 **設定圖像寬度**、**設定圖像高度**，以及 **UseAntialiasing**——這三個設定是取得精緻 PNG 的關鍵。

### 為什麼抗鋸齒很重要

若未啟用抗鋸齒，對角線與曲線會呈階梯狀，因為渲染器將每個像素視為「開」或「關」。開啟後會混合邊緣像素，產生類似相片編輯器的柔和效果。代價僅是極小的處理時間增加，對大多數 UI 匯出而言可忽略不計。

## 第四步：將文件儲存為 PNG（匯出文件為圖像）

設定完成後，我們終於 **將文件儲存為 PNG**。`Save` 方法接受檔案路徑與剛才配置好的選項。

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

就這樣——您的文件現在已是 800 × 600、已套用抗鋸齒的 PNG。打開 `output.png`，您會看到文字清晰、線條平滑，且沒有鋸齒痕跡。

### 驗證結果

您可以在任何圖像檢視器中快速檢查檔案。留意以下項目：

- 正確的尺寸 (800 × 600)  
- 文字或圖形上沒有可見的階梯邊緣  
- 若文件未設定背景色，則背景應為透明（大多數函式庫預設為白色）

如果圖像仍顯得鋸齒，請再次確認 `UseAntialiasing = true` 沒有在其他地方被覆寫。

## 第五步：邊緣情況與變形

### 更換輸出格式

想要 JPEG 而非 PNG？只要更改副檔名，並視需要調整壓縮設定：

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### 匯出多頁文件

當來源文件有多頁時，渲染器預設會為每一頁產生獨立的圖像檔。您可以透過迴圈逐頁處理：

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### 儲存至串流（例如 HTTP 回應）

若您在建構 Web API，可能想直接回傳 PNG：

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## 完整範例程式

以下是完整、可直接複製貼上的程式碼，涵蓋上述所有步驟：

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

執行此程式後，會在執行檔所在資料夾產生 `output.png`。開啟它，您會看到一張平滑的 800 × 600 PNG——正是我們想要的結果。

## 常見問題與除錯

- **圖像看起來模糊怎麼辦？**  
  模糊通常是因為將較小的來源頁面放大。請將來源頁面尺寸盡量接近目標尺寸，或透過 `imageOptions.Resolution` 提高 DPI（例如 `Resolution = 300`）。

- **這能在 .NET Framework 上執行嗎？**  
  能。相同的 API 也存在於傳統框架，只要引用對應的 DLL 即可。

- **可以自行設定背景顏色嗎？**  
  當然可以。在儲存前設定 `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;`。

- **抗鋸齒是硬體加速的嗎？**  
  大多數函式庫使用軟體抗鋸齒。若需要 GPU 加速，請尋找明確支援此功能的渲染引擎。

## 結論

我們已說明 **如何啟用抗鋸齒**，在 **將文件匯出為圖像** 時，並示範 **設定圖像寬度**、**設定圖像高度**，最後 **將文件儲存為 PNG** 的完整步驟。上述程式碼已可直接投入生產環境，您亦可自行改為 JPEG、多頁 PDF，或直接將圖像串流回客戶端。

接下來，您可以嘗試加入浮水印、調整 DPI 以符合列印品質，或將此邏輯整合至 ASP.NET Core 端點。原理相同——只要把檔案路徑換成回應串流即可。

祝開發順利，享受那清晰、抗鋸齒的圖像吧！

![已啟用抗鋸齒的 PNG 渲染圖](output.png "已啟用抗鋸齒的 PNG 渲染圖")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}