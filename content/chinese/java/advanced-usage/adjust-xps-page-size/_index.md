---
title: 使用 Aspose.HTML for Java 调整 XPS 页面大小
linktitle: 调整 XPS 页面大小
second_title: 使用 Aspose.HTML 进行 Java HTML 处理
description: 了解如何使用 Aspose.HTML for Java 调整 XPS 页面大小。轻松控制 XPS 文档的输出尺寸。
type: docs
weight: 16
url: /zh/java/advanced-usage/adjust-xps-page-size/
---

在本教程中，我们将指导您完成使用 Aspose.HTML for Java 调整 XPS 页面大小的过程。这个功能强大的库允许您操作 HTML 文档并将其呈现为各种格式，包括 XPS。当您需要控制 XPS 文档的输出尺寸时，调整页面尺寸至关重要。

## 先决条件

在我们开始之前，请确保您具备以下先决条件：

1. Java 开发环境：确保您的系统上安装了 Java 开发工具包 (JDK)。

2.  Aspose.HTML for Java 库：您需要下载 Aspose.HTML for Java 库并将其包含在您的 Java 项目中。你可以找到图书馆[这里](https://releases.aspose.com/html/java/).

3. 输入 HTML 文件：准备要渲染的 HTML 文件并调整 XPS 页面大小。您可以在本教程中使用自己的 HTML 文件。

## 导入包

首先，您需要导入必要的包才能使用 Aspose.HTML for Java。在 Java 类的开头包含这些包：

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 第1步：设置输入文件名

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    //...
}
```

在此步骤中，我们使用`FileInputStream`.

## 第 2 步：创建 HTML 文档并设置样式

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

//...
```

此步骤涉及创建一个`HTMLDocument`并向其添加样式。

## 第 3 步：创建 XPS 渲染选项

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

在这里，我们创建 XPS 渲染选项来配置渲染过程。

## 步骤 4：调整页面大小

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

此步骤涉及设置页面大小并指定是否将其调整为最宽页面。

## 第 5 步：渲染输出

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

在最后一步中，我们使用配置的选项渲染 XPS 输出。

## 结论

在本教程中，我们向您展示了如何使用 Aspose.HTML for Java 调整 XPS 页面大小。您可以控制 XPS 文档的输出尺寸，确保它们满足您的特定要求。通过提供的代码和步骤，您可以在 Java 应用程序中轻松实现此功能。

如果您有任何疑问或需要进一步帮助，请随时访问[Aspose.HTML for Java 文档](https://reference.aspose.com/html/java/)或寻求帮助[Aspose论坛](https://forum.aspose.com/).

## 常见问题解答

### Q1：什么是 Java 版 Aspose.HTML？

A1：Aspose.HTML for Java 是一个 Java 库，允许开发人员操作 HTML 文档并将其转换为各种格式，例如 XPS、PDF 和图像。

### Q2：哪里可以下载 Aspose.HTML for Java？

 A2：您可以从以下位置下载 Aspose.HTML for Java 库：[这个链接](https://releases.aspose.com/html/java/).

### 问题 3：Aspose.HTML for Java 是否有免费试用版？

 A3：是的，您可以从以下位置获得 Aspose.HTML for Java 的免费试用版：[这里](https://releases.aspose.com/).

### Q4：如何获得 Aspose.HTML for Java 的临时许可证？

 A4：要获取 Aspose.HTML for Java 的临时许可证，请访问[这一页](https://purchase.aspose.com/temporary-license/).

### Q5：我可以获得 Aspose.HTML for Java 的支持吗？

 A5：是的，您可以向Aspose社区寻求帮助和支持[Aspose论坛](https://forum.aspose.com/).