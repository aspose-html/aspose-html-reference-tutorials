---
title: 使用 Aspose.HTML 在 .NET 中进行 Web 抓取
linktitle: .NET 中的 Web 抓取
second_title: Aspose.HTML .NET HTML 操作 API
description: 学习使用 Aspose.HTML 在 .NET 中操作 HTML 文档。有效地导航、过滤、查询和选择元素，以增强 Web 开发。
type: docs
weight: 13
url: /zh/net/advanced-features/web-scraping/
---

在当今的数字时代，操作和提取 HTML 文档中的信息是开发人员的常见任务。Aspose.HTML for .NET 是一款功能强大的工具，可简化 .NET 应用程序中的 HTML 处理和操作。在本教程中，我们将探索 Aspose.HTML for .NET 的各个方面，包括先决条件、命名空间和分步示例，以帮助您充分利用其潜力。

## 先决条件

在深入了解 Aspose.HTML for .NET 的世界之前，您需要满足一些先决条件：

1. 开发环境：确保您已使用 Visual Studio 或任何其他兼容 .NET 开发的 IDE 设置了可用的开发环境。

2.  Aspose.HTML for .NET：从以下位置下载并安装 Aspose.HTML for .NET 库[下载链接](https://releases.aspose.com/html/net/)。您可以根据需要选择免费试用版或许可版。

3. HTML 基础知识：熟悉 HTML 结构和元素对于有效使用 Aspose.HTML for .NET 至关重要。

## 导入命名空间

首先，您需要在 C# 项目中导入必要的命名空间。这些命名空间提供对 Aspose.HTML for .NET 类和功能的访问：

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

在满足先决条件并导入命名空间的情况下，让我们逐步分解一些关键示例，以说明如何有效地使用 Aspose.HTML for .NET。

## 通过 HTML 导航

在此示例中，我们将浏览 HTML 文档并逐步访问其元素。

```csharp
public static void NavigateThroughHTML()
{
    //准备 HTML 代码
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    //从准备好的代码初始化文档
    using (var document = new HTMLDocument(html_code, "."))
    {
        //获取对 BODY 的第一个子项（第一个 SPAN）的引用
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); //输出：Hello

        //获取对 HTML 元素之间空白的引用
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); //输出： ' '

        //获取对第二个 SPAN 元素的引用
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); //输出：世界！
    }
}
```

在这个例子中，我们创建一个 HTML 文档，访问它的第一个子文档（a`SPAN`元素）、元素之间的空白，以及第二个`SPAN`元素，演示基本导航。

## 使用节点过滤器

节点过滤器允许您有选择地处理 HTML 文档中的特定元素。

```csharp
public static void NodeFilterUsageExample()
{
    //准备 HTML 代码
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    //根据准备好的代码初始化文档
    using (var document = new HTMLDocument(code, "."))
    {
        //使用自定义图像元素过滤器创建 TreeWalker
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                //输出：image1.png
                //输出：image2.png
            }
        }
    }
}
```

此示例演示如何使用自定义节点过滤器提取特定元素（在本例中为`IMG`HTML 文档中包含元素的集合。

## XPath 查询

XPath 查询使您能够根据特定条件搜索 HTML 文档中的元素。

```csharp
public static void XPathQueryUsageExample()
{
    //准备 HTML 代码
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    //根据准备好的代码初始化文档
    using (var document = new HTMLDocument(code, "."))
    {
        //评估 XPath 表达式以选择特定元素
        var result = document.Evaluate("//*[@class='happy']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        //迭代结果节点
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            //输出：Hello
            //输出：世界！
        }
    }
}
```

此示例展示了如何使用 XPath 查询根据元素的属性和结构来定位 HTML 文档中的元素。

## CSS 选择器

CSS 选择器提供了一种在 HTML 文档中选择元素的另一种方法，类似于 CSS 样式表定位元素的方式。

```csharp
public static void CSSSelectorUsageExample()
{
    //准备 HTML 代码
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    //根据准备好的代码初始化文档
    using (var document = new HTMLDocument(code, "."))
    {
        //使用 CSS 选择器根据类和层次结构提取元素
        var elements = document.QuerySelectorAll(".happy span");
        
        //迭代结果元素列表
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            //输出：Hello
            //输出：世界！
        }
    }
}
```

在这里，我们演示如何使用 CSS 选择器来定位 HTML 文档中的特定元素。

通过这些示例，您将对如何使用 Aspose.HTML for .NET 导航、过滤、查询和选择 HTML 文档中的元素有一个基本的了解。

## 结论

 Aspose.HTML for .NET 是一个多功能库，可帮助 .NET 开发人员高效处理 HTML 文档。借助其强大的导航、过滤、查询和选择元素功能，您可以无缝处理各种 HTML 处理任务。通过遵循本教程并浏览以下文档[Aspose.HTML for .NET 文档](https://reference.aspose.com/html/net/)，您可以充分发挥此工具在 .NET 应用程序中的潜力。

## 常见问题解答

### Q1. Aspose.HTML for .NET 可以免费使用吗？

A1：Aspose.HTML for .NET 提供免费试用版，但若要用于生产，则需要购买许可证。您可以在以下位置找到许可详细信息和选项[Aspose.HTML 购买](https://purchase.aspose.com/buy).

### Q2. 如何获取 Aspose.HTML for .NET 的临时许可证？

 A2：您可以从以下网站获取用于测试目的的临时许可证[Aspose.HTML 临时许可证](https://purchase.aspose.com/temporary-license/).

### Q3. 我可以在哪里寻求有关 Aspose.HTML for .NET 的帮助或支持？

 A3：如果您遇到任何问题或有疑问，您可以访问[Aspose.HTML 论坛](https://forum.aspose.com/)寻求援助和社区支持。

### Q4. 有没有其他资源可以用于学习 Aspose.HTML for .NET？

 A4：除了本教程之外，您还可以探索[Aspose.HTML for .NET 文档页面](https://reference.aspose.com/html/net/).

### Q5. Aspose.HTML for .NET 与最新的 .NET 版本兼容吗？

A5：Aspose.HTML for .NET 会定期更新以确保与最新的 .NET 版本和技术兼容。