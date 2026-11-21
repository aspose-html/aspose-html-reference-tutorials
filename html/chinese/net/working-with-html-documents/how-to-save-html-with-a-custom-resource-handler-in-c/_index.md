---
category: general
date: 2026-11-20
description: 学习如何使用自定义 ResourceHandler 在 C# 中保存 HTML，并使用简洁、可用于生产的代码将 HTML 保存到 zip
  压缩包中。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: zh
lastmod: 2026-11-20
og_description: 如何使用自定义 ResourceHandler 在 C# 中保存 HTML，并可选地将 HTML 保存到 zip 文件——面向 .NET
  开发者的完整可运行指南。
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: 如何使用自定义资源处理程序在 C# 中保存 HTML
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: 如何在 C# 中使用自定义资源处理程序保存 HTML
url: /zh/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用自定义资源处理程序保存 HTML

如果您需要了解 **如何保存 HTML**，无论是来自内存字符串还是已解析的文档，本指南提供完整的解决方案。使用自定义 `ResourceHandler` 可以控制目标流，这意味着您可以 **将 HTML 保存为 zip** 归档，而无需写入临时文件。

您将看到为什么相较于旧的 `IOutputStorage` 方法更倾向使用 `ResourceHandler`，以及如何设置它、如何扩展以实现 zip 压缩。完成本教程后，您可以将代码嵌入任何 .NET 6+ 项目，并根据自己的存储需求进行适配。

## 您将构建的内容

* 一个返回 `MemoryStream` 的最小 `ResourceHandler`。
* 使用 **HtmlAgilityPack** 创建的 `HtmlDocument`。
* 调用 `doc.Save` 将 HTML 写入处理程序提供的流。
* 一个可选的包装器，将生成的 HTML 压缩为 zip 文件。

前置条件：

* .NET 6 SDK 或更高版本。
* `HtmlAgilityPack` NuGet 包（`dotnet add package HtmlAgilityPack`）。
* 对 C# 流的基本了解。

## 第一步：创建自定义资源处理程序（主要方式来 **how to save html**）

`ResourceHandler` 基类（自查看器 SDK 版本 24.2 起可用）定义了一个抽象方法 `HandleResource`。实现此方法即可完全控制 HTML 的写入位置。

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**为什么重要：** 返回 `MemoryStream` 可以避免磁盘 I/O，降低延迟，并使单元测试保持确定性。该处理程序会被 `Save` 方法自动调用，您无需显式传递流。

## 第二步：加载或构建 HTML 文档

`HtmlAgilityPack` 提供了便利的 `HtmlDocument` 类，可解析字符串、文件或流。此示例中我们加载一个简单的字面量，相同代码同样适用于任何 HTML 源。

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**为什么重要：** 将文档保存在内存中与自定义处理程序的流式方式保持一致。它还允许您在保存前操作 DOM，例如注入脚本或修复错误标签。

## 第三步：使用自定义处理程序保存文档

使用 `MyHandler` 实例调用 `doc.Save` 会触发 `HandleResource` 方法。HTML 直接写入您返回的流。

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

`Save` 完成后，`MyHandler` 中的 `MemoryStream` 包含序列化后的 HTML。您可以这样获取：

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**结果：** 控制台会打印出您传入 `LoadHtml` 的完整 HTML，证明您已经掌握了 **如何使用自定义处理程序保存 HTML**。

## 第四步：扩展处理程序以 **save HTML to zip**

如果希望将 HTML 打包归档，只需修改 `MyHandler`，让其写入 `ZipArchiveEntry`。.NET 的 `System.IO.Compression` 命名空间使此操作非常简洁。

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

现在使用新的处理程序：

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**为什么可行：** `HandleResource` 方法创建名为 `document.html` 的 zip 条目。当 `doc.Save` 写入返回的流时，数据会自动压缩。由于 zip 在内存中构建，您可以直接从 Web API 返回、作为电子邮件附件发送，或存入数据库，而无需触及文件系统。

## 常见问题与边缘情况

### 如果需要在同一个 zip 中包含多个 HTML 文件怎么办？
为每次调用 `HandleResource` 创建一个新条目。`resourceName` 参数通常包含文件名，您可以直接使用：

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### 如何处理大型文档而不耗尽内存？
将 `MemoryStream` 替换为指向临时文件的 `FileStream`。处理程序返回文件流，压缩完成后再删除该临时文件。

### 该方案在 Linux 上的 .NET Core 能否使用？
可以。所有使用的 API（`MemoryStream`、`ZipArchive`、`HtmlAgilityPack`）均跨平台。确保目标框架至少为 .NET 6，以获得最佳兼容性。

### 能对 zip 包进行加密吗？
`ZipArchive` 本身仅通过第三方库（如 `SharpZipLib`）支持基于密码的加密。如果需要加密，可在将输出字节发送给客户端之前，使用提供 AES 加密的库对其进行包装。

## 专业技巧

* **复用处理程序**：在批量处理多个文档时复用同一个处理程序，避免为每个文件创建新的 `ZipArchive`，从而降低开销。
* **在 ZipArchive 构造函数中设置 `LeaveOpen: true`**：如果需要在归档仍打开时读取 zip 字节，这一点非常有用。
* **保存前验证 HTML**：调用 `doc.OptionCheckSyntax = true;` 可以提前捕获错误标签。
* **记录生成的 zip 大小**：异常大的输出通常意味着资源重复或压缩未生效。

## 完整可运行示例

下面是一个单文件示例，可直接粘贴到控制台项目（`dotnet new console`）并运行。它演示了普通 HTML 保存和 zip 压缩两种方式。



## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在自己的项目中进一步掌握 API 功能并探索替代实现方式。每个资源都提供完整的可运行代码示例和一步步的解释。

- [如何在 C# 中使用自定义资源处理程序保存 HTML](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [如何使用 ZipArchive – 将 HTML 和资源保存为 ZIP 文件](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [使用自定义资源处理程序将 HTML 保存为 zip – 步骤指南](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}