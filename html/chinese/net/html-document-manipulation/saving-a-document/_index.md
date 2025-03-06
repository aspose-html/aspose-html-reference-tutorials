---
title: 使用 Aspose.HTML 在 .NET 中保存文档
linktitle: 在 .NET 中保存文档
second_title: Aspose.HTML .NET HTML 操作 API
description: 通过我们的分步指南解锁 Aspose.HTML for .NET 的强大功能。学习创建、操作和转换 HTML 和 SVG 文档
weight: 16
url: /zh/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML 在 .NET 中保存文档


在当今的数字时代，创建和操作 HTML 和 SVG 文档对于许多软件开发人员和企业来说都是必不可少的。Aspose.HTML for .NET 是一个功能强大的库，可以简化这些任务，提供各种功能来处理 HTML、SVG 等。在本综合指南中，我们将深入探讨 Aspose.HTML for .NET 的基本知识，将每个示例分解为易于遵循的步骤。无论您是经验丰富的开发人员还是刚刚起步，您都会发现本指南对于利用 Aspose.HTML 的功能非常有用。

## 先决条件

在我们踏上这一旅程之前，请确保您已准备好所需的一切：

- 开发环境：确保您的计算机上安装了 Visual Studio 或任何其他 .NET 开发环境。

- Aspose.HTML for .NET：您需要获取 Aspose.HTML for .NET 库。您可以从以下位置下载[这里](https://releases.aspose.com/html/net/).

- 熟悉 C#：熟悉 C# 编程语言是有益的，但不是强制性的。本指南旨在方便初学者使用。

## 导入命名空间

要开始使用 Aspose.HTML for .NET，您需要将必要的命名空间导入到您的项目中。在您的 C# 代码中，包括以下命名空间：

### 步骤 1：导入 Aspose.HTML 命名空间
```csharp
using Aspose.Html;
```

该命名空间将授予您访问各种 HTML 和 SVG 操作功能的权限。

## HTML 到文件

### 步骤 1：初始化一个空的 HTML 文档
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

在此示例中，我们创建一个 HTML 文档并向其中添加一个简单的“Hello World！”文本。然后我们将 HTML 保存到磁盘上的文件中。

## 无链接文件的 HTML

### 步骤 1：准备一个简单的 HTML 文件
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

在这里，我们创建一个带有指向另一个文件的锚链接的基本 HTML 文件。

### 步骤 2：将 document.html 加载到内存中
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //创建保存选项实例
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //将最大处理深度设置为 0，以切断链接的 HTML 文件。
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    //保存文档
    document.Save(@".\html-to-file-example\document.html", options);
}
```

在此示例中，我们将一个 HTML 文档加载到内存中，设置最大处理深度以切断链接文件，并保存该文档。 

## HTML 到 MHTML

### 步骤 1：准备一个简单的 HTML 文件
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

就像示例 2 一样，我们创建一个带有指向另一个文件的锚链接的基本 HTML 文件。

### 步骤 2：将“document.html”加载到内存并保存为 MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    //将文档另存为 MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

在这里，我们将 HTML 文档加载到内存中并以 MHTML 格式保存。

## HTML 到 Markdown

### 步骤 1：准备 HTML 代码
```csharp
var html_code = "<H2>Hello World!</H2>";
```

在此步骤中，我们定义一个 HTML 代码片段，其中包含`<H2>`元素。

### 步骤 2：从 HTML 代码初始化文档并另存为 Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    //将文档保存为 Markdown 文件。
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

我们从代码片段创建一个 HTML 文档并将其保存为 Markdown 文件。

## SVG 到文件

### 步骤 1：准备 SVG 代码
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

在这里，我们创建一个绘制简单、彩色图形的 SVG 代码。

### 第 2 步：从代码初始化 SVG 文档并保存到磁盘
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    //将 SVG 文件保存到磁盘
    document.Save("document.svg");
}
```

在此步骤中，我们从代码创建一个 SVG 文档并将其保存为 SVG 文件。

## 结论

Aspose.HTML for .NET 是一个多功能库，可简化 .NET 应用程序中的 HTML 和 SVG 文档处理。在本指南中，我们介绍了五个基本示例，并将每个示例分解为分步说明。无论您是创建、操作还是转换文档，Aspose.HTML 都能满足您的需求。通过遵循这些步骤，您就可以很好地掌握这个强大的工具。

## 常见问题解答

### 问题1:什么是Aspose.HTML for .NET？

A1：Aspose.HTML for .NET 是一个 .NET 库，它提供了处理 HTML 和 SVG 文档的广泛功能，包括创建、操作和转换。

### 问题2：我可以在哪里下载 Aspose.HTML for .NET？

 A2：您可以从以下位置下载 Aspose.HTML for .NET[这里](https://releases.aspose.com/html/net/).

### Q3: Aspose.HTML for .NET 适合初学者吗？

A3：是的，Aspose.HTML for .NET 可供初学者和经验丰富的开发人员使用。本指南中的示例旨在方便初学者使用。

### 问题4：我可以使用 Aspose.HTML for .NET 将 HTML 转换为其他格式吗？

A4：是的，Aspose.HTML for .NET 支持转换为各种格式，包括 MHTML 和 Markdown，如示例所示。

### Q5：在哪里可以获得 Aspose.HTML for .NET 的支持？

 A5：您可以在 Aspose.HTML 社区论坛中找到支持和问题的答案[这里](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
