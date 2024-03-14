---
title: 使用 Aspose.HTML 在 .NET 中创建文档
linktitle: 在 .NET 中创建文档
second_title: Aspose.HTML .NET HTML 操作 API
description: 释放 Aspose.HTML for .NET 的强大功能。学习轻松创建、操作和优化 HTML 和 SVG 文档。探索分步示例和常见问题解答。
type: docs
weight: 14
url: /zh/net/html-document-manipulation/creating-a-document/
---

在不断发展的网络开发世界中，保持领先地位至关重要。 Aspose.HTML for .NET 为开发人员提供了一个强大的工具包来处理 HTML 文档。无论您是从头开始、从文件加载、从 URL 提取还是处理 SVG 文档，该库都能提供您所需的多功能性。

在本分步指南中，我们将深入研究使用 Aspose.HTML for .NET 的基础知识，确保您有能力在 Web 开发项目中使用这个强大的工具。在深入了解细节之前，让我们先回顾一下开始您的旅程所需的先决条件和必要的命名空间。

## 先决条件

要成功学习本教程并利用 Aspose.HTML for .NET 的强大功能，您需要满足以下先决条件：

- 安装了 .NET Framework 或 .NET Core 的 Windows 计算机。
- 像 Visual Studio 这样的代码编辑器。
- C# 编程基础知识。

现在您已经具备了先决条件，让我们开始吧。

## 导入命名空间

在开始使用 Aspose.HTML for .NET 之前，您需要导入必要的命名空间。这些命名空间包含对于处理 HTML 文档至关重要的类和方法。以下是您应导入的命名空间列表：

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

导入这些命名空间后，您现在就可以深入研究分步示例了。

## 从头开始创建 HTML 文档

### 第 1 步：初始化一个空 HTML 文档

```csharp
//初始化一个空的 HTML 文档。
using (var document = new Aspose.Html.HTMLDocument())
{
    //创建文本元素并将其添加到文档中
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    //将文档保存到磁盘。
    document.Save("document.html");
}
```

在此示例中，我们首先创建一个空 HTML 文档并添加“Hello World!”给它发短信。然后我们将文档保存到文件中。

## 从文件创建 HTML 文档

### 第 1 步：准备“document.html”文件

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### 第 2 步：从“document.html”文件加载

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //将文档内容写入输出流。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

在这里，我们准备一个包含“Hello World!”的文件。内容，然后将其加载为 HTML 文档。我们将文档的内容打印到控制台。

## 从 URL 创建 HTML 文档

### 步骤 1：从网页加载文档

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    //将文档内容写入输出流。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

在此示例中，我们直接从网页加载 HTML 文档并显示其内容。

## 从字符串创建 HTML 文档

### 第 1 步：准备 HTML 代码

```csharp
var html_code = "<p>Hello World!</p>";
```

### 步骤 2：从字符串变量初始化文档

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    //将文档保存到磁盘。
    document.Save("document.html");
}
```

在这里，我们从字符串变量创建一个 HTML 文档并将其保存到文件中。

## 从 MemoryStream 创建 HTML 文档

### 第一步：创建内存流对象

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    //将 HTML 代码写入内存对象
    sw.Write("<p>Hello World!</p>");
    //将位置设置为开头
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    //从内存流初始化文档
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        //将文档保存到磁盘。
        document.Save("document.html");
    }
}
```

在此示例中，我们从内存流创建 HTML 文档并将其保存到文件中。

## 使用 SVG 文档

### 第 1 步：从字符串初始化 SVG 文档

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    //将文档内容写入输出流。
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

在这里，我们从字符串创建并显示 SVG 文档。

## 异步加载 HTML 文档

### 第 1 步：创建 HTML 文档实例

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### 第 2 步：订阅“ReadyStateChange”事件

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //检查“ReadyState”属性的值。
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### 步骤 3：在指定的 Uri 处异步导航

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

在此示例中，我们异步加载 HTML 文档并处理“ReadyStateChange”事件以在加载完成时显示内容。

## 处理“OnLoad”事件

### 第 1 步：创建 HTML 文档实例

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### 第 2 步：订阅“OnLoad”事件

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### 步骤 3：在指定的 Uri 处异步导航

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

此示例演示异步加载 HTML 文档并处理“OnLoad”事件以在完成后显示内容。

## 综上所述

在动态的 Web 开发世界中，拥有合适的工具至关重要。 Aspose.HTML for .NET 为您提供了高效创建、操作和处理 HTML 和 SVG 文档的方法。这份全面的指南引导您了解了基本知识，确保您可以在项目中利用 Aspose.HTML for .NET 的强大功能。

## 常见问题解答

### Q1：什么是 .NET 的 Aspose.HTML？

A1：Aspose.HTML for .NET 是一个功能强大的 .NET 库，使开发人员能够处理 HTML 和 SVG 文档。它提供了广泛的功能，从从头开始创建文档到解析和操作现有的 HTML 和 SVG 文件。

### 问题 2：我可以将 Aspose.HTML for .NET 与 .NET Core 一起使用吗？

A2：是的，Aspose.HTML for .NET 与 .NET Framework 和 .NET Core 兼容，使其成为现代 .NET 应用程序的多功能选择。

### Q3：Aspose.HTML for .NET 适合网页抓取和解析吗？

A3：当然！ Aspose.HTML for .NET 是网页抓取和解析任务的绝佳选择，因为它能够从 URL 和字符串加载 HTML 文档。您可以提取数据、执行分析等等。

### 问题 4：如何获得对 Aspose.HTML for .NET 的支持？

 A4：如果您在使用 Aspose.HTML for .NET 时遇到任何问题或有疑问，您可以访问[Aspose论坛](https://forum.aspose.com/)感谢社区和 Aspose 专家的支持和帮助。

### A5：在哪里可以找到详细的文档和下载选项？

A5：有关完整的文档和下载选项的访问，您可以参考以下链接：

- [文档](https://reference.aspose.com/html/net/)
- [下载](https://releases.aspose.com/html/net/)
- [买](https://purchase.aspose.com/buy)
- [免费试用](https://releases.aspose.com/)
- [临时牌照](https://purchase.aspose.com/temporary-license/)