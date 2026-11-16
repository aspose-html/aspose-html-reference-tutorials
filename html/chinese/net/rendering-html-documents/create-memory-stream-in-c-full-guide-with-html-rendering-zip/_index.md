---
category: general
date: 2026-03-31
description: 在 C# 中创建内存流，学习将 HTML 渲染为 PNG，使用自定义资源处理程序，将 HTML 保存为 ZIP，并以编程方式设置字体样式——全部在一个教程中。
draft: false
keywords:
- create memory stream
- render html to png
- custom resource handler
- save html to zip
- set font style programmatically
language: zh
og_description: 在 C# 中创建内存流并即时将 HTML 渲染为 PNG，使用自定义资源处理程序，将 HTML 保存为 ZIP，并以编程方式设置字体样式。
og_title: 在 C# 中创建内存流 – 完整编程指南
tags:
- C#
- HTML rendering
- Streams
- ZIP archives
- Image processing
title: 在 C# 中创建内存流 – 完整指南，包含 HTML 渲染和 ZIP 导出
url: /zh/net/rendering-html-documents/create-memory-stream-in-c-full-guide-with-html-rendering-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建 Memory Stream – 完整指南（HTML 渲染 & ZIP 导出）

是否曾想过 **在 C# 中创建 memory stream**，然后将 HTML 文档转换为 PNG 图像、ZIP 文件，甚至实时更改其字体样式？你并不孤单。许多开发者在需要文档的内存表示却不想触碰文件系统时会卡住。

在本教程中，我们将一步步实现完整的端到端解决方案：构建自定义资源处理器，将 HTML 管道化到 `MemoryStream`，将同一文档压缩为 ZIP，最后使用抗锯齿渲染为图像。完成后，你将能够 **将 HTML 渲染为 PNG**、**将 HTML 保存为 ZIP**，以及 **以编程方式设置字体样式**，而无需在磁盘上写入临时文件。

## 前置条件

- .NET 6.0 或更高（API 在最近的版本中保持稳定）。  
- 引入提供 `HTMLDocument`、`ImageRenderer` 等类型的 HTML‑to‑image 库，例如 **HtmlRenderer.Core**（请替换为你实际使用的包）。  
- 对流、`using` 语句以及 C# 面向对象模式有基本了解。

> **专业提示：** 如果使用 Visual Studio，请启用 **可空引用类型**（`<Nullable>enable</Nullable>`），以便提前捕获细微错误。

## 第一步：使用自定义资源处理器创建 Memory Stream

我们首先需要一个处理器，告诉 HTML 引擎 *将* 哪些资源（图片、CSS 等）写入何处。通过继承 `ResourceHandler`，我们可以将所有输出定向到单个 `MemoryStream`。

```csharp
using System;
using System.IO;

// Step 1: Define a handler that writes resources to an in‑memory stream
class MemoryResourceHandler : ResourceHandler
{
    // The stream lives for the whole lifetime of the handler
    public MemoryStream OutputStream = new MemoryStream();

    // The engine calls this for every resource it needs to write
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}
```

**为何重要：**  
`MemoryStream` 完全驻留在 RAM 中，意味着没有磁盘 I/O，非常适合高性能场景，如 Web 服务或单元测试。该处理器还能让 API 满意，因为引擎期望每个资源都有一个 `Stream`。

## 第二步：加载 HTML 文档并保存到 Memory Stream

现在加载已有的 HTML 文件（或字符串），并指示它使用我们的 `MemoryResourceHandler`。在调用 `Save` 后，`OutputStream` 中即包含完整的 HTML 内容。

```csharp
using System.IO;

// Assume the HTML file lives under YOUR_DIRECTORY
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

// Instantiate the memory handler
MemoryResourceHandler memoryHandler = new MemoryResourceHandler();

// Save the document – all resources flow into the same MemoryStream
htmlDoc.Save(memoryHandler);
```

此时流的位置位于末尾，需要在读取内容前将其回滚。

```csharp
// Reset the stream position to the beginning
memoryHandler.OutputStream.Position = 0;

// Quick verification (optional)
// string htmlContent = new StreamReader(memoryHandler.OutputStream).ReadToEnd();
// Console.WriteLine(htmlContent);
```

> **注意：** 上面的 `ReadToEnd` 行被注释掉了，因为在生产环境中你可能会把流直接传递给其他组件，而不是打印出来。

## 第三步：使用自定义 ZIP 资源处理器对同一 HTML 进行压缩

有时需要将 HTML 与其资源一起打包。第二个自定义处理器可以在运行时为每个资源创建 ZIP 条目。

```csharp
using System.IO.Compression;

// Step 4: Define a handler that writes each resource into a ZIP archive
class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(string zipPath)
    {
        // Open (or create) the archive in write mode
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);
    }

    // The engine calls this for each resource; we create a ZIP entry with the same name
    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    // Proper disposal of the underlying ZipArchive
    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}
```

接下来我们复用同一个 `htmlDoc` 实例，将其写入 ZIP 文件。

```csharp
// Step 5: Save the HTML document into a ZIP file
using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
{
    htmlDoc.Save(zipHandler);
}
```

**边缘情况提示：** 如果 HTML 多次引用同一图片，ZIP 处理器会创建重复的条目。为避免此问题，可以维护一个 `HashSet<string>` 来记录已添加的名称，并返回已有条目的流。

## 第四步：以编程方式设置默认样式表的字体样式

在不修改源 HTML 的情况下更改文档外观非常实用，例如在生成带粗体标题的 PDF 预览时。库提供了 `DefaultViewStyleSheet`，可以直接调整。

```csharp
// Step 6: Apply bold and italic styling to the default view stylesheet
htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

你可以组合 `WebFontStyle` 中定义的任意标志。更改是即时生效的，且会影响后续的渲染或保存。

## 第五步：将 HTML 文档渲染为 PNG 图像

最后，将 HTML 转换为栅格图像。开启抗锯齿和提示后，文字清晰、边缘平滑。

```csharp
using System.Drawing; // For ImageRenderingOptions if needed

// Step 7: Render the document to an image with antialiasing and hinting
var renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    UseHinting = true
};

new ImageRenderer(renderingOptions).Render(htmlDoc, "YOUR_DIRECTORY/out.png");
```

**你将看到：** 在 `YOUR_DIRECTORY` 下生成名为 `out.png` 的 PNG 文件，其效果与浏览器渲染的 HTML 完全一致，并且带有我们之前设置的粗斜体样式。

![创建 memory stream 输出的截图](placeholder-image.png "创建 memory stream 示例")

*图片 alt 文本包含主要关键词，以满足 SEO 要求。*

## 常见问题与注意事项

| 问题 | 答案 |
|------|------|
| **保存到 ZIP 后还能复用同一个 `HTMLDocument` 吗？** | 可以。文档对象仍驻留在内存中，你可以使用不同的处理器多次调用 `Save`。 |
| **如果 HTML 包含大型二进制资源怎么办？** | `MemoryStream` 会相应增长。对于非常大的文件，考虑直接流式写入文件或使用 `BufferedStream`。 |
| **是否需要对 `MemoryResourceHandler` 调用 `Dispose`？** | 并非强制，因为它只持有一个 `MemoryStream`，在处理器被垃圾回收时会自动释放。不过，显式调用 `Dispose` 是个好习惯。 |
| **如何更改图像格式（例如改为 JPEG 而不是 PNG）？** | 向 `ImageRenderer.Render` 传入不同的文件扩展名，或使用 `ImageRenderer.RenderToBitmap` 后通过 `bitmap.Save("out.jpg", ImageFormat.Jpeg)` 保存。 |
| **ZIP 处理器是否线程安全？** | 否。`ZipArchive` 本身不是线程安全的，请序列化访问或为每个线程创建独立的处理器。 |

## 完整可运行示例

下面是一段可直接复制粘贴的完整程序，演示本文讨论的所有步骤。请将 `YOUR_DIRECTORY` 替换为你机器上的真实路径。

```csharp
// FullExample.cs
using System;
using System.IO;
using System.IO.Compression;

// Assume these types come from your HTML rendering library
using HtmlRendering; // placeholder namespace

class MemoryResourceHandler : ResourceHandler
{
    public MemoryStream OutputStream = new MemoryStream();
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}

class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(string zipPath) =>
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);

    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // 2️⃣ Write to a memory stream
        var memHandler = new MemoryResourceHandler();
        htmlDoc.Save(memHandler);
        memHandler.OutputStream.Position = 0;
        // Optional: verify content
        // Console.WriteLine(new StreamReader(memHandler.OutputStream).ReadToEnd());

        // 3️⃣ Zip the same document
        using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
        {
            htmlDoc.Save(zipHandler);
        }

        // 4️⃣ Change font style programmatically
        htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 5️⃣ Render to PNG with antialiasing & hinting
        var renderOpts = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            UseHinting = true
        };
        new ImageRenderer(renderOpts).Render(htmlDoc, "YOUR_DIRECTORY/out.png");

        Console.WriteLine("All operations completed successfully.");
    }
}
```

运行该程序后，你将得到三个产物：

1. 存放在 `memHandler.OutputStream` 中的 **内存 HTML**。  
2. 包含 HTML 及所有关联资源的 **`output.zip`**。  
3. **`out.png`** – 一张遵循粗斜体样式的渲染图像。

## 结论

我们展示了如何在 C# 中 **创建 memory stream**，并将其无缝集成到 HTML 渲染、ZIP 打包以及图像生成中。关键要点是，同一个 `HTMLDocument` 可以通过不同的 `ResourceHandler` 保存为多种形式——`MemoryStream`、ZIP 档案或 PNG 文件。

如果你想进一步探索，可以尝试：

- 使用接受 `Stream` 的 PDF 渲染器 **渲染为 PDF**。  
- 在将数据发送到网络前 **压缩 memory stream**（例如 `GZipStream`）。  
- 将多个 HTML 页面 **合并为一个 ZIP**，实现批量导出。

尽情实验吧，如有疑问欢迎留言。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}