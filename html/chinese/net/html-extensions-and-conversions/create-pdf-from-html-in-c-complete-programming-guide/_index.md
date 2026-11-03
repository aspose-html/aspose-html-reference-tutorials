---
category: general
date: 2026-06-22
description: 在 C# 中快速将 HTML 创建为 PDF——学习如何将 HTML 转换为 PDF、将 HTML 保存为 PDF，以及使用简易库导出 HTML
  为 PDF。
draft: false
keywords:
- create pdf from html
- convert html to pdf
- save html as pdf
- export html as pdf
- how to convert html to pdf
language: zh
og_description: 使用轻量级转换器在 C# 中将 HTML 创建为 PDF。本指南展示如何将 HTML 转换为 PDF、将 HTML 保存为 PDF，以及使用简洁代码导出
  HTML 为 PDF。
og_title: 使用 C# 从 HTML 创建 PDF – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create PDF from HTML in C# quickly—learn how to convert HTML to PDF,
    save HTML as PDF, and export HTML as PDF with a simple library.
  headline: Create PDF from HTML in C# – Complete Programming Guide
  type: TechArticle
- description: Create PDF from HTML in C# quickly—learn how to convert HTML to PDF,
    save HTML as PDF, and export HTML as PDF with a simple library.
  name: Create PDF from HTML in C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 SDK or later (the code works on .NET Core and .NET Framework
      alike). - Basic familiarity with C# and the command line. - An HTML file you
      want to turn into a PDF (we’ll call it `input.html`).'
  - name: How It Works
    text: 1. **Reading the HTML** – We pull the raw HTML string from `input.html`.
      This step is crucial for the **save html as pdf** part because the converter
      works with a string, not a file handle. 2. **Creating a `PdfDocument`** – Think
      of this as the blank canvas where each page will be painted. 3. **`Pdf
  - name: Handling CSS and Images
    text: '```csharp // Load HTML with a base URL so relative paths resolve correctly.
      string baseUrl = Path.GetDirectoryName(htmlPath) ?? ""; PdfGenerator.AddPdfPages(pdf,
      htmlContent, PageSize.A4, new PdfGenerateConfig { BaseUrl = new Uri($"file:///{baseUrl}/")
      }); ```'
  - name: Large Documents & Pagination
    text: 'If your HTML creates many pages, the library automatically adds them. However,
      you might want to control page breaks manually:'
  type: HowTo
tags:
- C#
- HTML
- PDF
- Conversion
title: 在 C# 中从 HTML 创建 PDF – 完整编程指南
url: /zh/net/html-extensions-and-conversions/create-pdf-from-html-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 从 HTML 创建 PDF – 完整编程指南

是否曾想过 **从 HTML 创建 PDF** 而不必与一堆命令行工具搏斗？你并不孤单。大多数开发者在需要将动态网页转换为可打印报告、发票或可下载手册时，都会遇到这个难题。

在本教程中，我们将一步步演示一个简洁的端到端解决方案，让你只需几行 C# 代码即可 **将 HTML 转换为 PDF**、**将 HTML 保存为 PDF**，甚至 **导出 HTML 为 PDF**。完成后，你将拥有一个可在任何 .NET 项目中直接使用的可复用方法——无需神秘依赖，也没有隐藏的魔法。

## 你将学到的内容

- 如何为 HTML‑to‑PDF 转换搭建一个最小的 C# 控制台应用。  
- 使用流行的 *HtmlRenderer.PdfSharp* 库（或任何类似库）**从 HTML 创建 PDF** 所需的完整代码。  
- 为什么有时更倾向于同步调用而非异步调用，以及各自适用的场景。  
- 常见陷阱——缺失的 CSS、大图片、相对路径——以及规避方法。  
- 一个快速测试，帮助你验证输出是否符合预期。

### 前置条件

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）。  
- 对 C# 和命令行有基本了解。  
- 一个你想转换为 PDF 的 HTML 文件（我们将其称为 `input.html`）。  

如果你满足以上条件，下面开始吧。

## 从 HTML 创建 PDF – 项目搭建

首先，创建一个全新的控制台项目。打开终端并输入：

```bash
dotnet new console -n HtmlToPdfDemo
cd HtmlToPdfDemo
```

接着，添加转换库。此示例我们使用 **HtmlRenderer.PdfSharp**，它封装了 PdfSharp 并能够开箱即用地处理大多数 HTML/CSS：

```bash
dotnet add package HtmlRenderer.PdfSharp --version 1.7.2
```

> **专业提示：** 如果你面向 .NET Framework，同样可以使用此 NuGet 包，只需确保项目文件的目标框架版本匹配即可。

现在你已经拥有了 **将 html 转换为 pdf** 所需的一切。

## 将 HTML 转换为 PDF – 使用 HtmlToPdfConverter

创建一个名为 `PdfConverter.cs` 的新类文件（或者为了快速演示，直接在 `Program.cs` 中编写所有代码）。下面是一个 **完整、可运行** 的示例，它会加载 HTML 文档、进行转换并将结果写入磁盘。

```csharp
using System;
using System.IO;
using TheArtOfDev.HtmlRenderer.PdfSharp;   // Namespace from HtmlRenderer.PdfSharp
using PdfSharp.Pdf;

namespace HtmlToPdfDemo
{
    /// <summary>
    /// Simple helper that encapsulates the HTML → PDF conversion logic.
    /// </summary>
    public static class PdfConverter
    {
        /// <summary>
        /// Converts the specified HTML file to a PDF and saves it.
        /// </summary>
        /// <param name="htmlPath">Full path to the source HTML file.</param>
        /// <param name="pdfPath">Full path where the PDF should be written.</param>
        public static void ConvertHtmlToPdf(string htmlPath, string pdfPath)
        {
            // Validate inputs early – helps you avoid vague exceptions later.
            if (!File.Exists(htmlPath))
                throw new FileNotFoundException($"HTML file not found: {htmlPath}");

            // Read the HTML content. Using UTF‑8 ensures you keep any special characters.
            string htmlContent = File.ReadAllText(htmlPath);

            // Create a new PDF document. This is the container that will hold our pages.
            using PdfDocument pdf = new PdfDocument();

            // The HtmlRender library does the heavy lifting. It parses the HTML and draws it onto a PDF page.
            PdfGenerator.AddPdfPages(pdf, htmlContent, PageSize.A4);

            // Finally, write the PDF to the destination path.
            pdf.Save(pdfPath);
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment.
            string inputHtml = Path.Combine(Environment.CurrentDirectory, "input.html");
            string outputPdf = Path.Combine(Environment.CurrentDirectory, "output.pdf");

            try
            {
                PdfConverter.ConvertHtmlToPdf(inputHtml, outputPdf);
                Console.WriteLine($"✅ Success! PDF created at: {outputPdf}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to create PDF: {ex.Message}");
            }
        }
    }
}
```

### 工作原理

1. **读取 HTML** – 我们从 `input.html` 中获取原始 HTML 字符串。这一步对 **将 html 保存为 pdf** 非常关键，因为转换器接受的是字符串，而不是文件句柄。  
2. **创建 `PdfDocument`** – 将其视作绘制每页内容的空白画布。  
3. **`PdfGenerator.AddPdfPages`** – 库的核心；它解析 HTML、应用基础 CSS，并将其渲染到一个或多个 A4 页面上。  
4. **保存文件** – `pdf.Save` 调用将二进制 PDF 写入磁盘，实际完成 **导出 html 为 pdf**。

运行程序：

```bash
dotnet run
```

如果一切配置正确，你会看到绿色对勾，并在可执行文件旁边找到 `output.pdf`。

## 将 HTML 保存为 PDF – 文件处理细节

你可能会想，*“为什么不直接把 PDF 流式输出到响应？”* 这是个好问题。在许多 Web‑API 场景下确实会直接流式返回字节，但在桌面应用或批处理任务中，往往需要生成实际的文件。上面的代码已经通过调用 `pdf.Save(pdfPath)` 实现了 **将 html 保存为 pdf**。

需要注意的几点：

- **覆盖保护** – `pdf.Save` 会悄悄覆盖已有文件。如果需要安全起见，可先检查 `File.Exists(pdfPath)`，然后决定重命名或提示用户。  
- **文件夹权限** – 确保进程对目标文件夹拥有写入权限，尤其是在 Linux 容器中默认用户可能受限。  
- **编码** – HTML 文件应为 UTF‑8 编码，否则最终 PDF 可能出现乱码。

## 导出 HTML 为 PDF – 高级选项

上述简单示例适用于大多数静态页面，但实际 HTML 往往包含外部 CSS、图片，甚至 JavaScript。下面介绍如何扩展转换器以处理这些情况。

### 处理 CSS 与图片

```csharp
// Load HTML with a base URL so relative paths resolve correctly.
string baseUrl = Path.GetDirectoryName(htmlPath) ?? "";
PdfGenerator.AddPdfPages(pdf, htmlContent, PageSize.A4, 
    new PdfGenerateConfig
    {
        BaseUrl = new Uri($"file:///{baseUrl}/")
    });
```

- **BaseUrl** 告诉渲染器去哪里寻找 `src="images/logo.png"` 或 `href="styles/main.css"`。  
- 对于远程资源，你可以将 `BaseUrl` 设置为 HTTP URL，但需注意网络延迟。

### 大文档与分页

如果你的 HTML 生成了多页，库会自动添加页面。不过，你可能希望手动控制分页：

```html
<div style="page-break-after: always;"></div>
```

在 C# 中，你也可以将 HTML 拆分为多个段落，分别调用 `AddPdfPages`，从而更细致地控制页眉和页脚。

## 将 HTML 转换为 PDF – 常见陷阱

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| 缺失字体 | PdfSharp 默认只支持标准字体。 | 通过 `PdfFontResolver` 嵌入 TrueType 字体。 |
| 图片不显示 | 相对路径错误或不支持的格式。 | 使用 `BaseUrl` 或将图片嵌入为 Base64。 |
| CSS 未生效 | 库只支持 CSS 的子集。 | 保持样式简洁，或使用无头浏览器（如 Puppeteer）预处理 HTML。 |
| 大页面导致内存溢出 | 所有页面在 `Save` 前都保存在内存中。 | 分块转换，或使用支持流式输出的 API（若有）。 |

提前处理这些问题，可为后续调试省下大量时间。

## 预期输出

运行示例后，使用任意 PDF 阅读器打开 `output.pdf`。你应该能看到 `input.html` 的忠实渲染——标题、段落以及图片（若有）都整齐地排布在 A4 页面上。文件大小通常在 50 KB（纯文本）到几百 KB（图片密集）之间。

![create pdf from html example output](https://example.com/assets/create-pdf-from-html.png "create pdf from html example output")

*上图展示了一个简单的 HTML 页面被转换为整洁的 PDF。*

## 小结与后续

## 接下来该学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并探索在项目中实现的替代方案。每篇资源都提供完整可运行的代码示例以及逐步解释。

- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create HTML Document with Styled Text and Export to PDF – Full Guide](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}