---
date: 2026-01-02
description: 了解如何在 Java 中使用 Aspose.HTML 将 EPUB 转换为 PDF，同时设置自定义 PDF 页面大小和其他 PDF 保存选项。
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 自定义 PDF 页面尺寸：为 EPUB 转 PDF 指定 PDF 保存选项
url: /zh/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 自定义 PDF 页面尺寸：为 EPUB 转 PDF 指定 PDF 保存选项

## 介绍

Aspose.HTML for Java 可轻松实现 **EPUB 转 PDF**，并让您全面控制输出，包括设置 **自定义 PDF 页面尺寸**。在本分步指南中，我们将从环境准备到微调 `PdfSaveOptions`，确保生成的 PDF 与您所需的页面尺寸完全匹配。无论您是在构建出版流水线、电子学习平台，还是仅需自动化文档转换，这里的技术都非常实用。

## 快速回答
- **本教程的主要目的是什么？** 将 EPUB 文件转换为 PDF 并应用自定义 PDF 页面尺寸。  
- **使用的库是哪一个？** Aspose.HTML for Java。  
- **需要许可证吗？** 提供免费试用版；生产环境需商业许可证。  
- **可以更改背景颜色吗？** 可以，使用 `PdfSaveOptions`。  
- **支持 Java 8+ 吗？** 完全支持——任何现代 Java 运行时均可。

## 什么是自定义 PDF 页面尺寸？

自定义 PDF 页面尺寸允许您为输出 PDF 的每一页定义精确的宽度和高度，而不是使用 A4、Letter 等标准尺寸。这在电子书、传单或任何需要视觉布局严格匹配特定设计的场景中尤为有用。

## 为什么选择 Aspose.HTML 进行 EPUB 转 PDF 转换？

- **高保真度：** 保留复杂布局、字体和图像。  
- **细粒度控制：** 通过 `PdfSaveOptions` 调整页面尺寸、背景、边距等。  
- **跨平台：** 在 Windows、Linux、macOS 上使用相同的 Java 代码。  
- **性能优秀：** 优化的渲染引擎实现快速转换。

## 前置条件

在开始之前，请确保您已具备：

- **Java 开发环境：** 已安装并配置 JDK 8 或更高版本。  
- **Aspose.HTML for Java：** 从[官方网站](https://releases.aspose.com/html/java/)下载最新 JAR 包。  
- **EPUB 文件：** 您希望转换的 `.epub` 文档。  

准备就绪后，下面进入实际的转换步骤。

## 步骤 1：打开 EPUB 文件

首先，需要使用 `FileInputStream` 打开 EPUB 文件。该流稍后会传递给转换器。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## 步骤 2：定义 PDF 保存选项

在这里设置 **自定义 PDF 页面尺寸** 以及可选的背景颜色。根据需要调整像素值以匹配目标尺寸。

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

### 小技巧：
- **像素 vs. 点：** `Length.fromPixels` 将屏幕像素转换为 PDF 点（1 点 = 1/72 英寸）。请选择能够反映最终打印尺寸的数值。

## 步骤 3：将 EPUB 转换为 PDF

准备好输入流和自定义选项后，调用转换器。输出的 PDF 将保存到您指定的位置。

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## 完整源代码

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
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
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## 常见问题及解决方案

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| **PDF 页面为空白** | 输入流在转换前已关闭 | 保持 `try‑with‑resources` 块在 `convertEPUB` 之后仍然打开。 |
| **页面尺寸不正确** | 使用的像素值未映射到所需的打印尺寸 | 将目标英寸转换为点（`1 inch = 72 points`），再使用 `Length.fromPixels` 转换为像素。 |
| **缺少字体** | EPUB 中未嵌入字体 | 确保字体已打包在 EPUB 中，或在主机机器上安装相应字体。 |

## 常见问答（FAQs）

### Aspose.HTML for Java 是免费库吗？
Aspose.HTML for Java 是商业库，但您可以从其[官方网站](https://releases.aspose.com/)获取免费试用版。

### 支持哪些 EPUB 格式的转换？
Aspose.HTML for Java 支持多种 EPUB 格式，兼容大多数 EPUB 文档。

### 我可以进一步自定义 PDF 输出吗？
可以，您可以通过 `PdfSaveOptions` 调整页面设置、背景颜色以及其他参数，以实现更细致的定制。

### Aspose.HTML for Java 试用版有哪些限制？
试用版可能存在一些限制，建议查阅官方文档获取详细信息。

### 哪里可以获得 Aspose.HTML for Java 的支持？
您可以在[Aspose.HTML 论坛](https://forum.aspose.com/)上寻找答案并获取技术支持。

---

**最后更新：** 2026-01-02  
**测试环境：** Aspose.HTML for Java 24.11（撰写时的最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}