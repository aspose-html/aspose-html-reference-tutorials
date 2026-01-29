---
category: general
date: 2025-12-29
description: 如何使用 Aspose.HTML 在 C# 中快速压缩 HTML —— 使用自定义 ZipResourceHandler 将 HTML 保存为
  zip。一步一步学习。
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: zh
og_description: 如何使用 Aspose.HTML 在 C# 中快速压缩 HTML。请按照本指南将 HTML 保存为 zip 并使用自定义资源处理创建
  zip 存档。
og_title: 如何在 C# 中压缩 HTML – 将 HTML 保存为 Zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: 如何在 C# 中压缩 HTML – 将 HTML 保存为 Zip
url: /zh/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中压缩 HTML – 将 HTML 保存为 Zip

在需要离线使用网页时，如何在 C# 中压缩 HTML 是一个常见需求。无论是将单个页面连同其图片打包，还是导出整个站点，**将 HTML 保存为 zip** 都能让内容整洁且便于携带。在本教程中，我们将完整演示一个可直接运行的解决方案，它不仅会压缩 HTML 标记，还会将所有引用的资源直接流式写入压缩包。

你将学会：

* 使用 .NET 的 `System.IO.Compression` 编程创建 zip 压缩包。
* 将自定义 `ResourceHandler` 插入 Aspose.HTML，使资源直接写入 zip。
* 处理已有 zip 文件和大二进制资源等边缘情况。

无需任何外部工具——只需 C#、Aspose.HTML 和几行代码。

## 你需要的环境

在开始之前，请确保拥有：

* **.NET 6+**（代码同样适用于 .NET Framework 4.6.2 及以上）。
* **Aspose.HTML for .NET** – 可从 Aspose 官网获取免费试用版，或使用已授权的版本。
* 开发环境（Visual Studio、VS Code、Rider——任选其一）。

就这些。除 `System.IO.Compression`（随 .NET 捆绑）和 `Aspose.HTML` 外，无需额外的 NuGet 包。

## 第一步：创建项目并导入命名空间

新建一个控制台项目（或在已有项目中加入代码）。在文件顶部添加所需的 `using` 指令：

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Pro tip:** 如果使用 Visual Studio，IDE 会提示添加缺失的 `Aspose.Html` NuGet 包。接受即可开始编写代码。

## 第二步：实现自定义 ZipResourceHandler

Aspose.HTML 在需要写入资源（如图片、CSS 文件或脚本）时会调用 `ResourceHandler`。通过重写 `HandleResource`，我们可以决定每个资源的写入位置。下面的处理器会创建一个与资源逻辑路径对应的 zip 条目，并返回指向该条目的可写流。

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Why this matters:**  
与先将资源写入临时文件夹再整体压缩不同，此处理器在写入时直接流式传输数据，减少磁盘 I/O 并保持低内存占用。它还能确保 zip 内部的文件夹层级与 HTML 的相对路径保持一致，浏览器在解压后打开页面时能够正确定位资源。

## 第三步：准备 Zip 压缩包

接下来打开（或创建）目标 zip 文件。`FileMode.Create` 标志会覆盖已有文件——非常适合可重复构建的场景。如果希望保留已有压缩包，可改为 `FileMode.OpenOrCreate` 并自行处理重复条目。

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Edge case:** 若进程在 `using` 块释放压缩包之前崩溃，可能会留下损坏的 zip。将代码放在 try/catch 中，并在失败时删除部分生成的文件，是一种简单的防护措施。

## 第四步：构建带嵌入资源的 HTML 文档

演示中，我们创建一个引用名为 `image.png` 的图片的简易 HTML 页面。在实际项目中，你可能会从文件或数据库中的字符串加载 HTML。

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

如果磁盘上已有真实的图片文件，可以在保存 HTML 前手动将它们加入 zip，或让 Aspose.HTML 通过处理器自行获取（例如从 URL）。我们编写的处理器同时支持本地路径和远程 URL。

## 第五步：配置保存选项以使用 ZipResourceHandler

现在告诉 Aspose.HTML 在写出资源时使用我们的自定义处理器。`HTMLSaveOptions` 类还允许指定 zip 内部的输出文件名，默认是 `index.html`。

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## 第六步：保存文档——所有内容直接流入 Zip

最后，调用 `Save`。Aspose.HTML 解析标记，定位 `<img>` 标签，调用 `HandleResource` 处理 `image.png`，并将 HTML 文件和图片一起写入同一个 zip 包。

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

当 `using` 块结束时，`ZipArchive` 会完成文件的最终写入，使其可以直接分发。

### 完整示例代码

下面是完整的程序代码。复制粘贴到 `Program.cs` 并运行——无需额外修改。

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Expected result:** 执行后，`output.zip` 包含两个条目：

```
index.html
image.png
```

如果解压后在浏览器中打开 `index.html`，图片能够正确显示，因为相对路径已被保留。

## 常见问题

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}