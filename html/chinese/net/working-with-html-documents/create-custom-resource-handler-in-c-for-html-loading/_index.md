---
category: general
date: 2026-08-15
description: 在 C# 中创建自定义资源处理程序，以管理 HTML 资源（如图像和 CSS）。学习 HTMLLoadOptions、内存流以及 HTMLDocument
  的加载。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: zh
lastmod: 2026-08-15
og_description: 在 C# 中创建自定义资源处理程序，以控制 HTML 资源的流式传输。本教程展示了 HTMLLoadOptions 的设置、内存流处理以及使用自定义逻辑加载
  HTMLDocument。
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: 在 C# 中创建自定义资源处理程序 – HTML 资源管理完整指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: 在 C# 中创建用于 HTML 加载的自定义资源处理程序
url: /zh/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建用于 HTML 加载的自定义资源处理器

如果您需要 **创建自定义资源处理器** 来处理 HTML 文件，本指南将手把手教您如何实现。您将学习在加载 HTML 文档时拦截图像、CSS 以及其他资源，使用 `HTMLLoadOptions` 和基于内存的流。

本教程涵盖实现可复用处理器、配置加载选项以及验证资源是否被正确捕获的全部内容。无需外部文档——只需下面的代码和说明即可。

## 前提条件

- .NET 6.0 或更高版本
- 基本的 C# 使用经验
- 已引用提供 `HTMLDocument`、`HtmlLoadOptions` 和 `ResourceHandler` 的 HTML 处理库（例如 GroupDocs.Viewer for .NET）

## 解决方案概览

我们将：

1. 通过继承 `ResourceHandler` **创建自定义资源处理器**。
2. 配置 `HTMLLoadOptions` 以使用该处理器。
3. 使用 `HTMLDocument` 加载 HTML 文件，处理器为每个资源提供流。
4. （可选）将接收到的资源保存到磁盘以进行验证。

每一步都包含完整的源代码及其背后的原理说明。

## 步骤 1：定义自定义资源处理器类

创建自定义处理器意味着重写 `HandleResource`，让库能够将资源字节写入您控制的流。使用 `MemoryStream` 可将数据保存在内存中，适合测试或后续处理。

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**为什么重要：**  
重写 `HandleResource` 让您完全掌控资源数据的去向。如果以后需要缓存图像、转换 CSS 或记录资源使用情况，只需将 `MemoryStream` 替换为任意自定义流实现即可。

## 步骤 2：配置 `HTMLLoadOptions` 使用该处理器

`HTMLLoadOptions` 允许您将处理器插入加载管道。设置 `ResourceHandler` 属性即可让查看器在遇到每个外部资源时调用 `MyHandler`。

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**为什么重要：**  
如果不分配 `ResourceHandler`，查看器会将资源写入默认位置（通常是临时文件夹）。通过指定自己的处理器，您 **创建自定义资源处理器** 的行为，从而符合应用的存储策略。

## 步骤 3：使用已配置的选项加载 HTML 文档

现在加载 HTML 文件。查看器会为每个遇到的资源调用 `MyHandler.HandleResource`。

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

此时 HTML 内容已被解析，所有外部资源都已流入 `MyHandler` 提供的内存缓冲区。

## 步骤 4（可选）：访问捕获的资源

如果需要检查或持久化资源，可以修改 `MyHandler`，将每个 `MemoryStream` 按资源名称存入字典。

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

加载完成后，您可以遍历 `handler.Resources` 并将每个资源写入磁盘：

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**为什么重要：**  
存储资源可用于后处理，例如图像优化、CSS 压缩或归档。它还能直观验证 **create custom resource handler** 逻辑是否如预期工作。

## 步骤 5：清理

`HTMLDocument` 与任何流都应在使用完毕后释放，以释放非托管资源。

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## 完整可运行示例

下面是一段自包含的程序，演示了从类定义到资源提取的全部步骤。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**预期输出**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

控制台会列出查看器通过您的自定义处理器流式传输的每个资源，确认 **create custom resource handler** 工作流已成功。

## 常见问题与边缘情况

| 问题 | 回答 |
|----------|--------|
| *如果资源很大（例如高分辨率图片）怎么办？* | 将 `MemoryStream` 替换为指向临时文件夹的 `FileStream`，以防止内存占用过高。 |
| *我可以按类型过滤资源吗？* | 在 `HandleResource` 中检查 `info.MimeType` 或 `info.Extension`，对不需要的类型返回 `null`。返回 `null` 会让查看器跳过该资源。 |
| *是否需要线程安全？* | 如果同一处理器实例在多个并发加载中使用，请使用锁保护 `Resources` 字典，或改用并发集合。 |
| *如何支持相对 URL？* | `ResourceInfo` 包含原始 URL，您可以将其与 HTML 文件的基路径组合，以在存储前解析相对引用。 |

## 结论

现在您已经掌握了在 C# 中 **创建自定义资源处理器** 以加载 HTML、配置 `HTMLLoadOptions`、捕获流式资源并负责任地进行清理的完整方法。此模式让您对资源管理拥有完整控制，可用于实时图像处理、CSS 重写或安全存储等场景。

接下来，您可以进一步探索 **HTMLDocument 加载** 的不同渲染选项，或扩展处理器实现 **C# resource handler**，直接写入云存储。尝试自定义 `HandleResource` 方法，以匹配项目的特定资源工作流。

## 接下来您应该学习什么？

以下教程与本指南所示技术密切相关，帮助您进一步掌握 API 功能并探索替代实现方式。

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}