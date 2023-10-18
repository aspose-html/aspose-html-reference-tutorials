---
title: 使用 Aspose.HTML 在 .NET 中保存文档
linktitle: 在 .NET 中保存文档
second_title: Aspose.HTML .NET HTML 操作 API
description: 通过我们的分步指南释放 Aspose.HTML for .NET 的强大功能。学习创建、操作和转换 HTML 和 SVG 文档
type: docs
weight: 16
url: /zh/net/html-document-manipulation/saving-a-document/
---

在当今的数字时代，创建和操作 HTML 和 SVG 文档对于许多软件开发人员和企业来说至关重要。 Aspose.HTML for .NET 是一个功能强大的库，可以简化这些任务，提供各种功能来处理 HTML、SVG 等。在这份综合指南中，我们将深入探讨 Aspose.HTML for .NET 的基本知识，并将每个示例分解为易于遵循的步骤。无论您是经验丰富的开发人员还是刚刚入门，您都会发现本指南对于利用 Aspose.HTML 的功能非常有价值。

## 先决条件

在我们踏上这段旅程之前，让我们确保您拥有所需的一切：

- 开发环境：确保您的计算机上安装了 Visual Studio 或任何其他 .NET 开发环境。

- Aspose.HTML for .NET：您需要获取Aspose.HTML for .NET 库。您可以从以下位置下载：[这里](https://releases.aspose.com/html/net/).

- C# 知识：熟悉 C# 编程语言是有益的，但不是强制性的。本指南旨在适合初学者。

## 导入命名空间

要开始使用 Aspose.HTML for .NET，您需要将必要的命名空间导入到您的项目中。在您的 C# 代码中，包含以下命名空间：

### 第1步：导入Aspose.HTML命名空间
```csharp
using Aspose.Html;
```

此命名空间将授予您访问各种 HTML 和 SVG 操作功能的权限。

## HTML 到文件

### 第 1 步：初始化一个空 HTML 文档
```csharp
//初始化一个空的 HTML 文档。
using (var document = new Aspose.Html.HTMLDocument())
{
    //创建文本元素并将其添加到文档中
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    //将 HTML 保存到磁盘上的文件中。
    document.Save("document.html");
}
```

在此示例中，我们创建一个 HTML 文档并添加一个简单的“Hello World!”给它发短信。然后我们将 HTML 保存到磁盘上的文件中。

## 没有链接文件的 HTML

### 第 1 步：准备一个简单的 HTML 文件
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

在这里，我们创建一个基本的 HTML 文件，其中包含指向另一个文件的锚链接。

### 第 2 步：将“document.html”加载到内存中
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //创建保存选项实例
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //将最大处理深度设置为 0 以切断链接的 HTML 文件。
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    //保存文档
    document.Save(@".\html-to-file-example\document.html", options);
}
```

在此示例中，我们将 HTML 文档加载到内存中，设置最大处理深度以切断链接文件，然后保存文档。 

## HTML 到 MHTML

### 第 1 步：准备一个简单的 HTML 文件
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

就像示例 2 中一样，我们创建一个基本 HTML 文件，其中包含指向另一个文件的锚链接。

### 第 2 步：将“document.html”加载到内存中并另存为 MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //将文档另存为 MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

在这里，我们将 HTML 文档加载到内存中并以 MHTML 格式保存。

## HTML 到 Markdown

### 第 1 步：准备 HTML 代码
```csharp
var html_code = "<H2>Hello World!</H2>";
```

在此步骤中，我们定义一个 HTML 代码片段，其中包含`<H2>`元素。

### 第 2 步：从 HTML 代码初始化文档并另存为 Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    //将文档另存为 Markdown 文件。
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

我们从代码片段创建一个 HTML 文档并将其保存为 Markdown 文件。

## SVG 到文件

### 第 1 步：准备 SVG 代码
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' 高度='80' 宽度='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

在这里，我们创建了一个 SVG 代码来绘制一个简单的彩色图形。

### 步骤 2：从代码初始化 SVG 文档并保存到磁盘
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    //将 SVG 文件保存到磁盘
    document.Save("document.svg");
}
```

在此步骤中，我们从代码创建一个 SVG 文档并将其保存为 SVG 文件。

## 结论

Aspose.HTML for .NET 是一个多功能库，可简化 .NET 应用程序中的 HTML 和 SVG 文档处理。在本指南中，我们介绍了五个基本示例，并将每个示例分解为分步说明。无论您是创建、操作还是转换文档，Aspose.HTML 都能满足您的需求。通过执行这些步骤，您就可以很好地掌握这个强大的工具。

## 常见问题解答

### Q1：什么是 .NET 的 Aspose.HTML？

A1：Aspose.HTML for .NET 是一个 .NET 库，它提供了处理 HTML 和 SVG 文档的广泛功能，包括创建、操作和转换。

### Q2：哪里可以下载 Aspose.HTML for .NET？

 A2：您可以从以下位置下载 Aspose.HTML for .NET[这里](https://releases.aspose.com/html/net/).

### Q3：Aspose.HTML for .NET 适合初学者吗？

A3：是的，Aspose.HTML for .NET 可供初学者和经验丰富的开发人员使用。本指南中的示例旨在适合初学者。

### Q4：我可以使用 Aspose.HTML for .NET 将 HTML 转换为其他格式吗？

A4：是的，Aspose.HTML for .NET 支持转换为各种格式，包括 MHTML 和 Markdown，如示例所示。

### 问题 5：在哪里可以获得 Aspose.HTML for .NET 的支持？

 A5：您可以在 Aspose.HTML 社区论坛中找到问题的支持和答案[这里](https://forum.aspose.com/).