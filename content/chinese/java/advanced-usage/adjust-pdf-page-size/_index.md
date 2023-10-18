---
title: 使用 Aspose.HTML for Java 调整 PDF 页面大小
linktitle: 调整 PDF 页面大小
second_title: 使用 Aspose.HTML 进行 Java HTML 处理
description: 了解如何使用 Aspose.HTML for Java 调整 PDF 页面大小。轻松从 HTML 创建高质量的 PDF。有效控制页面尺寸。
type: docs
weight: 15
url: /zh/java/advanced-usage/adjust-pdf-page-size/
---

在当今的数字时代，从 HTML 内容生成高质量 PDF 的需求不断增加。 Aspose.HTML for Java 是一个功能强大的 Java 库，可让您轻松地将 HTML 文档转换为 PDF 格式。在本教程中，我们将重点介绍使用 Aspose.HTML for Java 将 HTML 转换为 PDF 时调整页面大小。

## 先决条件

在开始之前，请确保您具备以下先决条件：

- Java 开发环境：确保您的系统上安装了 Java 开发工具包 (JDK)。
-  Aspose.HTML for Java：您需要从网站下载并安装Aspose.HTML for Java[这里](https://releases.aspose.com/html/java/).
- HTML 文档：您应该有一个可供转换的 HTML 文档。如果没有，请创建一个或使用现有的 HTML 文件。

## 导入包

首先，您需要导入必要的包才能使用 Aspose.HTML for Java。以下代码片段演示了如何执行此操作：

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

现在您已经具备了先决条件并导入了必要的包，让我们将调整 PDF 页面大小的过程分解为多个步骤：

## 第 1 步：读取 HTML 内容

首先，您需要阅读要转换为 PDF 的 HTML 内容。在此示例中，我们将从名为“FirstFile.html”的文件中读取 HTML。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## 第 2 步：编写 HTML 内容

接下来，您将 HTML 内容写入名为“FirstFileOut.html”的文件。

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    //在此处添加自定义 HTML 样式或内容
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## 第 3 步：将 HTML 渲染为 PDF

现在，您将把 HTML 内容呈现为 PDF 文件。我们将介绍两种场景：一种是页面大小未根据内容宽度进行调整，另一种是进行调整。

### 页面尺寸未调整

在这种情况下，页面大小设置为固定的宽度和高度，如果超过这些尺寸，可能会裁剪内容。

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

//从 HTML 文件创建 HTMLDocument 实例
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

//设置 PDF 渲染选项
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//渲染输出
pdf_renderer.render(device, html_document);
```

### 根据内容宽度调整页面大小

在这种情况下，页面大小会根据内容宽度进行调整。

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//渲染输出
pdf_renderer.render(device, html_document);
```

## 结论

在本教程中，我们探讨了如何使用 Aspose.HTML for Java 将 HTML 转换为 PDF 时调整 PDF 页面大小。您已经了解了先决条件，导入了所需的包，并按照分步指南完成了此任务。使用 Aspose.HTML for Java，您可以轻松控制生成的 PDF 的页面大小，确保您的内容按预期显示。

请随意尝试不同的页面大小和设置，以满足您的特定要求。如果您遇到任何问题或有其他疑问，请随时寻求帮助[Aspose.HTML for Java 文档](https://reference.aspose.com/html/java/)或者[Aspose 支持论坛](https://forum.aspose.com/).

## 常见问题解答

### Q1：什么是 Java 版 Aspose.HTML？

A1：Aspose.HTML for Java 是一个 Java 库，允许您处理 HTML 文档、操作、转换并将其呈现为各种格式，包括 PDF。

### Q2: 使用 Aspose.HTML for Java 将 HTML 转换为 PDF 时如何调整 PDF 页面大小？

 A2：您可以使用`PageSetup`类并设置`AdjustToWidestPage`财产给`true`或“假”，具体取决于您的要求。

### 问题 3：在将 HTML 内容转换为 PDF 之前，我可以自定义其样式吗？

A3：是的，您可以通过在将 HTML 内容转换为 PDF 之前添加 CSS 和 HTML 元素来自定义样式，如教程中所示。

### Q4：在哪里可以找到 Aspose.HTML for Java 的文档？

 A4：可以参考文档[这里](https://reference.aspose.com/html/java/)获取全面的信息和示例。

### Q5：Aspose.HTML for Java 有免费试用版吗？

 A5：是的，您可以访问 Aspose.HTML for Java 的免费试用版：[这个链接](https://releases.aspose.com/).