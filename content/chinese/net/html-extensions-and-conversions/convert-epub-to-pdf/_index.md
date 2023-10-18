---
title: 使用 Aspose.HTML 将 EPUB 转换为 .NET 中的 PDF
linktitle: 在 .NET 中将 EPUB 转换为 PDF
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML for .NET 将 EPUB 转换为 PDF。本分步指南涵盖了无缝文档转换的自定义选项、常见问题解答等。
type: docs
weight: 12
url: /zh/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

在本教程中，我们将探讨如何使用 Aspose.HTML for .NET 将 EPUB 文件转换为 PDF。 Aspose.HTML 是一个功能强大的.NET 库，提供了处理 HTML 和 EPUB 文档的各种功能。我们将介绍先决条件，导入必要的命名空间，并分解多个示例，详细解释每个步骤。

## 先决条件

在开始之前，请确保您具备以下先决条件：

1. Aspose.HTML for .NET：确保您的 .NET 项目中安装了 Aspose.HTML for .NET。您可以从以下位置下载：[这里](https://releases.aspose.com/html/net/).

2. 您的数据目录：您将需要一个用于存储 EPUB 文件的数据目录。

现在，让我们深入了解使用 Aspose.HTML for .NET 将 EPUB 转换为 PDF 的分步过程。

## 将 EPUB 转换为 PDF

### 第 1 步：初始化您的项目

确保您已设置 .NET 项目，并安装了 Aspose.HTML for .NET。

### 第2步：导入所需的命名空间

在您的 C# 代码文件中，导入必要的命名空间：

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### 步骤 3：打开 EPUB 文件

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //继续下一步...
}
```

- 代替`"Your Data Directory"`与 EPUB 文件所在的实际目录。
- 此代码打开 EPUB 文件进行阅读。

### 步骤 4：设置 PDF 选项并执行转换

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

- 创建一个实例`PdfSaveOptions`指定 PDF 转换设置。
- 使用`Converter.ConvertEPUB`使用给定选项将 EPUB 转换为 PDF 的方法。
- 将生成的 PDF 保存为“output.pdf”。

## 指定 PDF 保存选项

### 第 1 步：初始化您的项目

确保您已设置 .NET 项目并安装了 Aspose.HTML for .NET。

### 第2步：导入所需的命名空间

在 C# 代码中导入必要的命名空间：

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### 步骤 3：打开 EPUB 文件

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //继续下一步...
}
```

- 代替`"Your Data Directory"`与 EPUB 文件的实际目录。
- 打开 EPUB 文件进行阅读。

### 第 4 步：自定义 PDF 选项

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

- 创建一个实例`PdfSaveOptions`并根据您的要求进行定制。
- 在此示例中，我们将页面大小设置为宽度 3000 像素、高度 1000 像素，背景颜色设置为 Alice Blue。

### 第5步：执行转换

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

- 使用`Converter.ConvertEPUB`使用自定义选项将 EPUB 转换为 PDF 的方法。
- 将生成的 PDF 保存为“output.pdf”。

## 使用自定义流提供程序

### 第 1 步：初始化您的项目

设置 .NET 项目并安装 Aspose.HTML for .NET。

### 第2步：导入所需的命名空间

在您的 C# 代码中，导入必要的命名空间：

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### 步骤 3：打开 EPUB 文件

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //继续下一步...
}
```

- 代替`"Your Data Directory"`与 EPUB 文件的实际目录。
- 打开 EPUB 文件进行阅读。

### 第 4 步：使用自定义流提供程序

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    //继续下一步...
}
```

- 创建一个`MemoryStreamProvider`将转换结果作为内存流进行管理。
- 使用`Converter.ConvertEPUB`方法与自定义流提供程序。

### 第 5 步：保存结果

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- 访问包含转换后的数据的内存流。
- 将流位置设置为开头。
- 创建一个输出 PDF 文件并将内容从内存流复制到其中。

### MemoryStreamProvider 类源代码。 

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            //文档渲染期间创建的 MemoryStream 对象列表
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                //当仅需要一个输出流时（例如 XPS、PDF 或 TIFF 格式），将调用此方法。
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                //当需要创建多个输出流时调用此方法。例如，在渲染 HTML 到图像文件列表（JPG、PNG 等）期间
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                //在这里您可以释放充满数据的流，例如将其刷新到硬盘驱动器
            }
            public void Dispose()
            {
                //释放资源
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
现在，您已经学习了如何使用 Aspose.HTML for .NET 将 EPUB 文件转换为 PDF，并具有各种选项和自定义可能性。 Aspose.HTML 简化了流程，提供了对文档转换的灵活性和控制。

## 结论

Aspose.HTML for .NET 是一款用于将 EPUB 文件转换为 PDF 的多功能工具，提供自定义选项以根据您的需求定制生成的 PDF 文档。无论您需要简单的转换还是高级自定义，Aspose.HTML 都能满足您的需求。

如果您还没有下载 Aspose.HTML for .NET，您可以从[网站](https://releases.aspose.com/html/net/)立即开始在您的 .NET 应用程序中使用它。

---

## 常见问题解答

### Aspose.HTML for .NET 可以免费使用吗？
    Aspose.HTML for .NET 是一个商业产品，但可以免费试用[这里](https://releases.aspose.com/).

### 我可以自定义转换后的 PDF 的外观吗？
   是的，您可以通过调整页面大小和背景颜色等选项来自定义 PDF 外观，如示例 2 所示。

### 如何获得 Aspose.HTML for .NET 支持？
   您可以在以下位置找到支持和资源[Aspose.HTML 论坛](https://forum.aspose.com/).

### 我可以使用 Aspose.HTML for .NET 转换其他格式吗？
   是的，Aspose.HTML for .NET 支持各种文档格式，包括 HTML、EPUB 等。

### Aspose.HTML for ..NET适合大规模文档转换吗？
   Aspose.HTML for .NET 旨在高效处理大规模文档转换，使其适用于广泛的应用程序。

