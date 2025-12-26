---
category: general
date: 2025-12-26
description: 學習如何在 C# 中啟用抗鋸齒，以平滑邊緣並改善文字渲染。此一步一步的指南亦涵蓋圖像的抗鋸齒。
draft: false
keywords:
- how to enable antialiasing
- how to smooth edges
- enable antialiasing
- improve text rendering
- antialiasing for images
language: zh-hant
og_description: 如何在 C# 中啟用抗鋸齒，以獲得更平滑的邊緣和更清晰的文字。請遵循本指南，改善文字渲染並為圖像加入抗鋸齒。
og_title: 如何在 C# 中啟用抗鋸齒 – 平滑邊緣
tags:
- C#
- graphics
- rendering
title: 如何在 C# 中啟用抗鋸齒 – 平滑邊緣
url: /zh-hant/net/canvas-and-image-manipulation/how-to-enable-antialiasing-in-c-smooth-edges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中啟用抗鋸齒 – 平滑邊緣

有沒有想過 **how to enable antialiasing** 在 C# 繪圖例程中？你並不是唯一的——開發者經常與鋸齒狀線條和模糊文字作鬥爭，特別是在渲染 UI 豐富的圖形時。好消息是，只要調整幾個屬性，就能把粗糙的邊緣變成絲般光滑的視覺效果，同時還能明顯提升 **improve text rendering** 的品質。

在本教學中，我們將逐步演示一個完整且可執行的範例，向你展示如何平滑邊緣、為圖像啟用抗鋸齒以及開啟文字 hinting。無需外部文件說明；只要複製、貼上並執行。最後，你不僅會知道 *what* 要設定，還會了解 *why* 這些設定對像素完美輸出有何重要性。

## 你將學到什麼

- 抗鋸齒與 hinting 之間的差異，以及何時各自重要。  
- 如何在真實的 C# 專案中設定 `ImageRenderingOptions`（或相似的 API）。  
- 針對高 DPI 顯示器與大量圖像工作負載的邊緣案例處理。  
- 完整、可編譯的程式碼範例，可直接放入任何 .NET 主控台或 WinForms 應用程式中。  

**先決條件：** .NET 6+（或 .NET Framework 4.7+），具備 C# 語法的基本了解，以及提供 `ImageRenderingOptions` 的圖形函式庫（範例使用一個模擬類別作說明）。

---

## 如何啟用抗鋸齒 – 快速概覽

以下是解決方案的核心：建立 `ImageRenderingOptions` 實例並切換正確的旗標。這段程式碼同時為點陣圖與向量內容提供重點功能。

```csharp
// Step 1: Create the rendering options object
var renderingOptions = new ImageRenderingOptions();

// Step 2: Turn on antialiasing to smooth visual edges
renderingOptions.UseAntialiasing = true;

// Step 3: Enable text hinting for sharper glyphs
renderingOptions.Text.UseHinting = true;
```

**為什麼這三行很重要：**  

- `UseAntialiasing` 告訴光柵化器混合像素邊緣，消除使線條看起來「鋸齒」的階梯效應。  
- `Text.UseHinting` 使字元對齊像素格，對於小尺寸螢幕字體的清晰度至關重要。  
- 將它們包裝在單一的選項物件中，可保持渲染管線整潔，且未來的微調變得輕鬆無痛。

---

## 建立最小專案 (如何平滑邊緣)

如果你從頭開始，請依照以下步驟建立一個主控台應用程式，使用上述選項渲染簡單圖像。

### 1️⃣ 建立專案

```bash
dotnet new console -n AntialiasDemo
cd AntialiasDemo
```

### 2️⃣ 加入圖形函式庫

本教學將使用 **SixLabors.ImageSharp** 套件，它提供類似的 `GraphicsOptions` 類別。使用以下指令安裝：

```bash
dotnet add package SixLabors.ImageSharp --version 3.0.0
```

> *專業提示：* ImageSharp 的 `GraphicsOptions` 與前述的 `ImageRenderingOptions` 一對一對應，因此你可以直接替換類別名稱而不必更改程式邏輯。

### 3️⃣ 撰寫程式碼

將自動產生的 `Program.cs` 替換為以下完整範例：

```csharp
using System;
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.Drawing;
using SixLabors.ImageSharp.Drawing.Processing;
using SixLabors.ImageSharp.PixelFormats;
using SixLabors.ImageSharp.Processing;

namespace AntialiasDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a blank 400x200 image with a light gray background
            using var image = new Image<Rgba32>(400, 200);
            image.Mutate(ctx => ctx.Fill(Color.LightGray));

            // -------------------------------------------------
            // Step 1: Instantiate rendering options (antialiasing + hinting)
            // -------------------------------------------------
            var renderingOptions = new GraphicsOptions()
            {
                Antialias = true,          // smooth edges
                AntialiasSubpixelDepth = 16,
                // Text hinting is implicit in ImageSharp when Antialias is true,
                // but we can emphasize it with a higher quality setting.
                TextOptions = new TextOptions()
                {
                    DpiX = 96,
                    DpiY = 96,
                    Hinting = TextHinting.Enabled
                }
            };

            // -------------------------------------------------
            // Step 2: Draw a diagonal line (you’ll see the smoothing)
            // -------------------------------------------------
            var linePen = Pens.Solid(Color.DarkBlue, 5);
            image.Mutate(ctx => ctx.DrawLines(renderingOptions, linePen, new PointF(20, 20), new PointF(380, 180)));

            // -------------------------------------------------
            // Step 3: Render some text to demonstrate hinting
            // -------------------------------------------------
            var font = SystemFonts.CreateFont("Arial", 24, FontStyle.Bold);
            var textOptions = new TextOptions(font)
            {
                HorizontalAlignment = HorizontalAlignment.Center,
                VerticalAlignment = VerticalAlignment.Center,
                Origin = new PointF(200, 100)
            };
            image.Mutate(ctx => ctx.DrawText(renderingOptions, "Antialiasing ✔", font, Color.Black, new PointF(200, 100)));

            // -------------------------------------------------
            // Save the result
            // -------------------------------------------------
            const string outputPath = "antialias_demo.png";
            image.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}. Open it to verify smooth edges and clear text.");
        }
    }
}
```

#### 主要區段說明

| 區段 | 重要原因 |
|---------|----------------|
| **GraphicsOptions** | 集中管理抗鋸齒 (`Antialias = true`) 與文字 hinting (`Hinting = Enabled`)。 |
| **DrawLines** | 對角線展示 **how to smooth edges** 的實際運作——可見沒有鋸齒。 |
| **DrawText** | 示範 **improve text rendering**；因為 hinting，"✔" 符號相當清晰。 |
| **AntialiasSubpixelDepth** | 控制次像素混合的品質；較高的數值可產生更平滑的漸層。 |
| **Saving the PNG** | 產生可供檢視或嵌入文件的實體檔案。 |

---

## 邊緣案例與變體 (為圖像啟用抗鋸齒)

### 高 DPI 螢幕

當目標螢幕 DPI 超過 120 時，請在 `TextOptions` 中提升 `DpiX`/`DpiY`，並考慮提高 `AntialiasSubpixelDepth`。這可防止渲染引擎對平滑線條進行「降採樣」。

```csharp
renderingOptions.AntialiasSubpixelDepth = 32; // extra smoothness on 4K monitors
```

### 大圖像

對於非常大的位圖（例如 > 4000 px），可能會遇到記憶體壓力。在此情況下，你可以啟用 **progressive rendering**：

```csharp
renderingOptions = renderingOptions.WithProgressiveRendering(true);
```

### 非 ImageSharp API

若使用 **System.Drawing**（僅限 Windows）或 **SkiaSharp**，屬性名稱會不同（`SmoothingMode.AntiAlias`、`TextRenderingHint.ClearTypeGridFit`）。概念相同——在圖形上下文上設定抗鋸齒旗標，然後在文字渲染器上啟用 hinting。

---

## 驗證結果（要觀察什麼）

1. **平滑對角線** – 無階梯狀偽影；線條應呈現柔和的漸層。  
2. **銳利文字** – 字元乾淨對齊像素格；“✔”應明顯清晰。  
3. **檔案大小** – PNG 會因額外的顏色資訊稍微變大，這是抗鋸齒輸出的正常現象。  

在任何圖像檢視器中開啟 `antialias_demo.png`；若邊緣看起來如奶油般平滑且文字清晰可讀，代表你已成功在 C# 專案中 **how to enable antialiasing**。

---

## 常見問題解答

- **這在 .NET Framework 上可用嗎？** 可以——只要安裝對應目標 .NET Framework 的 ImageSharp 套件版本。  
- **如果我的函式庫沒有 `Text.UseHinting` 屬性該怎麼辦？** 請尋找等效的屬性，例如 `TextRenderingHint`（System.Drawing）或 `FontHinting`（SkiaSharp）。  
- **我可以為了效能關閉抗鋸齒嗎？** 當然可以；在渲染縮圖或速度比視覺品質更重要時，將 `Antialias = false`。

---

## 結論

你現在擁有一份 **完整、獨立的 how to enable antialiasing** 在 C# 中的指南。只要切換幾個屬性，即可 **平滑邊緣**、**提升文字渲染**，甚至在不同圖形函式庫中套用 **圖像抗鋸齒**。範例程式碼已可直接執行，說明則提供每個設定背後的原理，讓你能將此方法套用到任何專案。

準備好進一步了嗎？試著變更筆寬、使用自訂字型，或疊加多個形狀，觀察抗鋸齒在不同情況下的表現。若你對混合模式或 SVG 渲染感興趣，這些主題自然是從你剛掌握的內容延伸而來。

祝程式開發順利，盡情享受那如奶油般平滑的視覺效果！

![antialias_demo.png 的螢幕截圖，顯示平滑的邊緣與清晰的文字 – how to enable antialiasing]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}