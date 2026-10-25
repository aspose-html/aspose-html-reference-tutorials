---
category: general
date: 2026-10-25
description: 如何使用 ResourceHandler 控制资源加载，以及如何在 C# 中使用 Aspose.HTML 将 HTML 保存到流中。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use resourcehandler
- how to save html to stream
- Aspose.HTML ResourceHandler
- HTML to MemoryStream C#
- custom resource handling C#
language: zh
lastmod: 2026-10-25
og_description: 如何使用 ResourceHandler 控制资源加载，以及如何使用 Aspose.HTML for .NET 将 HTML 保存到流中。
og_image_alt: Screenshot of C# code using ResourceHandler to save HTML to a memory
  stream
og_title: 如何在 C# 中使用 ResourceHandler 并将 HTML 保存到流
schemas:
- author: Aspose
  dateModified: '2026-10-25'
  description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  headline: How to use ResourceHandler and save HTML to a stream in C#
  type: TechArticle
- description: How to use ResourceHandler to control resource loading and how to save
    HTML to a stream using Aspose.HTML in C#.
  name: How to use ResourceHandler and save HTML to a stream in C#
  steps:
  - name: Expected output
    text: 'Running the code above prints:'
  - name: 1. Embedding real resources
    text: 'If you need to embed an image, modify `MyHandler` to return a stream that
      contains the image bytes:'
  - name: 2. Handling large documents
    text: For very large HTML files, consider using `BufferedStream` or writing directly
      to a file‑based `FileStream` if memory becomes a bottleneck. The pattern for
      **how to save HTML to a stream** stays the same; only the stream type changes.
  - name: 3. Thread safety
    text: '`ResourceHandler` instances are **not** guaranteed to be thread‑safe. If
      you plan to reuse a handler across parallel conversions, either:'
  - name: 4. Disposing resources
    text: Both `HTMLDocument` and any streams you create implement `IDisposable`.
      Wrapping them in `using` blocks, as shown in Step 4, guarantees clean release
      of unmanaged resources.
  - name: What’s next?
    text: '* **Embed real images or CSS** by extending `MyHandler` (see the “Embedding
      real resources” section). * **Convert the stream to PDF** with `HtmlConverter.ConvertHtml`
      if you need a printable version. * **Stream the result directly from a Web API**
      using `FileStreamResult` or `MemoryStream` in ASP.NE'
  type: HowTo
tags:
- Aspose.HTML
- C#
- Stream handling
title: 如何在 C# 中使用 ResourceHandler 并将 HTML 保存到流
url: /zh/net/working-with-html-documents/how-to-use-resourcehandler-and-save-html-to-a-stream-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 ResourceHandler 并将 HTML 保存到流中

如果您需要在使用 Aspose.HTML 渲染 HTML 时 **how to use ResourceHandler**，本指南将向您展示一个完整、可直接运行的解决方案。您还将学习 **how to save HTML to a stream**，以便在不触及文件系统的情况下传输输出。

在内存中处理 HTML 是在即时生成电子邮件、API 响应或 PDF 时的常见做法。完成本教程后，您将拥有一个独立的 C# 程序，它创建 `HTMLDocument`，提供自定义 `ResourceHandler`，并将结果写入 `MemoryStream`。

## 前提条件

* .NET 6.0 或更高版本（代码同样适用于 .NET Core 3.1 和 .NET Framework 4.7+）
* **Aspose.HTML for .NET** NuGet 包  
  ```bash
  dotnet add package Aspose.HTML
  ```
* 对 C# async/await 有基本了解（可选但有帮助）

## 本教程涵盖内容

* 如何 **how to use ResourceHandler** 来拦截图像、CSS 或脚本请求
* 如何使用自定义处理程序配置 `HtmlSaveOptions`
* 如何 **how to save HTML to a stream** 使用 `MemoryStream`
* 边缘情况处理，例如缺少资源和流的释放
* 扩展处理程序以在以后嵌入真实资源的技巧

## 步骤 1：从字符串创建简单的 HTML 文档

第一步是从原始 HTML 实例化一个 `HTMLDocument`。该对象表示 Aspose.HTML 将要渲染的 DOM 树。

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System.IO;

// Simple HTML markup – you can replace this with any valid HTML string.
string htmlContent = "<html><body>Hello World</body></html>";

// The HTMLDocument constructor parses the string into a DOM.
HTMLDocument document = new HTMLDocument(htmlContent);
```

> **为什么这很重要：** 从字符串创建文档可以将整个工作流保持在内存中，这在您随后 **how to save HTML to a stream** 而不触及磁盘时至关重要。

## 步骤 2：实现自定义 ResourceHandler

`ResourceHandler` 是 Aspose.HTML 在需要外部资源（图像、CSS、字体等）时使用的钩子。通过重写 `HandleResource`，您可以决定为每个请求返回哪个流。

```csharp
// Define a handler that supplies an empty stream for every resource request.
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(Resource resource)
    {
        // Returning an empty MemoryStream effectively disables external resources.
        // You could return a real image stream here if you need to embed assets.
        return new MemoryStream();
    }
}

// Instantiate the handler so it can be attached to the save options.
MyHandler customHandler = new MyHandler();
```

> **您可能需要此功能的原因：** 在为电子邮件或 API 响应生成 HTML 时，通常不希望进行外部调用。提供空流可以防止 404 错误并加快渲染速度。这演示了 **how to use ResourceHandler** 用于“无资源”输出的方式。

## 步骤 3：配置 HtmlSaveOptions 以使用自定义处理程序

`HtmlSaveOptions` 让您能够控制保存过程。将 `ResourceHandler` 属性分配为您自定义的实现。

```csharp
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Attach the handler so every resource request goes through MyHandler.
    ResourceHandler = customHandler
};
```

> **提示：** 如果以后需要嵌入 CSS 或图像，请将 `MyHandler` 替换为根据 `resource.Uri` 返回相应流的版本。

## 步骤 4：将文档保存到 MemoryStream

现在您已经准备好 **how to save HTML to a stream**。使用 `MemoryStream` 可将输出保留在 RAM 中，便于通过 HTTP 发送、存储到数据库或传递给其他 API。

```csharp
using (MemoryStream outputStream = new MemoryStream())
{
    // The Save method writes the HTML (and any referenced resources) into the stream.
    document.Save(outputStream, saveOptions);

    // Reset the position so callers can read from the beginning.
    outputStream.Position = 0;

    // Example: Convert the stream to a string for debugging.
    using (StreamReader reader = new StreamReader(outputStream))
    {
        string resultHtml = reader.ReadToEnd();
        System.Console.WriteLine(resultHtml);
    }

    // At this point, outputStream can be returned from a web API, attached to an email,
    // or passed to another component without ever touching the file system.
}
```

### 预期输出

运行上述代码会输出：

```html
<html><head></head><body>Hello World</body></html>
```

由于自定义处理程序返回空流，外部的 `<link>` 或 `<img>` 标签未被解析，HTML 保持干净。

## 常见变体和边缘情况

### 1. 嵌入真实资源

如果需要嵌入图像，请修改 `MyHandler` 以返回包含图像字节的流：

```csharp
public override Stream HandleResource(Resource resource)
{
    if (resource.Uri.EndsWith(".png"))
    {
        // Load the PNG from embedded resources or a database.
        byte[] imageBytes = File.ReadAllBytes("logo.png");
        return new MemoryStream(imageBytes);
    }
    return new MemoryStream(); // Fallback for other resources.
}
```

### 2. 处理大型文档

对于非常大的 HTML 文件，如果内存成为瓶颈，可考虑使用 `BufferedStream` 或直接写入基于文件的 `FileStream`。**how to save HTML to a stream** 的模式保持不变，仅流的类型会改变。

### 3. 线程安全

`ResourceHandler` 实例 **不** 保证线程安全。如果您计划在并行转换中复用处理程序，请：

* 为每次转换创建一个新处理程序，或
* 在 `HandleResource` 中使用锁保护共享状态。

### 4. 释放资源

`HTMLDocument` 和您创建的任何流都实现了 `IDisposable`。如步骤 4 所示，将它们包装在 `using` 块中，可确保未受管理资源的干净释放。

## 专业提示：复用同一个 MemoryStream

如果需要将多个 HTML 输出合并到同一个流中，请在每次 `Save` 调用前重置位置：

```csharp
outputStream.Position = 0; // Clear previous content
document.Save(outputStream, saveOptions);
```

或者，为每次转换创建一个新的 `MemoryStream`，以避免意外的数据混合。

## 完整工作示例

下面是完整的程序，您可以复制粘贴到控制台应用程序中。它可在 .NET 6.0 和 Aspose.HTML 23.9（或更高版本）下编译。

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using System;
using System.IO;

namespace ResourceHandlerDemo
{
    // Custom handler that supplies empty streams for any requested resource.
    class MyHandler : ResourceHandler
    {
        public override Stream HandleResource(Resource resource)
        {
            // Return an empty stream to suppress external resources.
            return new MemoryStream();
        }
    }

    class Program
    {
        static void Main()
        {
            // Step 1: Create the HTML document.
            string htmlContent = "<html><body>Hello World</body></html>";
            HTMLDocument document = new HTMLDocument(htmlContent);

            // Step 2: Attach the custom ResourceHandler.
            MyHandler customHandler = new MyHandler();

            // Step 3: Configure save options.
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                ResourceHandler = customHandler
            };

            // Step 4: Save to a MemoryStream.
            using (MemoryStream outputStream = new MemoryStream())
            {
                document.Save(outputStream, saveOptions);
                outputStream.Position = 0;

                // Display the generated HTML for verification.
                using (StreamReader reader = new StreamReader(outputStream))
                {
                    string resultHtml = reader.ReadToEnd();
                    Console.WriteLine("Generated HTML:");
                    Console.WriteLine(resultHtml);
                }
            }
        }
    }
}
```

运行程序后，您将在控制台看到生成的 HTML 输出，确认 **how to use ResourceHandler** 和 **how to save HTML to a stream** 能够无缝协同工作。

## 结论

本教程演示了 **how to use ResourceHandler** 用于控制外部资源加载，以及使用 Aspose.HTML 在 C# 中 **how to save HTML to a stream** 的完整步骤。您现在拥有一种可复用的内存中 HTML 生成模式，非常适用于 Web API、电子邮件模板和 PDF 转换流水线。

### 接下来做什么？

* **通过扩展 `MyHandler` 来嵌入真实的图像或 CSS**（请参阅“嵌入真实资源”章节）。
* **使用 `HtmlConverter.ConvertHtml` 将流转换为 PDF**，如果您需要可打印的版本。
* **在 Web API 中直接流式传输结果**，使用 ASP.NET 中的 `FileStreamResult` 或 `MemoryStream`。

## 接下来应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方法。

- [如何在 C# 中保存 HTML – 使用自定义资源处理程序的完整指南](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [如何在 C# 中使用自定义资源处理程序保存 HTML](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [如何在 Aspose.HTML 中使用处理程序 – 加载 HTML，保存为 ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-handler-in-aspose-html-load-html-save-as-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}