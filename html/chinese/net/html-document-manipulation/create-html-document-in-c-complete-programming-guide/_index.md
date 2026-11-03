---
category: general
date: 2026-07-05
description: 快速在 C# 中创建 HTML 文档：加载 HTML 字符串，按 ID 获取元素，设置字体样式，并通过逐步示例修改段落样式。
draft: false
keywords:
- create html document
- load html string
- get element by id
- set font style
- modify paragraph style
language: zh
og_description: 在 C# 中创建 HTML 文档，并学习如何加载 HTML 字符串、通过 ID 获取元素、设置字体样式以及修改段落样式，一站式教程。
og_title: 使用 C# 创建 HTML 文档 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: 'Create HTML document in C# quickly: load HTML string, get element
    by ID, set font style, and modify paragraph style with a step‑by‑step example.'
  headline: Create HTML Document in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- HTML parsing
- DOM manipulation
- Styling
title: 在 C# 中创建 HTML 文档 – 完整编程指南
url: /zh/net/html-document-manipulation/create-html-document-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建 HTML 文档 – 完整编程指南

是否曾经需要 **创建 html 文档** 于 C#，却不知从何入手？你并不孤单；许多开发者在第一次尝试在服务器端操作 HTML 时都会遇到这个难题。在本指南中，我们将演示如何 **加载 html 字符串**、使用 **get element by id** 定位节点，然后 **设置字体样式** 或 **修改段落样式**，而无需引入笨重的浏览器引擎。

教程结束时，你将拥有一个可直接运行的代码片段，能够构建 HTML 文档、注入内容并为段落添加样式——全部使用纯 C# 代码。无需外部 UI、无需 JavaScript，只有干净、可测试的逻辑。

## 你将学到

- 如何使用 `HtmlDocument` 类 **创建 html 文档** 对象。  
- 将 **加载 html 字符串** 到该文档的最简方法。  
- 使用 **get element by id** 安全获取单个节点。  
- 为段落应用 **set font style** 标志（粗体、斜体、下划线）。  
- 将示例扩展为 **修改段落样式**，包括颜色、外边距等。  

**先决条件** – 你需要安装 .NET 6+，对 C# 有基本了解，并在项目中加入 `HtmlAgilityPack` NuGet 包（服务器端 HTML 解析的事实标准库）。如果你从未添加过 NuGet 包，只需在项目文件夹中运行 `dotnet add package HtmlAgilityPack`。

---

## 创建 HTML 文档并加载 HTML 字符串

第一步是 **创建 html 文档** 并将原始标记喂入其中。可以把 `HtmlDocument` 看作一块空白画布；`LoadHtml` 方法会把你的字符串绘制上去。

```csharp
using System;
using HtmlAgilityPack;   // NuGet: HtmlAgilityPack

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a new HtmlDocument (create html document)
        var doc = new HtmlDocument();

        // Step 2: Load a simple HTML string (load html string)
        string rawHtml = @"<html><body><p id='txt'>Sample text</p></body></html>";
        doc.LoadHtml(rawHtml);
        
        // The rest of the tutorial continues below...
    }
}
```

为什么使用 `LoadHtml` 而不是 `doc.Open`？`Open` 方法是旧版分支中遗留的包装，仅存在于老版本中；`LoadHtml` 是现代、线程安全的替代方案，且在 .NET Core 和 .NET Framework 上均可使用。  

> **专业提示：** 如果计划加载大型文件，考虑使用 `doc.Load(path)`，它会从磁盘流式读取，而不是将整个字符串一次性加载到内存。

---

## 根据 ID 获取元素

文档已驻留在内存后，我们需要 **get element by id**。这与 JavaScript 中的 `document.getElementById` 调用类似，只是发生在服务器端。

```csharp
// Step 3: Retrieve the paragraph element by its ID (get element by id)
var paragraph = doc.GetElementbyId("txt");

// Defensive check – always verify the node exists before touching it.
if (paragraph == null)
{
    Console.WriteLine("Element with ID 'txt' not found.");
    return;
}
```

`GetElementbyId` 方法只遍历一次 DOM 树，即使是大文档也相当高效。如果需要定位多个元素，可使用 `SelectNodes("//p[@class='myClass']")` 作为 XPath 替代方案。

---

## 为段落设置字体样式

拿到节点后，我们可以 **set font style**。`HtmlNode` 类并未提供专门的 `FontStyle` 属性，但我们可以直接操作 `style` 属性。为保持代码整洁，本文将模拟一个类似 `WebFontStyle` 的枚举。

```csharp
// Step 4: Define a simple flag enum for font styles
[Flags]
enum WebFontStyle
{
    None    = 0,
    Bold    = 1 << 0,
    Italic  = 1 << 1,
    Underline = 1 << 2
}

// Helper to translate flags into CSS
static string FontStyleToCss(WebFontStyle style)
{
    var parts = new System.Collections.Generic.List<string>();
    if (style.HasFlag(WebFontStyle.Bold)) parts.Add("font-weight: bold");
    if (style.HasFlag(WebFontStyle.Italic)) parts.Add("font-style: italic");
    if (style.HasFlag(WebFontStyle.Underline)) parts.Add("text-decoration: underline");
    return string.Join("; ", parts);
}

// Apply combined bold & italic style (set font style)
WebFontStyle combined = WebFontStyle.Bold | WebFontStyle.Italic;
string css = FontStyleToCss(combined);
paragraph.SetAttributeValue("style", css);
```

刚才发生了什么？我们构建了一个小枚举，将选中的标志转换为 CSS 字符串，并把该字符串写入 `<p>` 元素的 `style` 属性。结果是，当 HTML 最终渲染时，段落会显示 **粗体和斜体**。

**为什么使用标志（flags）？** 标志允许你在不嵌套多个 `if` 语句的情况下组合样式，并且与 CSS 的多声明用分号分隔的写法天然匹配。

---

## 修改段落样式 – 高级微调

样式并不止于粗体或斜体。让我们 **修改段落样式**，进一步加入颜色和行高。这演示了如何在不覆盖已有值的前提下继续扩展 CSS 字符串。

```csharp
// Retrieve any existing style attribute (might be empty)
string existingStyle = paragraph.GetAttributeValue("style", "");

// Append extra rules – note the trailing semicolon for safety
string extraCss = "color: #2A7AE2; line-height: 1.6";
string combinedStyle = string.IsNullOrWhiteSpace(existingStyle)
    ? extraCss
    : $"{existingStyle}; {extraCss}";

paragraph.SetAttributeValue("style", combinedStyle);
```

现在段落将以柔和的蓝色显示，并拥有舒适的行间距。  

> **注意：** 避免出现重复的 CSS 属性。如果后续再次设置 `font-weight`，大多数浏览器会采用最后出现的值，但这会增加调试难度。更清晰的做法是构建一个 `Dictionary<string,string>` 来存放 CSS 声明，最后统一序列化输出。

---

## 完整可运行示例

将所有内容组合起来，下面是一个 **完整、可运行的程序**，它创建 HTML 文档、加载字符串、按 ID 获取节点并为其设置样式。

```csharp
using System;
using HtmlAgilityPack;

[Flags]
enum WebFontStyle
{
    None      = 0,
    Bold      = 1 << 0,
    Italic    = 1 << 1,
    Underline = 1 << 2
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create HTML document
        var doc = new HtmlDocument();

        // 2️⃣ Load HTML string
        string rawHtml = @"<html><body><p id='txt'>Sample text</p></body></html>";
        doc.LoadHtml(rawHtml);

        // 3️⃣ Get element by ID
        var paragraph = doc.GetElementbyId("txt");
        if (paragraph == null)
        {
            Console.WriteLine("Paragraph not found.");
            return;
        }

        // 4️⃣ Set font style (bold + italic)
        WebFontStyle styleFlags = WebFontStyle.Bold | WebFontStyle.Italic;
        string css = FontStyleToCss(styleFlags);
        paragraph.SetAttributeValue("style", css);

        // 5️⃣ Modify paragraph style – add color & line‑height
        string extraCss = "color: #2A7AE2; line-height: 1.6";
        string combinedStyle = $"{css}; {extraCss}";
        paragraph.SetAttributeValue("style", combinedStyle);

        // 6️⃣ Output the final HTML
        string finalHtml = doc.DocumentNode.OuterHtml;
        Console.WriteLine("=== Final HTML ===");
        Console.WriteLine(finalHtml);
    }

    static string FontStyleToCss(WebFontStyle style)
    {
        var parts = new System.Collections.Generic.List<string>();
        if (style.HasFlag(WebFontStyle.Bold)) parts.Add("font-weight: bold");
        if (style.HasFlag(WebFontStyle.Italic)) parts.Add("font-style: italic");
        if (style.HasFlag(WebFontStyle.Underline)) parts.Add("text-decoration: underline");
        return string.Join("; ", parts);
    }
}
```

### 预期输出

运行程序后会打印：

```
=== Final HTML ===
<html><body><p id="txt" style="font-weight: bold; font-style: italic; color: #2A7AE2; line-height: 1.6">Sample text</p></body></html>
```

如果将生成的 HTML 粘贴到任意浏览器中，段落会显示为 “Sample text”，呈现粗斜体蓝色并拥有舒适的行高。

---

## 常见问题与边缘情况

**如果 HTML 字符串格式错误怎么办？**  
`HtmlAgilityPack` 具有容错能力，会尝试修复缺失的闭合标签。但在处理用户生成内容时，仍需始终进行输入验证，以防止 XSS 攻击。

**可以加载整个文件而不是字符串吗？**  
可以——使用 `doc.Load("path/to/file.html")`。相同的 DOM 方法（`GetElementbyId`、`SetAttributeValue`）依旧适用。

**如何以后移除某个样式？**  
获取当前的 `style` 属性，按 `;` 分割，过滤掉不需要的规则，然后把清理后的字符串重新设置回去。

**有没有办法一次添加多个类名？**  
当然——`paragraph.AddClass("highlight")`（扩展方法）或手动操作 `class` 属性：  
`paragraph.SetAttributeValue("class", "highlight anotherClass");`

---

## 结论

我们已经 **在 C# 中创建 html 文档**、**加载 html 字符串**、使用 **get element by id**，并演示了如何 **set font style** 与 **modify paragraph style**，代码简洁且符合惯用写法。该方法适用于任何规模的 HTML，从小片段到完整模板，且完全在服务器端运行——非常适合邮件生成、PDF 渲染或任何自动化报表流水线。

接下来可以尝试将内联 CSS 替换为

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在已有技术之上进一步提升。每篇资源都提供完整可运行的代码示例，并配有逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方式。

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Create HTML Document with Styled Text and Export to PDF – Full Guide](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}