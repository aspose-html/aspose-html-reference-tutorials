---
category: general
date: 2026-10-09
description: 建立 imagerenderingoptions 實例以啟用抗鋸齒並提升 .NET 應用程式的圖形渲染品質。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create imagerenderingoptions instance
- ImageRenderingOptions
- antialiasing
- SmoothingMode
- graphics rendering
language: zh-hant
lastmod: 2026-10-09
og_description: 建立 ImageRenderingOptions 實例以啟用抗鋸齒，實現 .NET 中更平滑的圖形渲染。請遵循逐步指南。
og_image_alt: Screenshot showing smooth edges after enabling antialiasing with ImageRenderingOptions
og_title: 建立 ImageRenderingOptions 實例 – 提升 .NET 圖形品質
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  headline: Create imagerenderingoptions instance for high‑quality graphics rendering
  type: TechArticle
- description: Create imagerenderingoptions instance to enable antialiasing and improve
    graphics rendering quality in .NET applications.
  name: Create imagerenderingoptions instance for high‑quality graphics rendering
  steps:
  - name: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
    text: '**Forgetting to pass the options** – Rendering methods that accept `ImageRenderingOptions`
      will ignore antialiasing if you call the overload without the options parameter.
      Always use the three‑parameter `GetThumbnail` or equivalent method.'
  - name: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
    text: '**Mixing SmoothingMode with ImageRenderingOptions** – Setting `Graphics.SmoothingMode`
      has no effect on Aspose.Slides rendering. Rely solely on `UseAntialiasing`.'
  - name: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
    text: '**Using an outdated library version** – `ImageRenderingOptions` was introduced
      in Aspose.Slides 20.5. Ensure your NuGet package is up‑to‑date; otherwise the
      class may be missing or lack the `UseAntialiasing` property.'
  type: HowTo
tags:
- .NET
- C#
- rendering
title: 建立 imagerenderingoptions 實例以進行高質素圖形渲染
url: /zh-hant/net/canvas-and-image-manipulation/create-imagerenderingoptions-instance-for-high-quality-graph/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立高品質圖形渲染的 ImageRenderingOptions 實例

如果您需要 **建立 ImageRenderingOptions 實例** 以產生更平滑的圖形，本指南會一步步說明。透過設定抗鋸齒 (antialiasing) 可消除鋸齒邊緣，取得專業等級的輸出，且不需額外函式庫。

您將學會如何實例化 `ImageRenderingOptions`、開啟抗鋸齒，並將選項套用至如 Aspose.Slides 或 System.Drawing 等渲染引擎。本文假設您已熟悉基本的 C# 語法，且具備 .NET 開發環境。

## 前置條件

- .NET 6.0 或更新版本（此 API 在 .NET Standard 2.0+ 可用）
- 參考包含 `ImageRenderingOptions` 的組件（例如 `Aspose.Slides.NET`）
- 使用 Visual Studio 2022 或已安裝 C# 擴充功能的 VS Code 等 IDE
- 基本的圖形渲染管線概念

## 步驟 1：建立 ImageRenderingOptions 實例

第一步是配置一個新的 `ImageRenderingOptions` 物件。此物件充當所有渲染相關旗標的容器。

```csharp
using Aspose.Slides;          // Replace with the appropriate namespace
using Aspose.Slides.Export;   // Needed for ImageRenderingOptions

// Step 1: Create the ImageRenderingOptions instance
ImageRenderingOptions imgOptions = new ImageRenderingOptions();
```

建立實例後，您即可完整掌控向量圖形的光柵化方式。之後可依需求開啟或關閉特定功能，例如抗鋸齒、文字渲染模式或影像壓縮。

## 步驟 2：啟用抗鋸齒以提升圖形渲染品質

抗鋸齒會平滑像素顏色之間的過渡，減少對角線或曲線上的階梯效應。較舊的 `SmoothingMode` 屬性已不建議使用；`UseAntialiasing` 為現代且推薦的做法。

```csharp
// Step 2: Turn on antialiasing for smoother output
imgOptions.UseAntialiasing = true;
```

將 `UseAntialiasing` 設為 `true`，即告訴渲染引擎在光柵化時套用高品質濾鏡。此旗標同時適用於向量圖形與文字，確保投影片的視覺一致性。

### 為何不使用 SmoothingMode？

`SmoothingMode` 屬於 `System.Drawing.Graphics`，僅影響 GDI+ 繪圖。當您透過 Aspose.Slides 轉換投影片或 PDF 時，`ImageRenderingOptions.UseAntialiasing` 是唯一被函式庫識別的旗標。使用較新的屬性可確保向前相容，並避免在非 Windows 平台上出現不可預期的行為。

## 步驟 3：將選項套用至渲染作業

當 `ImageRenderingOptions` 實例完成設定後，將其傳遞給執行實際渲染的方法。以下是一個完整且可執行的範例，示範如何載入簡報、將第一張投影片渲染為 PNG，並以啟用抗鋸齒的方式儲存影像。

```csharp
using System;
using Aspose.Slides;
using Aspose.Slides.Export;

class Program
{
    static void Main()
    {
        // Load a sample presentation
        using Presentation pres = new Presentation("sample.pptx");

        // Create and configure ImageRenderingOptions
        ImageRenderingOptions imgOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true   // Enable antialiasing
        };

        // Render the first slide to a PNG file
        Slide slide = pres.Slides[0];
        slide.GetThumbnail(2f, 2f, imgOptions)   // 2x scale for higher resolution
            .Save("slide1_antialiased.png", Export.SaveFormat.Png);

        Console.WriteLine("Slide rendered with antialiasing.");
    }
}
```

**關鍵程式碼說明**

- `new Presentation("sample.pptx")` 讀取來源檔案。  
- `GetThumbnail(2f, 2f, imgOptions)` 以雙倍預設 DPI 產生投影片的位圖，同時套用先前設定的渲染選項。  
- 產生的 PNG (`slide1_antialiased.png`) 因 `UseAntialiasing = true` 而呈現平滑的曲線與文字。

### 預期輸出

在任意影像檢視器中開啟 `slide1_antialiased.png`。與未使用抗鋸齒的渲染結果比較，您會注意到：

- 形狀的圓角不會出現鋸齒。  
- 文字邊緣清晰且略帶柔和，消除像素化瑕疵。  
- 整體視覺品質與原始 PowerPoint 觀看效果相符。

## 步驟 4：進階圖形渲染的可選調整

雖然抗鋸齒是最常用的旗標，`ImageRenderingOptions` 仍提供其他控制項：

| Property | Purpose | Typical value |
|----------|---------|---------------|
| `UseHighQualityRendering` | 為文字啟用次像素渲染 | `true` |
| `PixelFormat` | 決定輸出位圖的色深 | `PixelFormat.Format32bppArgb` |
| `ImageFormat` | 設定目標影像格式（PNG、JPEG 等） | `Export.SaveFormat.Png` |

您可以將這些設定串接使用：

```csharp
imgOptions.UseHighQualityRendering = true;
imgOptions.PixelFormat = System.Drawing.Imaging.PixelFormat.Format32bppArgb;
```

**專業提示：** 產生大尺寸 PDF 或高解析度 PNG 時，建議保留 `UseAntialiasing`，但同時留意記憶體使用量。抗鋸齒會增加額外的處理開銷，在低階機器上可能較為明顯。

## 常見陷阱與避免方法

1. **忘記傳遞選項** – 接受 `ImageRenderingOptions` 的渲染方法若未提供此參數，將不會套用抗鋸齒。務必使用三參數的 `GetThumbnail` 或等效方法。  
2. **同時使用 SmoothingMode 與 ImageRenderingOptions** – 設定 `Graphics.SmoothingMode` 對 Aspose.Slides 的渲染毫無影響，請僅依賴 `UseAntialiasing`。  
3. **使用過舊的函式庫版本** – `ImageRenderingOptions` 於 Aspose.Slides 20.5 版首次加入。請確保 NuGet 套件為最新版本，否則可能找不到此類別或缺少 `UseAntialiasing` 屬性。

## 結論

您現在已掌握 **建立 ImageRenderingOptions 實例**、開啟抗鋸齒，並將其整合至渲染工作流程的完整步驟。此方式可確保圖形渲染更平滑，取代傳統的 `SmoothingMode` 設定，且在各 .NET 平台上表現一致。

接下來，您可以探索其他渲染旗標、嘗試不同 DPI 比例，或結合 PDF 匯出以產生列印品質的資產。精通 `ImageRenderingOptions` 是高保真 .NET 圖形程式設計的基石。

---


## 接下來該學什麼？

以下教學與本指南所示技術緊密相關，提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中嘗試其他實作方式。

- [Create PNG from HTML – Full C# Rendering Guide](/html/english/net/rendering-html-documents/create-png-from-html-full-c-rendering-guide/)
- [Create image from HTML in C# – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/create-image-from-html-in-c-complete-step-by-step-guide/)
- [Create canvas text – Full Guide to Rendering Text on Images](/html/english/net/canvas-and-image-manipulation/create-canvas-text-full-guide-to-rendering-text-on-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}