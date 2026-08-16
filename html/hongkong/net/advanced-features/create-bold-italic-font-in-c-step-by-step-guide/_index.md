---
category: general
date: 2026-08-15
description: 快速在 C# 中建立粗斜體字型。學習如何使用內建的 Font 類別在 C# 中建立帶有粗體與斜體樣式的字型。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create bold italic font
- create font in c#
- C# FontStyle
- text styling C#
- System.Drawing.Font
language: zh-hant
lastmod: 2026-08-15
og_description: 在 C# 中建立粗斜體字型，並提供清晰範例。本教學說明如何使用 FontStyle 標誌在 C# 中建立字型，並解說常見的陷阱。
og_image_alt: Screenshot of text rendered with a bold italic Arial font in a C# console
  window
og_title: 在 C# 中建立粗斜體字型 – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  headline: Create bold italic font in C# – step‑by‑step guide
  type: TechArticle
- description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  name: Create bold italic font in C# – step‑by‑step guide
  steps:
  - name: Save the code to a file named `Program.cs`.
    text: Save the code to a file named `Program.cs`.
  - name: Open a terminal in the file’s directory.
    text: Open a terminal in the file’s directory.
  - name: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
    text: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
  - name: Replace the generated `Program.cs` with the code above.
    text: Replace the generated `Program.cs` with the code above.
  - name: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
    text: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
  - name: Build and run with `dotnet run`.
    text: Build and run with `dotnet run`.
  type: HowTo
tags:
- C#
- fonts
- text styling
title: 在 C# 中建立粗斜體字型 – 步驟指南
url: /zh-hant/net/advanced-features/create-bold-italic-font-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立粗斜體字型 – 步驟指南

如果你需要在 C# 中**建立粗斜體字型**，本指南會精確說明如何操作。你將看到一個完整、可執行的範例，同時示範如何使用標準 .NET `Font` 類別**在 C# 中建立字型**。

在 Windows 桌面應用程式、產生 PDF，或在伺服器上渲染 HTML 時，使用自訂字型是常見的工作。完成本教學後，你將能夠建立同時具備粗體與斜體的字型，了解為何使用位元運算子 `|`，以及處理字型系列缺失等常見例外情況。

## 你將學會

* 如何匯入處理字型所需的命名空間。  
* 結合 `FontStyle.Bold` 與 `FontStyle.Italic` 的語法。  
* 如何驗證字型是否成功建立。  
* 當請求的字型系列未安裝時的備援處理技巧。  

不需要任何外部函式庫——全部使用 .NET Framework / .NET Core 基礎類別庫。

## 前置條件

* .NET 6.0 SDK 或更新版本（此程式碼亦可於 .NET Framework 4.6+ 執行）。  
* 程式碼編輯器或 IDE（Visual Studio、VS Code、Rider 等）。  
* 基本的 C# 語法概念。  

符合上述前置條件後，即可直接依照步驟操作，無需額外設定。

## 步驟 1：加入必要的 using 指示詞

`Font` 類別位於 `System.Drawing` 命名空間，該命名空間屬於 .NET Core/.NET 5+ 的 `System.Drawing.Common` NuGet 套件。請在檔案頂部加入此命名空間：

```csharp
using System;
using System.Drawing;   // Provides Font and FontStyle
```

> **為何此步驟重要** – 若缺少 `using System.Drawing;`，編譯器將找不到 `Font` 或 `FontStyle`，導致出現「找不到類型或命名空間名稱」的錯誤。

## 步驟 2：使用位元 OR 運算子結合粗體與斜體樣式

在 .NET 中，`FontStyle` 是一個標記了 `[Flags]` 屬性的列舉。這表示可以使用 `|`（位元 OR）運算子合併多個值：

```csharp
// Step 2: Create a Font that is both bold and italic
var font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
```

### 說明

* `"Arial"` – 字型系列名稱。若系統未安裝 Arial，建構子會回退至預設字型。  
* `12` – 點數大小。  
* `FontStyle.Bold | FontStyle.Italic` – 結合兩個樣式旗標。`|` 運算子會合併每個旗標的二進位表示，產生同時代表「粗體 + 斜體」的單一值。

> **小技巧**：始終使用列舉名稱（`FontStyle.Bold`）而非魔法數字；這可提升可讀性，並避免列舉值變更時產生錯誤。

## 步驟 3：驗證已建立的字型（可選但建議執行）

列印字型屬性可協助確認樣式組合是否成功，特別是在新機器上除錯時。

```csharp
// Step 3: Output the font details to the console
Console.WriteLine($"Font family: {font.Name}");
Console.WriteLine($"Size (pt): {font.Size}");
Console.WriteLine($"Style: {font.Style}");
```

**預期輸出**

```
Font family: Arial
Size (pt): 12
Style: Bold, Italic
```

若輸出同時列出 `Bold` 與 `Italic`，表示字型已正確建立。

## 步驟 4：繪製樣本字串（視覺確認）

在 console 應用程式中無法直接看到字形樣式，但可產生圖片以證明結果。以下程式碼會使用粗斜體字型繪製「Hello, World!」並存為 *sample.png*：

```csharp
// Step 4: Draw text to an image file for visual confirmation
using (var bitmap = new Bitmap(300, 100))
using (var graphics = Graphics.FromImage(bitmap))
{
    graphics.Clear(Color.White);
    var brush = Brushes.Black;
    graphics.DrawString("Hello, World!", font, brush, new PointF(10, 30));
    bitmap.Save("sample.png");
    Console.WriteLine("Image saved as sample.png");
}
```

程式執行完畢後，開啟 *sample.png* 即可看到以粗斜體樣式呈現的文字。

![使用粗斜體字型渲染的範例文字](sample.png)

*圖片說明文字：在 C# 主控台視窗中以粗斜體 Arial 字型渲染的文字截圖* – 此說明文字符合 SEO 對圖片 alt 文字的要求。

## 步驟 5：當字型系列不可用時的優雅備援

若請求的系列（例如「Arial」）未安裝，`Font` 建構子會拋出 `ArgumentException`。將建立程式碼包在 `try/catch` 區塊中，並回退至已知安全的字型（如「Segoe UI」）。

```csharp
Font font;
try
{
    font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
}
catch (ArgumentException)
{
    Console.WriteLine("Arial not found – falling back to Segoe UI.");
    font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
}
```

**為何需要這樣處理？** 在容器化或無頭環境中，預設字型集合可能與一般桌面不同。提供備援可避免執行時崩潰，確保樣式一致。

## 完整、可執行的範例

將上述所有步驟整合，即可得到以下完整程式碼，直接複製、貼上並執行：

```csharp
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create the font (bold + italic)
        Font font;
        try
        {
            font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
        }
        catch (ArgumentException)
        {
            Console.WriteLine("Arial not found – using Segoe UI as fallback.");
            font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
        }

        // Display font information
        Console.WriteLine($"Font family: {font.Name}");
        Console.WriteLine($"Size (pt): {font.Size}");
        Console.WriteLine($"Style: {font.Style}");

        // Render a sample image
        using (var bitmap = new Bitmap(300, 100))
        using (var graphics = Graphics.FromImage(bitmap))
        {
            graphics.Clear(Color.White);
            graphics.DrawString("Hello, World!", font, Brushes.Black, new PointF(10, 30));
            bitmap.Save("sample.png");
        }

        Console.WriteLine("Sample image saved as sample.png");
    }
}
```

### 如何執行

1. 將程式碼儲存為 `Program.cs`。  
2. 在該檔案所在目錄開啟終端機。  
3. 執行 `dotnet new console -n FontDemo`（若需要建立專案骨架）。  
4. 用上述程式碼取代產生的 `Program.cs`。  
5. 執行 `dotnet add package System.Drawing.Common`（.NET Core/5+ 必須）。  
6. 使用 `dotnet run` 進行建置與執行。  

你將在主控台看到字型屬性的確認訊息，且 `sample.png` 會出現在專案資料夾中。

## 常見陷阱與避免方式

| 陷阱 | 為何會發生 | 解決方法 |
|------|------------|----------|
| **缺少 `System.Drawing.Common` 套件** | .NET Core 預設不包含 `System.Drawing`。 | 執行 `dotnet add package System.Drawing.Common`。 |
| **字型系列未安裝** | 無頭 Docker 映像常缺少 Windows 字型。 | 使用備援字型或在容器中安裝所需字型。 |
| **錯誤使用 `|`** | 使用 `+` 取代 `|` 會產生無效的組合。 | 必須以位元 OR 運算子 (`|`) 結合 `FontStyle` 值。 |
| **未釋放 `Font` 物件** | 未呼叫 `Dispose` 會導致 GDI 資源泄漏。 | 將 `Font` 包在 `using` 區塊，或在使用完畢後呼叫 `font.Dispose()`。 |

## 結論

你現在已掌握如何在 C# 中**建立粗斜體字型**，以及如何安全且有效率地**在 C# 中建立字型**。本教學涵蓋了匯入正確命名空間、結合 `FontStyle` 旗標、驗證結果、繪製視覺樣本，以及處理字型系列缺失的情況。

接下來，你可以探索：

* **建立底線或刪除線字型** – 加入 `FontStyle.Underline` 或 `FontStyle.Strikeout`。  
* **使用自訂 TrueType 字型** – 以 `PrivateFontCollection` 載入 `.ttf` 檔案。  
* **在 WinForms、WPF 或 PDF 產生中套用字型** – 同一個 `Font` 物件可傳遞給 UI 控制項或第三方函式庫。  

歡迎自行嘗試不同的字型系列、大小與樣式組合。若遇到問題，請再次檢視「常見陷阱」表格或參考官方 [.NET 文件：System.Drawing.Font](https://learn.microsoft.com/dotnet/api/system.drawing.font)。祝程式開發愉快！

## 下一步該學什麼？

以下教學與本指南的技術緊密相關，能在此基礎上延伸更多 API 功能，並提供完整的程式碼範例與逐步說明，協助你在專案中探索不同的實作方式。

- [在 C# 中以程式方式合併字型 – 步驟指南](/html/indonesian/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/)
- [建立具樣式文字的 HTML 文件並匯出為 PDF – 完整指南](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [將 docx 轉換為 png – 建立 zip 壓縮檔的 C# 教學](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}