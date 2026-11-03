---
category: general
date: 2026-04-06
description: 学习如何在 C# 中启用抗锯齿、设置图像宽度和高度，并将文档保存为 PNG——快速导出文档为图像的指南。
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: zh
og_description: 如何在将文档导出为图像时启用抗锯齿。本指南展示了如何设置图像宽度、设置图像高度以及将文档保存为 PNG。
og_title: 如何启用抗锯齿 – 将文档导出为图像
tags:
- C#
- ImageRendering
- Antialiasing
title: 如何启用抗锯齿 – 使用 C# 将文档导出为图像
url: /zh/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中启用抗锯齿 – 将文档导出为图像

有没有想过在将文档转换为图片时**如何启用抗锯齿**？也许你尝试了快速的 `Save` 调用，但结果出现锯齿，尤其是在对角线条上。好消息是，你不需要图形专家——只需几行 C# 代码和正确的选项。

在本教程中，我们将逐步演示 **设置图像宽度**、**设置图像高度**，以及最后 **将文档保存为 PNG**，从而实现 **将文档导出为图像** 并拥有平滑的边缘。完成后，你将拥有一个可直接运行的代码片段，生成一张 800 × 600、已开启抗锯齿的清晰 PNG。

## 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）  
- 引用支持 `ImageRenderingOptions` 的渲染库（例如 Aspose.Words、Syncfusion，或任何提供类似属性的 API）  
- 对 C# 语法有基本了解  

无需繁重的配置——只需添加 NuGet 包即可开始。

## 第 1 步：安装渲染库

首先，将包引入项目。如果使用 Aspose.Words，运行：

```bash
dotnet add package Aspose.Words
```

> **专业提示：** 保持库版本为最新；截至 2026 年 4 月的最新版本已加入针对抗锯齿的性能优化。

## 第 2 步：创建 Document 对象

加载或创建要渲染的文档。下面是一个最小示例，构建一个包含简单段落的单页文档：

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

`Document` 类是入口点，所有渲染内容都来源于它。在实际项目中，你可能会加载已有的 .docx 文件：

```csharp
// Document doc = new Document("input.docx");
```

## 第 3 步：定义渲染选项（宽度、高度、抗锯齿）

现在回答核心问题：**如何启用抗锯齿**。`ImageRenderingOptions` 对象可以切换平滑功能并控制尺寸。

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

请注意注释：它们明确提到了 **set image width**、**set image height** 和 **UseAntialiasing**——这三个参数是获得精致 PNG 的关键。

### 为什么抗锯齿很重要

如果不使用抗锯齿，对角线和曲线会出现阶梯状，因为渲染器将每个像素视为完全打开或关闭。开启抗锯齿后会混合边缘像素，产生类似照片编辑器的柔和视觉效果。代价仅是极小的处理时间增加，对大多数 UI 导出而言几乎可以忽略不计。

## 第 4 步：将文档保存为 PNG（导出文档为图像）

准备好选项后，最终 **将文档保存为 PNG**。`Save` 方法接受文件路径以及我们刚配置的选项。

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

就这样——你的文档现在已经是一个 800 × 600、已应用抗锯齿的 PNG。如果打开 `output.png`，你会看到文字清晰、线条平滑，没有锯齿痕迹。

### 验证结果

可以使用任意图像查看器快速检查文件。关注以下几点：

- 正确的尺寸（800 × 600）  
- 文本或形状上没有可见的阶梯状边缘  
- 如果文档未设置背景色，则背景应为透明（大多数库默认白色）

如果图像仍然出现锯齿，请再次确认 `UseAntialiasing = true` 没有在其他地方被覆盖。

## 第 5 步：边缘情况与变体

### 更改输出格式

想要 JPEG 而不是 PNG？只需更改文件扩展名，并可选地调整压缩参数：

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### 导出多页文档

当源文档包含多页时，渲染器默认为每页生成单独的图像文件。你可以遍历页面：

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### 保存到流（例如 HTTP 响应）

如果你在构建 Web API，可能希望直接返回 PNG：

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## 完整可运行示例

下面是完整的、可直接复制粘贴的程序，包含本文讨论的所有步骤：

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

运行此程序会在可执行文件所在文件夹生成 `output.png`。打开后，你会看到一张平滑的 800 × 600 PNG——正是我们想要的效果。

## 常见问题与故障排除

- **如果图像看起来模糊怎么办？**  
  当你对较小的源页面进行放大时会出现模糊。保持源页面尺寸接近目标尺寸，或通过 `imageOptions.Resolution` 提高 DPI（例如 `Resolution = 300`）。

- **这在 .NET Framework 上能工作吗？**  
  能。相同的 API 在经典框架中也可用，只需引用相应的 DLL。

- **可以控制背景颜色吗？**  
  完全可以。在保存之前设置 `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;`。

- **抗锯齿是硬件加速的吗？**  
  大多数库使用软件抗锯齿。如果需要 GPU 加速，请寻找明确支持该功能的渲染引擎。

## 结论

我们已经介绍了 **如何在导出文档为图像时启用抗锯齿**，演示了 **设置图像宽度** 与 **设置图像高度**，并展示了 **将文档保存为 PNG** 的完整步骤。上述代码片段已可投入生产使用，且可以轻松改为 JPEG、多页 PDF，或直接将图像流式传输给客户端。

接下来，你可以尝试添加水印、调整 DPI 以获得打印质量输出，或将此逻辑集成到 ASP.NET Core 接口中。原理相同，只需将文件路径替换为响应流即可。

祝编码愉快，享受这些清晰、抗锯齿的图像吧！

![已启用抗锯齿的渲染 PNG](output.png "已启用抗锯齿的渲染 PNG")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}