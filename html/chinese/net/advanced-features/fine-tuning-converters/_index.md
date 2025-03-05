---
title: 使用 Aspose.HTML 在 .NET 中微调转换器
linktitle: .NET 中的微调转换器
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML for .NET 将 HTML 转换为 PDF、XPS 和图像。带有代码示例和常见问题解答的分步教程。
type: docs
weight: 16
url: /zh/net/advanced-features/fine-tuning-converters/
---

## 介绍

Aspose.HTML for .NET 是一个功能强大的库，允许开发人员操作和转换各种格式的 HTML 文档。无论您需要将 HTML 转换为 PDF、XPS 或图像，还是执行其他与 HTML 相关的任务，Aspose.HTML 都提供了一套强大的工具来帮助您完成工作。

在本教程中，我们将探索 Aspose.HTML for .NET 的一些基本功能，并为每个示例提供分步说明。在本教程结束时，您将对如何在 .NET 应用程序中使用 Aspose.HTML for .NET 有一个扎实的理解。

## 先决条件

在深入研究示例之前，请确保您已满足以下先决条件：

-  Aspose.HTML for .NET：您应该已安装 Aspose.HTML for .NET 库。您可以从[下载链接](https://releases.aspose.com/html/net/).

- 临时许可证（可选）：如果您没有有效许可证，可以从[这里](https://purchase.aspose.com/temporary-license/).

现在，让我们探讨一下 Aspose.HTML for .NET 的一些常见用例。

## 导入命名空间

在您的 C# 代码中，首先导入必要的命名空间：

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## 将 HTML 转换为 PDF

### 步骤 1：准备 HTML 代码

```csharp
var code = @"<span>Hello World!!</span>";
```

### 第 2 步：初始化 HTML 文档

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步骤 3：创建 PDF 设备并指定输出文件

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### 步骤 4：将 HTML 渲染为 PDF

```csharp
document.RenderTo(device);
```

此示例将 HTML 代码片段转换为 PDF 文档。您可以根据需要自定义 HTML 代码和输出文件。

## 设置自定义页面大小

### 步骤 1：准备 HTML 代码

```csharp
var code = @"<span>Hello World!!</span>";
```

### 第 2 步：初始化 HTML 文档

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步骤 3：创建 PDF 渲染选项

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### 步骤 4：创建 PDF 设备并指定选项和输出文件

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 步骤 5：将 HTML 渲染为 PDF

```csharp
document.RenderTo(device);
```

此示例演示如何为生成的 PDF 文档设置自定义页面大小。

## 调整分辨率

### 步骤 1：准备 HTML 代码并保存到文件

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### 第 2 步：初始化 HTML 文档

```csharp
using (var document = new HTMLDocument("document.html"))
```

### 步骤 3：创建低分辨率 PDF 渲染选项

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### 步骤 4：创建 PDF 设备并指定低分辨率的选项和输出文件

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### 步骤 5：将 HTML 渲染为低分辨率 PDF

```csharp
document.RenderTo(device);
```

### 步骤 6：创建高分辨率 PDF 渲染选项

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### 步骤 7：创建 PDF 设备并指定高分辨率的选项和输出文件

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### 步骤 8：将 HTML 渲染为高分辨率 PDF

```csharp
document.RenderTo(device);
```

此示例说明了在将 HTML 渲染为 PDF 时如何调整分辨率，同时考虑低分辨率和高分辨率屏幕。

## 指定背景颜色

### 步骤 1：准备 HTML 代码并保存到文件

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### 第 2 步：初始化 HTML 文档

```csharp
using (var document = new HTMLDocument("document.html"))
```

### 步骤 3：使用背景颜色初始化 PDF 渲染选项

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### 步骤 4：创建 PDF 设备并指定选项和输出文件

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 步骤 5：将 HTML 渲染为 PDF

```csharp
document.RenderTo(device);
```

此示例演示如何在将 HTML 转换为 PDF 时指定背景颜色。

## 设置左页面和右页面大小

### 步骤 1：准备 HTML 代码

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### 第 2 步：初始化 HTML 文档

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步骤 3：使用左、右页面大小创建 PDF 渲染选项

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### 步骤 4：创建 PDF 设备并指定选项和输出文件

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 步骤 5：将 HTML 渲染为 PDF

```csharp
document.RenderTo(device);
```

本示例显示如何在将 HTML 转换为 PDF 时为左页和右页设置不同的页面大小。

## 根据内容调整页面大小

### 步骤 1：准备 HTML 代码

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### 第 2 步：初始化 HTML 文档

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步骤 3：创建 PDF 渲染选项

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### 步骤 4：创建 PDF 设备并指定选项和输出文件

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 步骤 5：将 HTML 渲染为 PDF

```csharp
document.RenderTo(device);
```

本例演示了在将 HTML 转换为 PDF 时如何将页面大小调整为最宽的内容。

## 指定 PDF 权限

### 步骤 1：准备 HTML 代码

```csharp
var code = @"<div>Hello World!!</div>";
```

### 第 2 步：初始化 HTML 文档

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步骤 3：创建具有权限的 PDF 渲染选项

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### 步骤 4：创建 PDF 设备并指定选项和输出文件

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### 步骤 5：将 HTML 渲染为 PDF

```csharp
document.RenderTo(device);
```

此示例演示如何在将 HTML 转换为受保护的 PDF 时指定权限和加密。

## 指定图像特定选项

### 步骤 1：准备 HTML 代码

```csharp
var code = @"<div>Hello World!!</div>";
```

### 第 2 步：初始化 HTML 文档

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步骤 3：创建图像渲染选项

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### 步骤 4：创建图像设备并指定选项和输出文件

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### 步骤 5：将 HTML 渲染为图像

```csharp
document.RenderTo(device);
```

此示例演示如何使用特定的渲染选项（如格式、分辨率和平滑模式）将 HTML 转换为图像。

## 指定 XPS 渲染选项

### 步骤 1：准备 HTML 代码

```csharp
var code = @"<span>Hello World!!</span>";
```

### 第 2 步：初始化 HTML 文档

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步骤 3：使用页面大小创建 XPS 渲染选项

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### 步骤 4：创建 XPS 设备并指定选项和输出文件

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### 步骤 5：将 HTML 呈现为 XPS

```csharp
document.RenderTo(device);
```

此示例显示如何使用自定义页面大小和渲染选项将 HTML 转换为 XPS。

## 将多个 HTML 文档合并为 PDF

### 步骤 1：准备多个文档的 HTML 代码

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### 步骤 2：创建要合并的 HTML 文档

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### 步骤 3：初始化 HTML 渲染器

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### 步骤 4：创建合并输出的 PDF 设备

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### 步骤 5：将 HTML 文档合并为 PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

此示例演示如何使用 Aspose.HTML for .NET 将多个 HTML 文档合并为一个 PDF 文件。

## 设置渲染超时

### 步骤 1：使用 JavaScript 准备 HTML 代码

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### 第 2 步：初始化 HTML 文档

```csharp
using (var document = new HTMLDocument(code, "."))
```

### 步骤 3：初始化 HTML 渲染器

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### 步骤 4：创建 PDF 设备并设置渲染超时

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### 步骤 5：使用超时将 HTML 渲染为 PDF

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

此示例演示了如何在将 HTML 转换为 PDF 时设置渲染超时，这在处理动态内容或长时间运行的脚本时很有用。

## 结论

Aspose.HTML for .NET 是一个多功能库，可帮助开发人员高效处理 HTML 文档。在本教程中，我们介绍了各种示例，从基本的 HTML 到 PDF 的转换，到更高级的功能，如自定义页面大小、分辨率和权限。通过遵循这些示例，您可以在 .NET 应用程序中充分利用 Aspose.HTML for .NET 的潜力。

如果您有任何疑问或需要进一步的帮助，请随时访问[Aspose.HTML 论坛](https://forum.aspose.com/)寻求支持和指导。

## 常见问题解答

### Q1.Aspose.HTML for .NET是什么？
   
A1：Aspose.HTML for .NET 是一个 .NET 库，它使开发人员能够以编程方式操作和转换 HTML 文档。它提供了处理 HTML 内容的广泛功能，包括 HTML 到 PDF、XPS 和图像转换，以及高级渲染选项。

### Q2. 我可以在哪里下载 Aspose.HTML for .NET？

 A2: 您可以从以下位置下载 Aspose.HTML for .NET[下载链接](https://releases.aspose.com/html/net/).

### Q3. 我需要许可证才能使用 Aspose.HTML for .NET 吗？

A3：虽然您可以在没有许可证的情况下使用 Aspose.HTML for .NET，但建议您获取生产使用许可证以解锁所有功能并删除任何水印或限制。

### Q4. 如何保护使用 Aspose.HTML for .NET 生成的 PDF 文件？

A4：您可以在使用 Aspose.HTML for .NET 将 HTML 渲染为 PDF 时指定 PDF 权限和加密设置。这允许您控制谁可以访问和修改生成的 PDF 文件。

### Q5. 我可以将 HTML 转换为其他格式（例如 XPS 或图像）吗？

A5：是的，Aspose.HTML for .NET 支持将 HTML 转换为各种格式，包括 PDF、XPS 和图像（例如 JPEG）。您可以自定义转换设置以满足您的特定要求。