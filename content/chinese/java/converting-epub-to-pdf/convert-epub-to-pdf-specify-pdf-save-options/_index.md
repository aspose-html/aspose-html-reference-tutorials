---
title: 指定 EPUB 到 PDF 的 PDF 保存选项
linktitle: 指定 EPUB 到 PDF 的 PDF 保存选项
second_title: 使用 Aspose.HTML 进行 Java HTML 处理
description: 了解如何使用强大的 HTML 操作库 Aspose.HTML 在 Java 中将 EPUB 转换为 PDF。
type: docs
weight: 12
url: /zh/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

## 介绍

Aspose.HTML for Java 是处理 HTML 和 EPUB 文档的强大工具。在本分步指南中，我们将引导您完成使用 Aspose.HTML for Java 将 EPUB 文件转换为 PDF 的过程。无论您是经验丰富的开发人员还是刚刚入门，本教程都将为您提供有效执行此任务所需的知识和技能。

## 先决条件

在我们开始之前，请确保您具备以下先决条件：

- Java 开发环境：您的系统上必须设置 Java 开发环境。

-  Aspose.HTML for Java：下载并安装 Aspose.HTML for Java 库。您可以在以下位置找到该库和相关文档[网站](https://releases.aspose.com/html/java/).

- EPUB 文件：您需要一个要转换为 PDF 的 EPUB 文件。

现在，让我们深入了解使用 Aspose.HTML for Java 将 EPUB 转换为 PDF 的分步指南。

## 第 1 步：打开 EPUB 文件

首先，打开现有的 EPUB 文件进行阅读。您可以使用`FileInputStream`为了达成这个。这是此步骤的代码：

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    //您后续步骤的代码将位于此处。
}
```

## 第 2 步：定义 PDF 保存选项

创建一个实例`PdfSaveOptions`具有自定义页面大小和背景颜色。您可以根据您的要求配置页面设置。您可以这样做：

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

## 步骤 3：将 EPUB 转换为 PDF

现在，请致电`ConvertEPUB`将 EPUB 文件转换为 PDF 的方法。指定输入流、PDF 保存选项和输出位置。其操作方法如下：

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

恭喜！您已使用 Aspose.HTML for Java 成功将 EPUB 文件转换为 PDF。您现在可以在指定的输出位置访问转换后的 PDF 文件。

## 完整的源代码
```java
Specifying PDF Save Options for EPUB to PDF
        //打开现有的 EPUB 文件进行阅读。
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            //使用自定义页面大小和背景颜色创建 PdfSaveOptions 的实例。
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            //调用ConvertEPUB方法将EPUB转换为PDF。
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## 结论

在本教程中，我们学习了如何使用 Aspose.HTML for Java 将 EPUB 文件转换为 PDF 格式。这个多功能库为开发人员提供了强大的文档操作工具。通过遵循本指南中概述的步骤，您可以将 EPUB 到 PDF 转换无缝集成到您的 Java 应用程序中。

## 常见问题 (FAQ)

### Aspose.HTML for Java 是免费的库吗？
 Aspose.HTML for Java 是一个商业库，但您可以从他们的网站获得免费试用版[网站](https://releases.aspose.com/).

### 支持转换哪些 EPUB 格式？
Aspose.HTML for Java支持各种EPUB格式的转换，确保与大多数EPUB文档的兼容性。

### 我可以进一步自定义 PDF 输出吗？
是的，您可以通过调整页面设置、背景颜色和其他设置来自定义 PDF 输出`PdfSaveOptions`.

### Aspose.HTML for Java 的试用版有任何限制吗？
试用版可能有一些限制，因此建议查看文档以了解详细信息。

### 在哪里可以获得 Aspose.HTML for Java 的支持？
您可以在以下位置找到问题的答案并寻求支持[Aspose.HTML 论坛](https://forum.aspose.com/).
