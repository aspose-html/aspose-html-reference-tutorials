---
title: 使用 Aspose.HTML 在 .NET 中应用计量许可证
linktitle: 在 .NET 中应用计量许可证
second_title: Aspose.Slides .NET HTML 操作 API
description: 了解如何在 Aspose.HTML for .NET 中应用计量许可证。有效管理您的 HTML 操作需求。现在就开始！
type: docs
weight: 10
url: /zh/net/licensing-and-initialization/apply-metered-license/
---
在本教程中，我们将指导您完成使用 Aspose.HTML 在 .NET 应用程序中应用计量许可证的过程。计量许可证是一种管理您的 HTML 操作需求的许可的便捷方法。通过执行以下步骤，您将能够将计量许可证应用于您的 Aspose.HTML for .NET 项目。

## 先决条件

在继续之前，请确保满足以下先决条件：

- 有效的 Aspose.HTML for .NET 许可证。您可以从以下位置获取它：[提出购买](https://purchase.aspose.com/buy).
-  Aspose.HTML for .NET 库，您可以从以下位置下载[这里](https://releases.aspose.com/html/net/).
- 存储输入 HTML 文件的数据目录路径。

现在，让我们分解示例代码并详细解释每个步骤：

## 导入命名空间

在您的 .NET 项目中，您需要包含必要的命名空间。在 C# 文件顶部添加以下 using 语句：

```csharp
using Aspose.Html;
```

## 分步指南

在这里，我们将示例代码分解为多个步骤，并详细解释每个步骤。

### 设置数据目录路径：

   首先，您应该设置输入 HTML 文件所在的数据目录的路径。您需要更换`"Your Data Directory"`与实际路径。

   ```csharp
   string dataDir = "Your Data Directory";
   ```

### 设置计量公钥和私钥：

   要申请计量许可证，您需要提供您的公钥和私钥。当您从 Aspose 购买计量许可证时，您可以获得这些密钥。代替`"*****"`使用您实际的公钥和私钥。

   ```csharp
   Aspose.Html.Metered metered = new Aspose.Html.Metered();
   metered.SetMeteredKey("YOUR_PUBLIC_KEY", "YOUR_PRIVATE_KEY");
   ```

### 加载 HTML 文档：

   使用 HTMLDocument 类从数据目录加载 HTML 文档。确保更换`"input.html"`与实际的文件名。

   ```csharp
   HTMLDocument document = new HTMLDocument(dataDir + "input.html");
   ```

### 打印内部 HTML：

   加载HTML文档后，您可以访问文件内部的HTML并将其打印到控制台进行验证。

   ```csharp
   Console.WriteLine(document.Body.InnerHTML);
   ```

就是这样！您已成功将计量许可证应用到 .NET 项目并加载了 HTML 文档。

## 结论

在本教程中，我们演示了如何使用 Aspose.HTML for .NET 应用计量许可证。通过执行以下步骤，您可以将 Aspose.HTML 无缝集成到 .NET 应用程序中以进行 HTML 操作。

---

## 常见问题 (FAQ)

### 什么是 Aspose.HTML for .NET 中的计量许可证？
计量许可证允许您根据您的使用情况按即用即付的方式支付 Aspose.HTML 费用。这是一种灵活的许可选项。

### 在哪里可以获得 Aspose.HTML for .NET 的计量许可证？
您可以从以下位置购买计量许可证[提出购买](https://purchase.aspose.com/buy).

### 如何下载 Aspose.HTML for .NET 库？
您可以从以下位置下载该库[这里](https://releases.aspose.com/html/net/).

### Aspose.HTML for .NET 是否有免费试用选项？
是的，您可以从以下位置获取免费试用版[这里](https://releases.aspose.com/).

### 我在哪里可以获得有关 Aspose.HTML for .NET 的支持或提出问题？
您可以加入社区并寻求支持[Aspose 论坛](https://forum.aspose.com/).