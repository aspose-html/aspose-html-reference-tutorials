---
title: 使用 Aspose.HTML 在 .NET 中将 EPUB 转换为 XPS
linktitle: 在 .NET 中将 EPUB 转换为 XPS
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML for .NET 在 .NET 中将 EPUB 转换为 XPS。按照我们的分步指南轻松完成转换。
weight: 13
url: /zh/net/html-extensions-and-conversions/convert-epub-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML 在 .NET 中将 EPUB 转换为 XPS


您是否正在寻找一种无缝方法，在 .NET 应用程序中将 EPUB 文件转换为 XPS 格式？Aspose.HTML for .NET 提供了一个强大的解决方案，可轻松实现此目的。在本分步指南中，我们将引导您完成使用 Aspose.HTML 将 EPUB 转换为 XPS 的过程。让我们开始吧！

## 先决条件

在深入了解 EPUB 到 XPS 的转换过程之前，您需要确保已满足以下先决条件：

### 1. Aspose.HTML for .NET 库

确保你的项目中安装了 Aspose.HTML for .NET 库。如果你还没有安装，你可以从[Aspose.HTML for .NET 下载页面](https://releases.aspose.com/html/net/).

### 2. 输入 EPUB 文件

您需要一个要转换为 XPS 的 EPUB 文件。确保您有一个可供转换的 EPUB 文件。

### 3. .NET 开发环境

本指南假设您的机器上已设置了可运行的 .NET 开发环境。

## 导入命名空间

首先，您应该导入 Aspose.HTML 必要的命名空间：

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## 将 EPUB 转换为 XPS

让我们将 EPUB 文件转换为 XPS 格式的过程分解为多个步骤。

### 步骤1.1：打开EPUB文件

首先，使用 FileStream 打开现有的 EPUB 文件进行阅读：

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //继续转换过程
}
```

### 步骤 1.2：创建 XpsSaveOptions

创建 XpsSaveOptions 的实例。此步骤对于配置 XPS 输出至关重要：

```csharp
var options = new XpsSaveOptions();
```

### 步骤 1.3：将 EPUB 转换为 XPS

现在，让我们调用 ConvertEPUB 方法将 EPUB 转换为 XPS：

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## 指定自定义 XPS 选项

您可以通过指定自定义选项（例如页面大小和背景颜色）进一步定制 XPS 输出。

### 步骤 2.1：自定义页面大小和背景颜色

使用自定义页面大小和背景颜色创建 XpsSaveOptions 的实例：

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### 步骤 2.2：使用自定义选项将 EPUB 转换为 XPS

现在，调用 ConvertEPUB 方法使用自定义选项将 EPUB 转换为 XPS：

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## 使用自定义流提供程序

在此步骤中，我们将使用自定义流提供程序将 EPUB 转换为 XPS，以便您操作生成的数据。

### 步骤 3.1：创建 MemoryStreamProvider

创建 MemoryStreamProvider 的实例：

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    //继续转换过程
}
```

### 步骤 3.2：使用 Stream Provider 将 EPUB 转换为 XPS

使用 MemoryStreamProvider 将 EPUB 转换为 XPS：

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### 步骤 3.3：访问并保存结果

检索包含转换数据的内存流并将其保存到输出文件：

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### MemoryStreamProvider 类源代码

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            //文档渲染期间创建的 MemoryStream 对象列表
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                //当只需要一个输出流时（例如 XPS、PDF 或 TIFF 格式），将调用此方法。
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                //当需要创建多个输出流时，将调用此方法。例如，在将 HTML 渲染到图像文件列表（JPG、PNG 等）期间
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                //在这里，你可以释放充满数据的流，例如，将其刷新到硬盘上
            }
            public void Dispose()
            {
                //释放资源
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
恭喜！您已成功使用 Aspose.HTML for .NET 将 EPUB 文件转换为 XPS 格式。

## 结论

在本综合教程中，我们探讨了如何利用 Aspose.HTML for .NET 将 EPUB 文件转换为 XPS 格式，并提供各种自定义选项。无论您是经验丰富的开发人员还是刚刚起步，Aspose.HTML 都可以简化此过程，让您轻松处理 EPUB 到 XPS 的转换。

有疑问或遇到问题？查看[Aspose.HTML 文档](https://reference.aspose.com/html/net/)了解更多见解或寻求帮助[Aspose.HTML 社区论坛](https://forum.aspose.com/).

## 常见问题

### 什么是 Aspose.HTML for .NET？
Aspose.HTML for .NET 是一个功能强大的库，使开发人员能够在 .NET 应用程序中处理 HTML、EPUB 和 XPS 文档。

### 我可以在哪里下载 Aspose.HTML for .NET？
您可以从[下载页面](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET 有免费试用版吗？
是的，你可以从[这里](https://releases.aspose.com/).

### 如何获取 Aspose.HTML for .NET 的临时许可证？
要获取临时许可证，请访问[临时执照页面](https://purchase.aspose.com/temporary-license/).

### 在哪里可以找到更多有关 Aspose.HTML for .NET 的教程和文档？
探索各种教程和详细文档[Aspose.HTML 文档](https://reference.aspose.com/html/net/)页。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
