---
title: 使用 Aspose.HTML 将 EPUB 转换为 .NET 中的 XPS
linktitle: 在 .NET 中将 EPUB 转换为 XPS
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何使用 Aspose.HTML for .NET 将 EPUB 转换为 .NET 中的 XPS。按照我们的分步指南轻松进行转换。
type: docs
weight: 13
url: /zh/net/html-extensions-and-conversions/convert-epub-to-xps/
---

您是否正在寻找一种在 .NET 应用程序中将 EPUB 文件转换为 XPS 格式的无缝方法？ Aspose.HTML for .NET 提供了一个强大的解决方案来轻松实现这一目标。在本分步指南中，我们将引导您完成使用 Aspose.HTML 将 EPUB 转换为 XPS 的过程。让我们开始吧！

## 先决条件

在开始 EPUB 到 XPS 转换过程之前，您需要确保满足以下先决条件：

### 1.Aspose.HTML for .NET 库

确保您的项目中安装了 Aspose.HTML for .NET 库。如果您还没有这样做，您可以从[Aspose.HTML for .NET 下载页面](https://releases.aspose.com/html/net/).

### 2.输入EPUB文件

您需要一个要转换为 XPS 的 EPUB 文件。确保您有可用于转换的 EPUB 文件。

### 3..NET开发环境

本指南假设您的计算机上设置了有效的 .NET 开发环境。

## 导入命名空间

首先，您应该为 Aspose.HTML 导入必要的命名空间：

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## 将 EPUB 转换为 XPS

让我们将 EPUB 文件转换为 XPS 格式的过程分解为多个步骤。

### 步骤1.1：打开EPUB文件

首先，使用 FileStream 打开现有的 EPUB 文件进行读取：

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    //继续转换过程
}
```

### 步骤1.2：创建XpsSaveOptions

创建 XpsSaveOptions 的实例。此步骤对于配置 XPS 输出至关重要：

```csharp
var options = new XpsSaveOptions();
```

### 步骤1.3：将 EPUB 转换为 XPS

现在，我们调用 ConvertEPUB 方法将 EPUB 转换为 XPS：

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## 指定自定义 XPS 选项

您可以通过指定页面大小和背景颜色等自定义选项来进一步自定义 XPS 输出。

### 步骤2.1：自定义页面尺寸和背景颜色

创建具有自定义页面大小和背景颜色的 XpsSaveOptions 实例：

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

现在，调用 ConvertEPUB 方法，使用自定义选项将 EPUB 转换为 XPS：

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## 使用自定义流提供程序

在此步骤中，我们将使用自定义流提供程序将 EPUB 转换为 XPS，从而允许您操作结果数据。

### 步骤3.1：创建MemoryStreamProvider

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

检索包含转换后的数据的内存流并将其保存到输出文件：

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### 类 MemoryStreamProvider 源代码

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
恭喜！您已使用 Aspose.HTML for .NET 成功将 EPUB 文件转换为 XPS 格式。

## 结论

在这个综合教程中，我们探索了如何利用 Aspose.HTML for .NET 通过各种自定义选项将 EPUB 文件转换为 XPS 格式。无论您是经验丰富的开发人员还是新手，Aspose.HTML 都可以简化流程，让您轻松处理 EPUB 到 XPS 的转换。

有任何疑问或遇到问题吗？查看[Aspose.HTML 文档](https://reference.aspose.com/html/net/)获取更多见解或寻求帮助[Aspose.HTML 社区论坛](https://forum.aspose.com/).

## 经常问的问题

### 什么是 .NET 的 Aspose.HTML？
Aspose.HTML for .NET 是一个功能强大的库，使开发人员能够在 .NET 应用程序中使用 HTML、EPUB 和 XPS 文档。

### 在哪里可以下载 Aspose.HTML for .NET？
您可以从以下位置下载 Aspose.HTML for .NET[下载页面](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET 是否有免费试用版？
是的，您可以从以下位置获得免费试用[这里](https://releases.aspose.com/).

### 如何获得 Aspose.HTML for .NET 的临时许可证？
要获得临时许可证，请访问[临时许可证页面](https://purchase.aspose.com/temporary-license/).

### 在哪里可以找到有关 Aspose.HTML for .NET 的更多教程和文档？
探索有关的各种教程和详细文档[Aspose.HTML 文档](https://reference.aspose.com/html/net/)页。