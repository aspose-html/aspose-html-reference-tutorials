---
category: general
date: 2026-03-02
description: 學習如何啟用抗鋸齒，並在使用 hinting 時以程式方式套用粗體，同時一次設定多種字型樣式。
draft: false
keywords:
- how to enable antialiasing
- how to apply bold
- how to use hinting
- set font style programmatically
- set multiple font styles
language: zh-hant
og_description: 了解如何在 C# 中以程式方式啟用抗鋸齒、套用粗體以及使用 hinting，並設定多種字型樣式。
og_title: 如何在 C# 中啟用抗鋸齒 – 完整字體樣式指南
tags:
- C#
- graphics
- text rendering
title: 如何在 C# 中啟用抗鋸齒 – 完整字體樣式指南
url: /zh-hant/net/canvas-and-image-manipulation/how-to-enable-antialiasing-in-c-complete-font-style-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中啟用抗鋸齒 – 完整字體樣式指南

有沒有想過 **如何在 .NET 應用程式中啟用抗鋸齒** 來繪製文字？你並不是唯一有此疑問的人。大多數開發者在高 DPI 螢幕上看到 UI 顯得鋸齒狀時，都會卡關，而解決方法往往隱藏在幾個屬性切換之中。在本教學中，我們將一步步說明如何開啟抗鋸齒、**如何套用粗體**，甚至 **如何使用 hinting** 讓低解析度螢幕仍保持清晰。完成後，你將能 **以程式方式設定字體樣式**，並且 **一次結合多種字體樣式**，毫不費力。

我們會涵蓋所有必備資訊：所需的命名空間、完整可執行範例、每個旗標的意義，以及可能遇到的幾個坑。無需外部文件，直接把本指南複製貼上到 Visual Studio，即可立即看到效果。

## 前置條件

- .NET 6.0 或更新版本（使用的 API 屬於 `System.Drawing.Common` 以及一個小型輔助函式庫）
- 基本的 C# 知識（了解 `class` 與 `enum` 為何物）
- 任一 IDE 或文字編輯器（Visual Studio、VS Code、Rider…皆可）

如果你已具備上述條件，讓我們直接開始吧。

---

## 如何在 C# 文字繪製中啟用抗鋸齒

平滑文字的核心在於 `Graphics` 物件的 `TextRenderingHint` 屬性。將它設為 `ClearTypeGridFit` 或 `AntiAlias` 即可告訴渲染器混合像素邊緣，消除階梯狀效果。

```csharp
using System;
using System.Drawing;
using System.Drawing.Text;   // for TextRenderingHint
using System.Windows.Forms; // for a quick demo form

public class AntialiasDemo : Form
{
    protected override void OnPaint(PaintEventArgs e)
    {
        base.OnPaint(e);

        // Step 3: Enable antialiasing for smoother glyph edges
        e.Graphics.TextRenderingHint = TextRenderingHint.AntiAlias;
        // You could also use ClearTypeGridFit for LCD screens:
        // e.Graphics.TextRenderingHint = TextRenderingHint.ClearTypeGridFit;

        // Draw sample text so you can see the effect
        e.Graphics.DrawString(
            "Antialiased Text",
            new Font("Segoe UI", 24, FontStyle.Regular),
            Brushes.Black,
            new PointF(20, 20));
    }

    [STAThread]
    public static void Main()
    {
        Application.Run(new AntialiasDemo());
    }
}
```

**為什麼這樣有效：** `TextRenderingHint.AntiAlias` 會強制 GDI+ 引擎將字形邊緣與背景混合，產生更平滑的外觀。在現代 Windows 機器上這通常是預設值，但許多自訂繪圖情境會把提示重設為 `SystemDefault`，因此我們需要明確設定。

> **專業小技巧：** 若你的目標是高 DPI 螢幕，請搭配 `Graphics.ScaleTransform` 使用 `AntiAlias`，以確保文字在縮放後仍保持銳利。

### 預期結果

執行程式後，會開啟一個視窗顯示「Antialiased Text」且無鋸齒。若將相同字串在未設定 `TextRenderingHint` 的情況下繪製，差異將十分明顯。

---

## 如何以程式方式套用粗體與斜體字體樣式

套用粗體（或其他樣式）不只是設定一個布林值；你必須結合 `FontStyle` 列舉中的旗標。前面的程式碼片段使用了自訂的 `WebFontStyle` 列舉，但原理與 `FontStyle` 完全相同。

```csharp
// Step 1: Create a CSS‑style container (simulated with FontStyle)
FontStyle combinedStyle = FontStyle.Bold | FontStyle.Italic;

// Step 2: Apply bold and italic font styles using the enum
Font styledFont = new Font("Segoe UI", 28, combinedStyle);
```

在實務上，你可能會把樣式存入設定物件，稍後再套用：

```csharp
public class TextOptions
{
    public FontStyle FontStyle { get; set; } = FontStyle.Regular;
    public bool UseAntialiasing { get; set; } = false;
    public bool UseHinting { get; set; } = false;
}
```

然後在繪製時使用：

```csharp
var options = new TextOptions
{
    FontStyle = FontStyle.Bold | FontStyle.Italic,
    UseAntialiasing = true,
    UseHinting = true
};

Font font = new Font("Segoe UI", 24, options.FontStyle);
if (options.UseAntialiasing)
    e.Graphics.TextRenderingHint = TextRenderingHint.AntiAlias;
if (options.UseHinting)
    e.Graphics.TextRenderingHint = TextRenderingHint.SingleBitPerPixelGridFit;

// Draw with the configured font
e.Graphics.DrawString("Bold & Italic", font, Brushes.DarkBlue, new PointF(20, 80));
```

**為什麼要結合旗標？** `FontStyle` 是位元欄位列舉（bit‑field enum），每種樣式（Bold、Italic、Underline、Strikeout）佔用不同的位元。使用位元 OR（`|`）即可在不覆寫先前選項的情況下疊加多種樣式。

---

## 如何在低解析度螢幕上使用 Hinting

Hinting 會將字形輪廓微調至像素格線對齊，這在螢幕無法呈現次像素細節時尤為重要。在 GDI+ 中，hinting 透過 `TextRenderingHint.SingleBitPerPixelGridFit` 或 `ClearTypeGridFit` 來控制。

```csharp
// Step 4: Turn on hinting to improve text rendering on low‑resolution displays
if (options.UseHinting)
{
    // SingleBitPerPixelGridFit works well on older LCD panels
    e.Graphics.TextRenderingHint = TextRenderingHint.SingleBitPerPixelGridFit;
}
```

### 何時使用 hinting

- **低 DPI 螢幕**（例如 96 dpi 的傳統顯示器）
- **點陣字型**（每個像素都很重要的情況）
- **對效能要求高的應用程式**（完整抗鋸齒過於耗資）

如果同時啟用抗鋸齒 *與* hinting，渲染器會先優先處理 hinting，然後再套用平滑。順序很重要；若希望 hinting 作用於已平滑的字形，請在設定抗鋸齒之後 **再設定 hinting**。

---

## 一次設定多種字體樣式 – 實作範例

把前面的步驟全部結合，以下是一個精簡示範，會：

1. **啟用抗鋸齒**（`how to enable antialiasing`）
2. **套用粗體與斜體**（`how to apply bold`）
3. **開啟 hinting**（`how to use hinting`）
4. **一次設定多種字體樣式**（`set multiple font styles`）

```csharp
using System;
using System.Drawing;
using System.Drawing.Text;
using System.Windows.Forms;

public class FullStyleDemo : Form
{
    private readonly TextOptions _options = new()
    {
        FontStyle = FontStyle.Bold | FontStyle.Italic,
        UseAntialiasing = true,
        UseHinting = true
    };

    protected override void OnPaint(PaintEventArgs e)
    {
        base.OnPaint(e);

        // Apply antialiasing if requested
        if (_options.UseAntialiasing)
            e.Graphics.TextRenderingHint = TextRenderingHint.AntiAlias;

        // Apply hinting after antialiasing
        if (_options.UseHinting)
            e.Graphics.TextRenderingHint = TextRenderingHint.SingleBitPerPixelGridFit;

        // Build the font with multiple styles
        using Font font = new Font("Segoe UI", 30, _options.FontStyle);

        // Render the text
        e.Graphics.DrawString(
            "Bold + Italic + Hinted",
            font,
            Brushes.DarkGreen,
            new PointF(20, 20));
    }

    [STAThread]
    public static void Main()
    {
        Application.Run(new FullStyleDemo());
    }
}
```

#### 你應該會看到的畫面

視窗會以深綠色顯示 **Bold + Italic + Hinted**，文字因抗鋸齒而平滑，因 hinting 而對齊格線。若將任一旗標註解掉，文字將變得鋸齒（無抗鋸齒）或稍微錯位（無 hinting）。

---

## 常見問題與邊緣案例

| 問題 | 解答 |
|----------|--------|
| *如果目標平台不支援 `System.Drawing.Common`，該怎麼辦？* | 在 .NET 6+ 的 Windows 上仍可使用 GDI+。若需跨平台圖形，請考慮 SkiaSharp——它提供類似的抗鋸齒與 hinting 設定，可透過 `SKPaint.IsAntialias` 使用。 |
| *我可以同時結合 `Underline`、`Bold` 與 `Italic` 嗎？* | 完全可以。`FontStyle.Bold | FontStyle.Italic | FontStyle.Underline` 的寫法與其他組合相同。 |
| *啟用抗鋸齒會影響效能嗎？* | 會有輕微影響，特別是在大畫布上。如果每幀要繪製上千個字串，建議對兩種設定進行效能基準測試後再決定。 |
| *如果字體家族本身沒有粗體字重，會怎樣？* | GDI+ 會自行合成粗體樣式，外觀可能比真正的粗體字重更重。若追求最佳視覺品質，請選擇內建粗體字重的字體。 |
| *能否在執行時動態切換這些設定？* | 可以——只要更新 `TextOptions` 物件，並呼叫控制項的 `Invalidate()` 重新繪製即可。 |

---

## 圖片說明

![Screenshot showing how to enable antialiasing in C# code and the resulting smooth text](/images/antialias-demo.png)

*替代文字:* **如何在 C# 中啟用抗鋸齒** – 圖片示範了程式碼與平滑輸出結果。

---

## 重點回顧與後續步驟

我們已說明 **如何在 C# 圖形環境中啟用抗鋸齒**、**如何以程式方式套用粗體與其他樣式**、**如何在低解析度螢幕上使用 hinting**，以及 **如何一次設定多種字體樣式**。完整範例將四個概念結合，提供即用即跑的解決方案。

接下來你可以：

- 探索 **SkiaSharp** 或 **DirectWrite**，取得更豐富的文字渲染管線。
- 嘗試 **動態字體載入**（`PrivateFontCollection`），將自訂字型打包進應用程式。
- 加入 **使用者介面控制**（如勾選框切換抗鋸齒/Hinting），即時觀察效果變化。

歡迎自行調整 `TextOptions` 類別、替換字體，或將此邏輯整合至 WPF、WinUI 等應用程式。原則不變：設定好

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}