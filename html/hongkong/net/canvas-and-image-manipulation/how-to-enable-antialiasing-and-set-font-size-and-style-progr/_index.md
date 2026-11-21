---
category: general
date: 2026-11-20
description: 如何在 C# 圖形中啟用抗鋸齒，並以程式方式設定字型大小與字型樣式，提供使用 ImageRenderingOptions 的完整可執行範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- set font size
- set font style programmatically
- C# graphics rendering
- ImageRenderingOptions example
language: zh-hant
lastmod: 2026-11-20
og_description: 如何在 C# 圖形中啟用抗鋸齒、設定字體大小以及以程式方式設定字體樣式，使用 ImageRenderingOptions – 完整程式碼與說明。
og_image_alt: Screenshot of antialiased text with custom font size and style generated
  by C# code showing how to enable antialiasing
og_title: 如何在 C# 中啟用抗鋸齒並以程式方式設定字型大小與樣式
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to enable antialiasing in C# graphics and set font size, set font
    style programmatically with a complete, runnable example using ImageRenderingOptions.
  headline: How to enable antialiasing and set font size and style programmatically
    in C#
  type: TechArticle
tags:
- C#
- graphics
- antialiasing
- fonts
title: 如何在 C# 中以程式方式啟用抗鋸齒並設定字型大小與樣式
url: /zh-hant/net/canvas-and-image-manipulation/how-to-enable-antialiasing-and-set-font-size-and-style-progr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中以程式方式啟用抗鋸齒並設定字體大小與樣式

在 C# 圖形中啟用抗鋸齒是常見需求，當您需要形狀或文字的平滑邊緣時。本教學將示範如何使用 **ImageRenderingOptions** 類別以程式方式啟用抗鋸齒、設定字體大小以及設定字體樣式。完成本指南後，您將擁有一個獨立的主控台應用程式，能將清晰、具樣式的文字渲染至影像檔案。

您將學會如何配置渲染管線、選擇適當的字體系列、調整字體大小，並在程式碼中直接套用粗體或斜體樣式。唯一的前置條件是近期的 .NET SDK 以及 Aspose.Imaging NuGet 套件，範例會自動安裝該套件。

## 前置條件

- .NET 6.0 SDK 或更新版本（下載自 https://dotnet.microsoft.com/）
- Visual Studio 2022 或任何支援 .NET 專案的編輯器
- **Aspose.Imaging** NuGet 套件（提供 `ImageRenderingOptions` 的函式庫）

您可以使用以下指令加入套件：

```bash
dotnet add package Aspose.Imaging
```

## 使用 ImageRenderingOptions 啟用抗鋸齒

`ImageRenderingOptions` 是控制 Aspose.Imaging 繪製圖形的核心物件。設定其 `UseAntialiasing` 屬性會指示光柵化器平滑邊緣，從而消除關閉抗鋸齒時出現的鋸齒「階梯」效應。

```csharp
// Step 1: Create a new ImageRenderingOptions instance
ImageRenderingOptions renderingOptions = new ImageRenderingOptions();

// Step 2: Enable antialiasing for smoother graphics
renderingOptions.UseAntialiasing = true;
```

啟用抗鋸齒對於高品質的 UI 元素、圖表渲染以及任何對視覺忠實度有要求的情境皆相當重要。

## 以程式方式設定字體大小

字體大小決定最終點陣圖中字形的顯示尺寸。您可以透過建立帶有指定點大小的 `Font` 物件來變更它。以下範例將大小設定為 **24 pt**，這是常見的可讀標題尺寸。

```csharp
// Step 3: Choose a font family and size
Font font = new Font("Arial", 24); // 24‑point Arial
```

您可以將 `24` 替換為任意整數或浮點數，以符合版面需求。若需要以像素為單位的尺寸，`Font` 類別亦接受 `GraphicsUnit` 參數。

## 以程式方式設定字體樣式

在建立 `Font` 時傳入 `WebFontStyle` 標誌即可套用粗體、斜體或底線樣式。`WebFontStyle` 列舉透過位元 OR 運算結合多種樣式。

```csharp
// Step 4: Apply bold and italic styles
font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);
```

若僅需單一樣式，可使用 `WebFontStyle.Bold`、`WebFontStyle.Italic` 或 `WebFontStyle.Underline`。此方式讓您能 **以程式方式設定字體樣式**，而無需硬編碼不同的字體檔案。

## 完整可執行範例

以下是一個完整的主控台應用程式，將所有步驟整合在一起：

```csharp
using System;
using Aspose.Imaging;
using Aspose.Imaging.Brushes;
using Aspose.Imaging.ImageOptions;
using Aspose.Imaging.Sources;
using Aspose.Imaging.FileFormats.Png;
using Aspose.Imaging.Graphics;
using Aspose.Imaging.Fonts;
using Aspose.Imaging.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Create rendering options and enable antialiasing
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            // Enable hinting for sharper text on low‑resolution images
            TextOptions = new TextOptions { UseHinting = true }
        };

        // 2️⃣ Define the font (size + style)
        Font font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);

        // 3️⃣ Prepare a bitmap with a white background
        int width = 800;
        int height = 200;
        using (var bitmap = new RasterImage(width, height, PixelFormat.Format24bppRgb))
        {
            bitmap.SaveOptions = new PngOptions { ColorType = PngColorType.Truecolor };
            bitmap.Fill(new SolidBrush(Color.White));

            // 4️⃣ Create a graphics object that respects our rendering options
            using (Graphics graphics = new Graphics(bitmap, renderingOptions))
            {
                // Position the text in the center of the image
                PointF location = new PointF(50, 80);
                graphics.DrawString("Antialiased Bold Italic Text", font, new SolidBrush(Color.Black), location);
            }

            // 5️⃣ Save the result
            string outputPath = "antialiased_text.png";
            bitmap.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}");
        }
    }
}
```

### 各區段說明

| 區段 | 重要原因 |
|---------|----------------|
| **Rendering options** | 啟用 `UseAntialiasing` 可確保向量圖形與文字的邊緣平滑。 |
| **TextOptions.UseHinting** | Hinting 透過調整字形輪廓，提高低解析度輸出的可讀性。 |
| **Font construction** | `Font` 建構子在一次呼叫中同時結合 **設定字體大小** 與 **以程式方式設定字體樣式**。 |
| **Graphics object** | 將 `renderingOptions` 傳遞給 `Graphics` 可確保所有繪圖操作皆遵循抗鋸齒與 hinting 設定。 |
| **DrawString** | 此方法使用已設定的字體渲染文字，產生最終的抗鋸齒輸出。 |
| **Saving** | PNG 格式保留精確的像素資料，不會產生額外的壓縮雜訊。 |

#### 預期輸出

執行程式後會產生 **antialiased_text.png**，其外觀如下：

![Antialiased text example](https://example.com/antialiased_text.png "Antialiased text with custom font size and style – how to enable antialiasing")

此影像顯示以 24 pt 渲染的清晰、粗斜體 Arial 文字，邊緣平滑，證實 **如何啟用抗鋸齒** 已如預期運作。

## 常見變體與邊緣情況

- **不同的字體系列** – 將 `"Arial"` 替換為任何已安裝的字體名稱（例如 `"Times New Roman"`）。若字體不存在，Aspose.Imaging 會拋出 `FontNotFoundException`。
- **變更字體大小** – 調整 `Font` 建構子的第二個參數為任意浮點值。較大的數值提升可讀性，但可能需要更大的點陣圖。
- **多重樣式** – 使用 `|` 運算子結合 `WebFontStyle.Underline`、`Bold` 與 `Italic`：`WebFontStyle.Bold | WebFontStyle.Underline`。
- **高 DPI 渲染** – 若需 Retina 風格的輸出，可在保持相同字體大小的前提下增大點陣圖尺寸（例如 1600 × 400），抗鋸齒仍會產生平滑效果。
- **停用抗鋸齒** – 設定 `renderingOptions.UseAntialiasing = false;` 以比較視覺差異。文字將呈現鋸齒狀，對除錯或效能測試有幫助。

## 專業提示

- **快取 `Font` 物件**，若在迴圈中繪製多個字串；每次迭代重新建立 `Font` 會增加開銷。
- **將 `TextOptions.UseHinting` 與抗鋸齒同時使用**，可在低解析度影像上取得銳利度與平滑度的最佳平衡。
- **驗證輸出檔案**，可使用能顯示像素細節的影像檢視器（如 Photoshop 或 GIMP）開啟。這有助於確認抗鋸齒確實生效。

## 結論

現在您已了解如何在 C# 圖形中 **啟用抗鋸齒**、如何 **設定字體大小**，以及如何使用 `ImageRenderingOptions` **以程式方式設定字體樣式**。完整範例展示了一套實用工作流程，您可直接套用於自己的專案，無論是產生圖表、製作 UI 縮圖，或為 Web 服務產生動態圖形。

接下來，您可以探索 **以程式方式設定字體顏色**、加入 **漸層填色**，或使用相同的抗鋸齒設定來渲染 **向量圖形**。所有這些主題皆建立在本指南的基礎上，讓您能夠完全以程式碼創建高品質圖形。祝您渲染愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助您精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 C# 中將 HTML 渲染為 PNG 時啟用抗鋸齒](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-when-rendering-html-to-png-in-c/)
- [如何在 C# 中為 HTML 圖像渲染啟用抗鋸齒](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-for-html-image-rendering-in-c/)
- [如何在 Aspose HTML 轉 PDF 轉換中啟用抗鋸齒 (C#)](/html/english/net/html-extensions-and-conversions/how-to-enable-antialiasing-in-aspose-html-to-pdf-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}