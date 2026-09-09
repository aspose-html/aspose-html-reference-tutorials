---
category: general
date: 2025-12-29
description: 在 C# 中创建 HTML 文档，学习如何设置字体族、设置字体大小，然后使用 Aspose.HTML 将 HTML 保存为 PDF 或将
  HTML 转换为 PDF。
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: zh
og_description: 在 C# 中创建 HTML 文档，立即了解如何设置字体族、设置字体大小，然后使用 Aspose.HTML 将 HTML 保存为 PDF
  或将 HTML 转换为 PDF。
og_title: 创建 HTML 文档 – 样式化文本与 PDF 导出
tags:
- aspnet
- csharp
- pdf-generation
title: 创建带样式文本的HTML文档并导出为PDF – 完整指南
url: /zh/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建带样式文本的 HTML 文档并导出为 PDF

是否曾经需要在代码中即时 **创建 HTML 文档** 并将其转换为 PDF，而无需离开 C# 代码？也许你正在构建报表引擎、发票生成器，或只是为用户提供快速预览。好消息是，你可以使用 Aspose.HTML 只需几行代码就实现，而且可以完全控制字体族、字体大小，甚至粗体‑斜体样式。

在本教程中，我们将完整演示整个过程——从创建内存中的 HTML 文档到将其保存为 PDF 文件。结束时，你将准确掌握如何 **set font family**、**set font size**，以及 **save HTML as PDF**（即 **convert HTML to PDF**），并提供一段简洁、可直接用于生产环境的代码示例。

## 你需要的环境

- .NET 6+（该 API 同时支持 .NET Core 和 .NET Framework）  
- Aspose.HTML for .NET NuGet 包 (`Aspose.Html`) – 通过 `dotnet add package Aspose.Html` 安装  
- 磁盘上一个可写入的文件夹，用于保存生成的 PDF  

![创建 HTML 文档示例](/images/create-html-document.png){alt="创建 HTML 文档示例"}

## 步骤 1：创建 HTML 文档

首先，我们需要一个空的 HTML 文档对象。可以把它想象成一块全新的画布，稍后将在其上绘制带样式的段落。

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**为什么这很重要：** `HTMLDocument` 为你提供了类似 DOM 的结构，能够以编程方式进行操作。直到最后一步才需要处理原始字符串或文件 I/O。

## 步骤 2：添加段落并设置字体族和字体大小

现在我们将创建一个 `<p>` 元素，插入一些文本，并显式定义字体族和大小。这正是 **set font family** 和 **set font size** 关键字发挥作用的地方。

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

**小技巧：** 如果需要 Web 安全的回退字体，可以提供逗号分隔的列表，例如 `"Arial, Helvetica, sans-serif"`；浏览器（或 Aspose）会选取第一个可用的字体。

## 步骤 3：使用 WebFontStyle 标志应用粗体和斜体样式

Aspose.HTML 提供了一个便利的枚举 `WebFontStyle`，允许你通过按位或（OR）组合样式。让我们把文本同时设为粗体 **且** 斜体。

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**内部原理是什么？** `FontStyle` 属性会转换为 CSS 的 `font-weight` 和 `font-style` 声明。通过对标志进行 OR 运算，我们避免了编写两行独立的 CSS。

## 步骤 4：将 HTML 转换为 PDF（保存 HTML 为 PDF）

最后一步是实际的转换。只需一次调用 `Save`，Aspose.HTML 即会渲染 DOM 并将 PDF 文件写入磁盘。这同时满足 **save html as pdf** 与 **convert html to pdf** 的需求。

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

**预期结果：** 打开 `styled.pdf`，你会看到一个段落显示 “Bold & Italic text”，使用 18‑px Arial，呈现为粗体斜体。PDF 尺寸为标准 A4 页面，文本可选中——这得益于矢量渲染。

## 完整工作示例

将所有步骤整合在一起，下面是完整的、可直接运行的程序：

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

### 运行代码

1. 安装 Aspose.HTML NuGet 包：  
   ```bash
   dotnet add package Aspose.Html
   ```
2. 将 `C:\Temp\styled.pdf` 替换为你拥有写入权限的文件夹路径。  
3. 构建并运行：`dotnet run`。  

运行后，你应该会在控制台看到确认文件位置的消息，生成的 PDF 将包含带样式的段落。

## 常见问题与边缘情况

- **如果我需要自定义 Web 字体怎么办？**  
  在创建段落之前，使用 `HTMLFontFaceRule` 加载字体，或引用远程的 `@font-face` CSS 文件。

- **可以在转换前添加图片吗？**  
  完全可以。使用 `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` 并将 `img.Source` 设置为本地路径或 data URI。

- **多页 PDF 如何处理？**  
  添加更多元素（表格、div 等），当内容超过页面高度时，Aspose.HTML 会自动分页。

- **有没有办法控制 PDF 元数据？**  
  传入 `PdfSaveOptions` 实例，并设置 `Author`、`Title` 或 `PdfAConformanceLevel` 等属性。

## 小结

我们已经介绍了如何在 C# 中 **create HTML document**，**set font family**，**set font size**，以及应用粗体‑斜体样式，最终 **save HTML as PDF**——即使用 Aspose.HTML **convert HTML to PDF**。该代码片段足够简短，可直接嵌入任何 .NET 项目，又足够完整，可作为更复杂报表场景的坚实基础。

## 后续步骤

- 试验 CSS 类以实现可复用的样式。  
- 组合多个段落、表格和图片，构建更丰富的 PDF。  
- 如需归档级文档，可探索 PDF/A 合规性。  

随意调整字体、大小或颜色——程序化生成的内容没有限制。祝编码愉快，愿你的 PDF 总是如你所想精准呈现！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}