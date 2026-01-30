---
category: general
date: 2026-01-01
description: 如何使用 C# 和 CSS 加粗标题并应用斜体样式。学习设置标题字体粗细、应用粗体和斜体，并快速为标题设置样式。
draft: false
keywords:
- how to bold heading
- how to apply italic
- apply bold and italic
- how to apply bold
- set heading font weight
language: zh
og_description: 如何在第一句中加粗标题，然后学习使用斜体，结合粗体和斜体，并通过清晰的示例设置标题字体粗细。
og_title: 如何加粗标题 – CSS 与 C# 完整指南
tags:
- CSS
- C#
- Web Development
title: 使用 CSS 和 C# 加粗标题 – 完整分步指南
url: /zh/net/working-with-html-documents/how-to-bold-heading-with-css-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何加粗标题 – CSS 与 C# 完整指南

有没有想过在网页中**如何加粗标题**而不必翻阅无尽的文档？你并不是唯一的遇到这种情况的人。大多数开发者在需要快速的视觉调整时都会卡住，尤其是当他们在混合使用 HTML、CSS 和一点 C# 来驱动 UI 时。  

在本教程中，我们将通过一个完整、可运行的示例，向你展示如何对 `<h1>` 元素应用加粗、斜体以及组合样式。过程中我们还会涉及**如何应用斜体**、**如何同时应用加粗和斜体**，以及使用 CSS `font-weight` 与低层 `WebFontStyle` API 之间的细微差别。完成后，你将能够自信地**设置标题字体粗细**，无论使用哪种技术栈。

## 先决条件

- .NET 6+（或如果你更喜欢 .NET Framework 4.8）
- Visual Studio 2022 或任何兼容 C# 的 IDE
- HTML 与 CSS 的基础知识
- 一个简单的 WinForms 或 WPF 项目，用于托管 WebView2 控件（示例使用 WinForms）

如果上述内容听起来陌生，请不要慌张——我们会指向你所需的最小代码，你可以直接复制粘贴到新项目中。

---

## 步骤 1：创建最小化的 HTML 页面

首先，我们需要一个 WebView2 控件能够加载的 HTML 文件。将以下内容保存为 `index.html`，放在项目的输出文件夹中（例如 `bin\Debug\net6.0-windows`）。

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

> **为什么这很重要**：保持 CSS 极简可以为我们提供一块干净的画布，从而准确看到 C# 代码的效果。`id="title"` 属性让脚本能够轻松定位该标题。

---

## 步骤 2：使用 WebView2 设置 WinForms 项目

创建一个新的 **Windows Forms App**（`.NET 6`），并添加 **Microsoft.Web.WebView2** NuGet 包。将 `WebView2` 控件拖到窗体上，命名为 `webView`，并将其 `Dock` 属性设为 `Fill`。

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

> **专业提示**：如果导航失败，请再次确认 `index.html` 已复制到输出文件夹（设置 *Copy to Output Directory* → *Copy always*）。

---

## 步骤 3：在 C# 中定位标题元素

页面加载完成后，我们可以获取 `<h1>` 元素。`CoreWebView2` API 提供了 `ExecuteScriptAsync` 方法来运行 JavaScript 并返回结果。不过，为了本教程的目的，我们将使用随 WebView2 一起提供的 **低层 DOM 包装器**（通过 `webView.CoreWebView2` 可访问）。

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

> **为什么要这样做**：直接访问 DOM 可以避免注入大型 JavaScript 代码块。这样更简洁，也展示了使用 WebView2 API **如何应用加粗**。

---

## 步骤 4：应用加粗、斜体和组合样式

现在我们将使用三种不同的方法来为标题设置样式：

1. **CSS `font-weight`** – 最常见的方式，满足 **设置标题字体粗细** 的需求。  
2. **CSS `font-style`** – **如何应用斜体**。  
3. **`WebFontStyle` 标志** – 低层替代方案，可 **同时应用加粗和斜体**。

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

> **说明**：  
> • `fontWeight = '700'` 告诉浏览器以 **加粗** 权重渲染文本。  
> • `fontStyle = 'italic'` 使字形倾斜，满足 **如何应用斜体** 的查询。  
> • 注释行展示了如果你有一个暴露该枚举的包装器，如何在 C# 中设置 `WebFontStyle`。在真实场景中，你会对 `heading` 对象调用 C# 方法，例如 `heading.Font.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;`。

若要真正从 C# 调用低层 API，需要一个 COM 互操作包装器。下面是一个最小示例，假设你已经引用了 `Microsoft.Web.WebView2.Wpf` 命名空间：

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

> **底线**：如果你熟悉 WebView2 的 COM 模型，使用标志方式可以获得细粒度控制。否则，CSS 方式完全足够，并且在所有浏览器上都能工作。

---

## 步骤 5：整合所有内容 – 完整可运行示例

下面是一个完整的 `MainForm.cs` 文件，直接编译运行即可。它加载 HTML，并在导航完成后为标题设置样式。

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

### 预期输出

运行应用后，窗口会显示：

- **“Dynamic Heading”** 以 **加粗**（权重 700）和 **斜体** 渲染。  
- 周围的段落保持不变。  
- 若检查元素（Ctrl + Shift + I），会看到内联样式已被应用。

---

## 常见问题与边缘情况

### 1️⃣ *如果标题已经有类怎么办？*  
你可以通过 `classList.add('my‑bold‑italic')` 添加一个类，并在样式表中定义相应样式，或者继续使用示例中的内联样式。需要快速一次性修改时，内联样式更方便。

### 2️⃣ *所有浏览器都遵循 `font-weight: 700` 吗？*  
是的，700 对应 CSS 规范中的 **Bold** 权重。如果所使用的字体族没有提供加粗字形，浏览器会合成加粗效果，可能会稍显模糊。因此建议使用包含真实加粗字形的字体族（例如 Arial）。

### 3️⃣ *能为从普通到加粗的过渡添加动画吗？*  
完全可以。添加 CSS 过渡：

```css
h1 {
    transition: font-weight 0.3s ease, font-style 0.3s ease;
}
```

然后在 C# 中切换样式，即可看到平滑的动画效果。

### 4️⃣ *可访问性方面怎么办？*  
加粗和斜体属于视觉提示，而非语义信息。为屏幕阅读器考虑，可添加 `aria-label`，或使用正确的标题层级（`<h1>` → `<h2>`）来传达重要性。

---

## 专业技巧与注意事项

- **专业提示**：将 CSS 放在单独的文件中，仅使用 C# 切换类。这样 UI 逻辑更清晰，易于维护。  
- **注意**：避免覆盖用户代理样式。有些浏览器会对 `<strong>` 标签默认使用 `font-weight: bold`，除非有意为之，否则不要将其与手动样式混用。  
- **性能提示**：内联样式更改成本低，但如果要为大量元素设置样式，建议一次性通过脚本调用批量处理，以减少往返次数。

---

## 结论

我们已经覆盖了关于 **如何加粗标题**、**如何应用斜体** 的全部要点，并提供了 **同时加粗和斜体** 的技巧以及从 C# 编程方式 **设置标题字体粗细** 的方法。通过一个小型 HTML 页面、WinForms WebView2 主机以及几次 `ExecuteScriptAsync` 调用，

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}