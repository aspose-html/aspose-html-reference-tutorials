---
title: 使用 Aspose.HTML 在 .NET 中应用计量许可证
linktitle: 在 .NET 中应用计量许可证
second_title: Aspose.HTML .NET HTML 操作 API
description: 了解如何在 Aspose.HTML for .NET 中应用计量许可证。高效管理您的 HTML 操作需求。立即开始！
weight: 10
url: /zh/net/licensing-and-initialization/apply-metered-license/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML 在 .NET 中应用计量许可证

在本教程中，我们将指导您使用 Aspose.HTML 在 .NET 应用程序中应用计量许可证的过程。计量许可证是一种管理 HTML 操作需求许可的便捷方式。通过遵循以下步骤，您将能够将计量许可证应用于您的 Aspose.HTML for .NET 项目。

## 先决条件

继续操作之前，请确保已满足以下先决条件：

- 有效的 Aspose.HTML for .NET 许可证。您可以从以下位置获取[Aspose 购买](https://purchase.aspose.com/buy).
- Aspose.HTML for .NET 库，您可以从以下网址下载[这里](https://releases.aspose.com/html/net/).
- 存储输入 HTML 文件的数据目录路径。

现在，让我们分解示例代码并详细解释每个步骤：

## 导入命名空间

在您的 .NET 项目中，您需要包含必要的命名空间。在 C# 文件顶部添加以下 using 语句：

```csharp
using Aspose.Html;
```

## 逐步指南

在这里，我们将示例代码分解为多个步骤，并详细解释每个步骤。

### 设置数据目录路径：

   首先，你应该设置输入 HTML 文件所在的数据目录的路径。你需要替换`"Your Data Directory"`与实际路径。

   ```csharp
   string dataDir = "Your Data Directory";
   ```

### 设置计量公钥和私钥：

   要应用计量许可证，您需要提供公钥和私钥。您可以在从 Aspose 购买计量许可证时获得这些密钥。替换`"*****"`使用您的实际公钥和私钥。

   ```csharp
   Aspose.Html.Metered metered = new Aspose.Html.Metered();
   metered.SetMeteredKey("YOUR_PUBLIC_KEY", "YOUR_PRIVATE_KEY");
   ```

### 加载 HTML 文档：

   使用 HTMLDocument 类从数据目录加载 HTML 文档。确保替换`"input.html"`使用实际的文件名。

   ```csharp
   HTMLDocument document = new HTMLDocument(dataDir + "input.html");
   ```

### 打印内部 HTML：

   加载HTML文档后，您可以访问并将文件内部的HTML打印到控制台进行验证。

   ```csharp
   Console.WriteLine(document.Body.InnerHTML);
   ```

就这样！您已成功将计量许可证应用于 .NET 项目并加载 HTML 文档。

## 结论

在本教程中，我们演示了如何使用 Aspose.HTML for .NET 应用计量许可证。通过遵循这些步骤，您可以将 Aspose.HTML 无缝集成到您的 .NET 应用程序中以进行 HTML 操作。

---

## 常见问题 (FAQ)

### Aspose.HTML for .NET 中的计量许可证是什么？
计量许可允许您根据使用情况按现收现付的方式为 Aspose.HTML 付费。这是一种灵活的许可选项。

### 我可以在哪里获得 Aspose.HTML for .NET 的计量许可证？
您可以从购买计量许可证[Aspose 购买](https://purchase.aspose.com/buy).

### 如何下载 Aspose.HTML for .NET 库？
您可以从[这里](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET 是否有免费试用选项？
是的，你可以从[这里](https://releases.aspose.com/).

### 在哪里可以获得支持或者询问有关 Aspose.HTML for .NET 的问题？
您可以加入社区并寻求支持[Aspose 论坛](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
