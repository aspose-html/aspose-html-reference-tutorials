---
title: 使用 Aspose.HTML for Java 调整 XPS 页面大小
linktitle: 调整 XPS 页面大小
second_title: 使用 Aspose.HTML 进行 Java HTML 处理
description: 了解如何使用 Aspose.HTML for Java 调整 XPS 页面大小。轻松控制 XPS 文档的输出尺寸。
weight: 16
url: /zh/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML for Java 调整 XPS 页面大小


在本教程中，我们将指导您使用 Aspose.HTML for Java 调整 XPS 页面大小的过程。这个功能强大的库允许您操作 HTML 文档并将其呈现为各种格式，包括 XPS。当您需要控制 XPS 文档的输出尺寸时，调整页面大小至关重要。

## 先决条件

在开始之前，请确保您已满足以下先决条件：

1. Java 开发环境：确保您的系统上安装了 Java 开发工具包 (JDK)。

2.  Aspose.HTML for Java 库：您需要下载 Aspose.HTML for Java 库并将其包含在 Java 项目中。您可以找到库[这里](https://releases.aspose.com/html/java/).

3. 输入 HTML 文件：准备要渲染并调整 XPS 页面大小的 HTML 文件。在本教程中，您可以使用自己的 HTML 文件。

## 导入包

首先，您需要导入使用 Aspose.HTML for Java 所需的包。在 Java 类的开头包含这些包：

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## 步骤 1：设置输入文件名

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

此步骤涉及创建一个`HTMLDocument`并添加样式。

## 步骤 3：创建 XPS 渲染选项

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

这一步涉及设置页面大小并指定是否将其调整为最宽的页面。

## 步骤 5：渲染输出

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

在最后一步，我们使用配置的选项呈现 XPS 输出。

## 结论

在本教程中，我们向您展示了如何使用 Aspose.HTML for Java 调整 XPS 页面大小。您可以控制 XPS 文档的输出尺寸，确保它们满足您的特定要求。使用提供的代码和步骤，您可以轻松地在 Java 应用程序中实现此功能。

如果您有任何疑问或需要进一步的帮助，请随时访问[Aspose.HTML for Java 文档](https://reference.aspose.com/html/java/)或寻求帮助[Aspose 论坛](https://forum.aspose.com/).

## 常见问题解答

### 问题1:什么是 Aspose.HTML for Java？

A1：Aspose.HTML for Java 是一个 Java 库，允许开发人员操作和转换 HTML 文档为各种格式，例如 XPS、PDF 和图像。

### 问题2：我可以在哪里下载 Aspose.HTML for Java？

 A2: 您可以从以下位置下载 Aspose.HTML for Java 库[此链接](https://releases.aspose.com/html/java/).

### 问题3：Aspose.HTML for Java 有免费试用版吗？

 A3：是的，您可以从以下网站免费试用 Aspose.HTML for Java[这里](https://releases.aspose.com/).

### Q4: 如何获取 Aspose.HTML for Java 的临时许可证？

 A4: 要获取 Aspose.HTML for Java 的临时许可证，请访问[本页](https://purchase.aspose.com/temporary-license/).

### 问题5：我可以获得 Aspose.HTML for Java 的支持吗？

 A5：是的，您可以在 Aspose 社区上寻求帮助和支持[Aspose 论坛](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
