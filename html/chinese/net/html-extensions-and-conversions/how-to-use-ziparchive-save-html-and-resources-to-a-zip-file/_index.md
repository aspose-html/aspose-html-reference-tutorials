---
category: general
date: 2026-03-29
description: 学习如何在 C# 中使用 ZipArchive 将 HTML 转换为 ZIP、将 HTML 保存为 ZIP，并压缩 HTML 图片——全部在一个清晰的教程中。
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: zh
og_description: 了解如何在 C# 中使用 ZipArchive 将 HTML 转换为 ZIP、将 HTML 保存为 ZIP，并压缩 HTML 图片，配有完整可运行的示例。
og_title: 如何使用 ZipArchive – 将 HTML 和资源保存到 ZIP 文件
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: 如何使用 ZipArchive – 将 HTML 和资源保存到 ZIP 文件
url: /zh/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 ZipArchive – 将 HTML 和资源保存为 ZIP 文件

是否曾经想过 **如何使用 ZipArchive** 将 HTML 页面与其图像、CSS 和其他资源打包在一起？你并不孤单。许多开发者在需要发布一个自包含的 HTML 包时会遇到困难，尤其是当页面引用外部资源时。好消息是？只需几行 C# 和 Aspose.HTML，你就可以 **将 HTML 转换为 ZIP**、**将 HTML 保存为 ZIP**，甚至 **压缩 HTML 图像**，而无需离开 IDE。

在本教程中，我们将完整演示整个过程——从创建一个简单的 `HTMLDocument` 到通过自定义 `ResourceHandler` 处理每个链接资源。完成后，你将拥有一个可直接使用的 ZIP 文件，能够放入任何 Web 服务器或作为电子邮件附件。无需外部脚本，无需手动复制——纯 .NET。

## 前提条件

- **.NET 6+**（或 .NET Framework 4.6+）。使用的 API 属于 `System.IO.Compression`。
- **Aspose.HTML for .NET** 已安装（NuGet 包 `Aspose.Html`）。
- 对 C# 语法有基本了解。
- 使用 Visual Studio 或 VS Code 等 IDE。

就这些。无需额外工具，也不需要第三方 zip 实用程序。准备好了吗？让我们开始吧。

## 第一步：设置项目并添加依赖

Create a new console project:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

`Aspose.Html` 包提供了 `HTMLDocument` 类和我们稍后会扩展的 `ResourceHandler` 基类。内置的 `System.IO.Compression` 命名空间提供了 `ZipArchive` 和 `ZipArchiveEntry`。

> **小贴士：** 如果目标是 .NET 6，可以使用顶级语句来保持 `Main` 方法简洁。下面的代码使用经典的 `Program` 类以便更清晰。

## 第二步：创建自定义资源处理程序

当 Aspose.HTML 保存文档时，它会请求 `ResourceHandler` 为每个外部文件（图像、CSS、字体等）提供一个 `Stream`。通过重写 `HandleResource`，我们可以直接将每个资源写入 zip 条目。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**为什么这很重要：** 与其先将资源写入磁盘再压缩，不如让处理程序直接流式写入 zip，这样可以减少 I/O 开销，并确保 zip 与 HTML 内容保持同步。

## 第三步：构建 HTML 文档

为了演示，我们将嵌入一个引用外部图像 `logo.png` 的小型 HTML 片段。在实际项目中，你可能会从文件或数据库加载 HTML。

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

如果需要 **压缩 HTML 图像**，只需确保图像文件位于可执行文件旁边（或作为资源嵌入）。`ZipResourceHandler` 会自动将图像添加到归档中。

## 第四步：打开（或创建）ZIP 文件并保存

现在我们把所有内容连接起来。我们为输出 zip 打开一个 `FileStream`，以 *Update* 模式实例化 `ZipArchive`，并将自定义处理程序传递给 `HTMLDocument.Save`。

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

当 `using` 块结束时，zip 会自动完成并关闭。生成的 `output.zip` 包含：

- `index.html`（序列化的 HTML 文档）
- `logo.png`（HTML 中引用的图像）

你可以通过任意文件资源管理器打开 zip 来验证内容。

## 第五步：验证结果（可选）

最好再次确认 zip 实际可用。下面是一段可以在前面代码后运行的简短片段，用于列出条目：

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

你应该会看到类似如下内容：

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

从解压后的文件夹打开 `index.html`，你会看到图像正确渲染——这证明 **save HTML to ZIP** 按预期工作。

## 常见变体与边缘情况

### 1. 为 HTML 文件使用不同的条目名称

默认情况下 Aspose 将 HTML 写入 `index.html`。如果需要自定义名称，可以在保存前设置 `htmlDocument.FileName`：

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. 手动添加额外文件

有时你想打包额外的文件（例如 README）。可以在调用 `htmlDocument.Save` 之前直接向 `ZipArchive` 添加它们：

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. 高效处理大图像

如果你的 HTML 引用的图像非常大，建议事先对其进行缩放，以保持 zip 大小合理。`System.Drawing.Common` 包可以帮助完成此操作：

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

然后在 HTML 中将 `<img src='logo_resized.png'>` 指向该图像。

## 完整、可运行的示例

下面是完整的程序，你可以复制粘贴到 `Program.cs` 中。只要已安装 Aspose.HTML NuGet 包，它即可直接编译运行。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**预期输出：** 控制台会打印成功信息，`output.zip` 会出现在项目文件夹中，包含 `index.html` 和 `logo.png`。

## 常见问题

- **这在 .NET Core 上可用吗？**  
  是的。`System.IO.Compression.ZipArchive` 属于 .NET Standard，因此相同代码可在 .NET 5、.NET 6 和 .NET 7 上运行。

- **如果需要更强力地 **压缩 HTML 图像**？**  
  你可以在将图像添加到 zip 之前进行预处理（调整大小、转换为 WebP 等）。处理程序本身只会流式传输它收到的数据。

- **我可以加密 zip 吗？**  
  `ZipArchive` 仅通过第三方库（例如 `SharpZipLib`）支持 AES 加密。如果需要加密，可使用该库创建 zip，然后将流作为自定义 `ResourceHandler` 提供给 Aspose。

- **有没有办法设置 zip 内的根文件夹？**  
  有——在 `HandleResource` 中给 `resourceName` 前加上文件夹名称，例如 `var entry = _zipArchive.CreateEntry($\"site/{resourceName}\", ...)`。

## 结论

现在你已经了解了在 C# 中 **如何使用 ZipArchive** 来 **将 HTML 转换为 ZIP**、**将 HTML 保存为 ZIP**，以及 **压缩 HTML 图像**，整个过程简洁统一。通过扩展 `ResourceHandler`，我们避免了任何临时文件，使过程在内存使用上更高效。该模式易于扩展：只需将生成的 zip 放到 Web 服务器、通过电子邮件发送，或存入云存储即可。

接下来你可以探索的方向：

- **以编程方式创建 ZIP 归档**，用于整个网站文件夹（`create zip archive c#`）。
- **在压缩前添加 PDF 或 DOCX 转换**，以获得更丰富的文档包。
- **与 ASP.NET Core 集成**，将 zip 直接流式传输到客户端浏览器（`FileStreamResult`）。

对压缩 HTML、处理字体或优化图像大小还有疑问？请在评论区留言或在 Stack Overflow 上联系我。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}