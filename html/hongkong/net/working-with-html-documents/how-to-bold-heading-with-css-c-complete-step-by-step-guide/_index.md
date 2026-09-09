---
category: general
date: 2026-01-01
description: 如何使用 C# 與 CSS 加粗標題並套用斜體樣式。學習設定標題字體粗細、套用粗體與斜體，快速為標題設計樣式。
draft: false
keywords:
- how to bold heading
- how to apply italic
- apply bold and italic
- how to apply bold
- set heading font weight
language: zh-hant
og_description: 如何在第一句中將標題加粗，然後學習套用斜體、結合粗斜體，並以清晰範例設定標題字體粗細。
og_title: 如何將標題加粗 – CSS 與 C# 完整指南
tags:
- CSS
- C#
- Web Development
title: 如何使用 CSS 與 C# 加粗標題 – 完整逐步指南
url: /zh-hant/net/working-with-html-documents/how-to-bold-heading-with-css-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何將標題加粗 – CSS 與 C# 完整指南

有沒有想過在網頁上 **如何將標題加粗** 而不必翻閱無盡的文件？你並不是唯一有此疑問的人。大多數開發者在需要快速視覺調整時都會遇到這個問題，尤其是當他們同時混合使用 HTML、CSS 與少量 C# 來驅動 UI 時。

在本教學中，我們將逐步示範一個完整且可執行的範例，向您展示如何對 `<h1>` 元素套用粗體、斜體以及兩者結合的樣式。過程中，我們也會說明 **如何套用斜體**、如何 **同時套用粗體與斜體**，以及使用 CSS `font-weight` 與低階 `WebFontStyle` API 之間的細微差異。完成後，您將能自信地 **設定標題字體粗細**，不論使用哪種技術堆疊。

## 前置條件

- .NET 6+（或若偏好則使用 .NET Framework 4.8）
- Visual Studio 2022 或任何相容 C# 的 IDE
- 基本的 HTML 與 CSS 知識
- 一個簡易的 WinForms 或 WPF 專案，用於承載 WebView2 控制項（範例使用 WinForms）

如果上述任一項目您不熟悉，請不要慌張——我們會提供最小化的程式碼範例，您可以直接複製貼上到新專案中。

---

## 步驟 1：建立最小化的 HTML 頁面

首先，我們需要一個 WebView2 控制項能載入的 HTML 檔案。將以下內容儲存為 `index.html`，放置於專案的輸出資料夾（例如 `bin\Debug\net6.0-windows`）。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Heading Styling Demo</title>
    <style>
        /* Default styling – we’ll override this from C# */
        h1 {
            font-family: 'Arial', sans-serif;
            font-weight: normal;
            font-style: normal;
        }
    </style>
</head>
<body>
    <h1 id="title">Dynamic Heading</h1>
    <p>Open the C# console or UI to see the heading change.</p>
</body>
</html>
```

> **為何重要：** 保持 CSS 最小化能提供乾淨的起點，讓我們清楚看到 C# 程式碼的效果。`id="title"` 屬性讓腳本能輕鬆定位到標題。

---

## 步驟 2：使用 WebView2 設定 WinForms 專案

建立一個新的 **Windows Forms App**（`.NET 6`），並加入 **Microsoft.Web.WebView2** NuGet 套件。將 `WebView2` 控制項拖曳至表單，命名為 `webView`，並將其 `Dock` 屬性設為 `Fill`。

```csharp
using System;
using System.Windows.Forms;
using Microsoft.Web.WebView2.Core;

namespace HeadingStyler
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
            InitializeAsync();
        }

        private async void InitializeAsync()
        {
            // Ensure the WebView2 runtime is available
            await webView.EnsureCoreWebView2Async();

            // Load the local HTML file
            var htmlPath = System.IO.Path.Combine(
                AppDomain.CurrentDomain.BaseDirectory, "index.html");
            webView.CoreWebView2.Navigate($"file:///{htmlPath}");
        }
    }
}
```

> **專業提示：** 若導向失敗，請再次確認 `index.html` 已複製至輸出資料夾（設定 *Copy to Output Directory* → *Copy always*）。

---

## 步驟 3：在 C# 中定位標題元素

頁面載入完成後，我們即可取得 `<h1>` 元素。`CoreWebView2` API 提供 `ExecuteScriptAsync` 方法，可執行 JavaScript 並回傳結果。然而，在本教學中，我們將使用隨 WebView2 提供的 **低階 DOM 包裝器**（可透過 `webView.CoreWebView2` 取得）。

```csharp
private async void WebView_NavigationCompleted(
    object sender, CoreWebView2NavigationCompletedEventArgs e)
{
    // Step 1: Locate the heading element you want to style
    var heading = await webView.CoreWebView2
        .ExecuteScriptAsync("document.querySelector('h1');");

    // The script returns a JS object reference we can manipulate.
    // In practice we’ll call methods on it via ExecuteScriptAsync.
}
```

> **為何這樣做：** 直接存取 DOM 可避免注入大型 JavaScript 程式碼，讓程式更簡潔，並展示 **如何套用粗體**（使用 WebView2 API）。

---

## 步驟 4：套用粗體、斜體與結合樣式

現在，我們將使用三種不同的方法來為標題設定樣式：

1. **CSS `font-weight`** – 最常見的方式，滿足 **設定標題字體粗細** 的需求。
2. **CSS `font-style`** – 說明 **如何套用斜體**。
3. **`WebFontStyle` 標誌** – 一種低階的替代方案，讓我們能同時 **套用粗體與斜體**。

```csharp
private async void StyleHeading()
{
    // 1️⃣ Apply a bold weight (700) – classic CSS method
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        h.style.fontWeight = '700';
    ");

    // 2️⃣ Apply italic style – fulfills “how to apply italic”
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        h.style.fontStyle = 'italic';
    ");

    // 3️⃣ Use the low‑level API to combine bold + italic flags
    // This requires the WebFontStyle enumeration from the WebView2 SDK.
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        // The following line mimics WebFontStyle usage in C#
        // Note: This is illustrative; actual flag usage happens in C#
        // h.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
    ");
}
```

> **說明：**  
> • `fontWeight = '700'` 告訴瀏覽器以 **粗體** 的字重渲染文字。  
> • `fontStyle = 'italic'` 使字形傾斜，滿足 **如何套用斜體** 的需求。  
> • 註解行示範了若有提供列舉的包裝器，如何在 C# 中設定 `WebFontStyle`。在實務上，您會對 `heading` 物件呼叫 C# 方法，例如 `heading.Font.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;`。

若要在 C# 中實際呼叫低階 API，您需要一個 COM interop 包裝器。以下是一個最小範例，假設您已參考 `Microsoft.Web.WebView2.Wpf` 命名空間：

```csharp
using Microsoft.Web.WebView2.WinForms;
using Microsoft.Web.WebView2.Core;
using System.Runtime.InteropServices;

private async void ApplyWebFontStyle()
{
    var script = @"
        (function() {
            var h = document.querySelector('h1');
            // Expose the element to C#
            return h;
        })();";

    var result = await webView.CoreWebView2.ExecuteScriptAsync(script);
    // The result is a JSON representation; you’d need a proper COM object to set flags.
    // For brevity, the example focuses on the CSS path which works everywhere.
}
```

> **重點：** 若您熟悉 WebView2 的 COM 模型，使用旗標方式可提供精細的控制。否則，使用 CSS 方式已足夠，且在所有瀏覽器上皆可運作。

---

## 步驟 5：整合全部 – 完整可執行範例

以下是一個單一的 `MainForm.cs` 檔案，可直接編譯執行。它會載入 HTML，並在導向完成後為標題套用樣式。

```csharp
using System;
using System.Windows.Forms;
using Microsoft.Web.WebView2.Core;

namespace HeadingStyler
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
            webView.NavigationCompleted += WebView_NavigationCompleted;
            InitializeAsync();
        }

        private async void InitializeAsync()
        {
            await webView.EnsureCoreWebView2Async();
            var htmlPath = System.IO.Path.Combine(
                AppDomain.CurrentDomain.BaseDirectory, "index.html");
            webView.CoreWebView2.Navigate($"file:///{htmlPath}");
        }

        private async void WebView_NavigationCompleted(
            object sender, CoreWebView2NavigationCompletedEventArgs e)
        {
            // Apply the three styling techniques
            await webView.CoreWebView2.ExecuteScriptAsync(@"
                var h = document.querySelector('h1');
                h.style.fontWeight = '700';   // bold
                h.style.fontStyle = 'italic'; // italic
                // For low‑level API, you’d use:
                // h.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
            ");
        }
    }
}
```

### 預期輸出

執行應用程式後，視窗會顯示：

- **「Dynamic Heading」** 以 **粗體**（字重 700）與 **斜體** 呈現。
- 周圍的段落保持不變。
- 若檢查元素（Ctrl + Shift + I），即可看到套用的行內樣式。

---

## 常見問題與邊緣情況

### 1️⃣ *如果標題已經有 class 呢？*  
您可以透過 `classList.add('my‑bold‑italic')` 新增 class，並在樣式表中定義樣式，或如示範般繼續使用行內樣式。當需要快速、一次性的變更時，行內樣式較為便利。

### 2️⃣ *所有瀏覽器都支援 `font-weight: 700` 嗎？*  
會的，700 在 CSS 規範中對應 **Bold**（粗體）字重。若字型家族未提供粗體字形，瀏覽器會自行合成，可能會稍顯模糊。因此建議使用具備真實粗體變體的字型家族（例如 Arial）。

### 3️⃣ *能否為從正常到粗體的過渡加入動畫？*  
當然可以。加入 CSS 轉場效果：

```css
h1 {
    transition: font-weight 0.3s ease, font-style 0.3s ease;
}
```

### 4️⃣ *可及性方面怎麼處理？*  
粗體與斜體屬於視覺提示，並非語意標記。對於螢幕閱讀器，建議加入 `aria-label` 或使用正確的標題層級（`<h1>` → `<h2>`）來傳達重要性。

---

## 專業技巧與注意事項

- **專業提示：** 將 CSS 放在獨立檔案，僅使用 C# 來切換 class。這樣 UI 邏輯更清晰，也更易於維護。
- **注意事項：** 可能會覆寫使用者代理樣式。某些瀏覽器會對 `<strong>` 標籤預設 `font-weight: bold`；除非有意，否則避免與手動樣式混用。
- **效能說明：** 行內樣式變更成本低，但若要樣式化數十個元素，建議在單一腳本呼叫中批次處理，以減少往返次數。

---

## 結論

我們已完整說明 **如何將標題加粗**、**如何套用斜體**，以及 **同時套用粗體與斜體** 的技巧，並示範如何從 C# 程式碼中 **設定標題字體粗細**。透過一個小型的 HTML 頁面、WinForms WebView2 主機，以及少量的 `ExecuteScriptAsync` 呼叫，

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}