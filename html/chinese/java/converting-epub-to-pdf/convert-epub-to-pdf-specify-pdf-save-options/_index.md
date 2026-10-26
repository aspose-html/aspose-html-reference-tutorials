---
date: 2026-05-30
description: 了解如何在 Java 中使用 Aspose.HTML 将 EPUB 转换为 PDF，同时设置自定义 PDF 页面大小和其他 PDF 保存选项。
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: 为 EPUB 转 PDF 指定 PDF 保存选项
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: 自定义 PDF 页面大小 - 为 EPUB 转 PDF 指定 PDF 保存选项
url: /zh/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 自定义 PDF 页面尺寸：为 EPUB 转 PDF 指定 PDF 保存选项

## 介绍

Aspose.HTML for Java 使 **convert EPUB to PDF** 变得轻松，并让您对输出拥有完整控制，包括设置 **custom PDF page size**。在本分步指南中，我们将从环境准备到微调 `PdfSaveOptions`，帮助您生成符合精确页面尺寸要求的 PDF。无论您是在构建出版流水线、电子学习平台，还是仅需自动化文档转换，这里的技术都非常有价值。

## 快速回答
- **本教程的主要目的是什么？** 将 EPUB 文件转换为 PDF，同时应用自定义 PDF 页面尺寸。  
- **使用的是哪个库？** Aspose.HTML for Java。  
- **需要许可证吗？** 提供免费试用版；生产环境需要商业许可证。  
- **可以更改背景颜色吗？** 可以，使用 `PdfSaveOptions`。  
- **支持 Java 8+ 吗？** 完全支持——任何现代 Java 运行时均可。

## 什么是自定义 PDF 页面尺寸？

自定义 PDF 页面尺寸允许您为输出 PDF 的每一页定义精确的宽度和高度，而不是使用 A4、Letter 等标准尺寸。您可以使用点（1 point = 1/72 inch）或像素进行设置，从而实现像素级的布局控制。这对于电子书、传单或任何需要匹配预定义格式而无需手动后处理的设计尤为理想。

## 为什么使用 Aspose.HTML 进行 EPUB 转 PDF 转换？

Aspose.HTML 只需两行代码即可将 EPUB 转换为 PDF，同时保留复杂布局、嵌入字体和高分辨率图像。它支持 **50+ input and output formats**，能够在不将整个文件加载到内存的情况下渲染高达 **2,000 pages** 的 PDF，并在 Windows、Linux 和 macOS 上提供一致的结果。该库还提供细粒度的 PDF‑save 选项，让您可以从 Java 中调节页面尺寸、背景颜色、边距和压缩设置。

## 前置条件
- **Java 开发环境：** 已安装并配置 JDK 8 或更高版本。  
- **Aspose.HTML for Java：** 从[网站](https://releases.aspose.com/html/java/)下载最新的 JAR 包。  
- **EPUB 文件：** 您想要转换的 `.epub` 文档。  

现在一切就绪，让我们深入实际的转换步骤。

## 如何使用自定义页面尺寸将 EPUB 转换为 PDF？

`FileInputStream` 是一个读取文件原始字节的 Java 类。  
`PdfSaveOptions` 是 Aspose.HTML 中用于配置 PDF 输出设置（如页面尺寸和背景颜色）的类。  
使用 `FileInputStream` 加载 EPUB，配置 `PdfSaveOptions` 以指定精确的页面尺寸，然后调用转换器。以下三步工作流可在典型电子书大小下在一分钟内完成转换，并能以最少代码改动扩展到更大的集合。

### 步骤 1：打开 EPUB 文件

首先，创建指向源 `.epub` 的 `FileInputStream`。在转换完成之前保持流打开，可防止出现“空白页”错误。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### 步骤 2：定义 PDF 保存选项

`PdfSaveOptions` 是 Aspose.HTML 的配置类，控制 PDF 输出设置，如页面尺寸、背景颜色和边距。  
`Length.fromPixels` 将屏幕像素转换为 PDF 点（1 point = 1/72 inch），允许您使用熟悉的像素单位指定尺寸。

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

#### 专业提示：
- **Pixels vs. Points：** `Length.fromPixels` 将屏幕像素转换为 PDF 点（1 point = 1/72 inch）。请选择能反映最终打印尺寸的数值。

### 步骤 3：将 EPUB 转换为 PDF

准备好输入流和自定义选项后，调用转换器。输出的 PDF 将保存到您指定的位置，保持您定义的精确页面尺寸。

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` 是一个在 PDF 转换期间启用页面并行处理的方法。

## 完整源代码

完整、可运行的示例将上述三步合并为一个 Java 类。请将占位符路径替换为您自己的文件位置。

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
|-------|-------|-----|
| **PDF pages are blank** | Input stream closed before conversion | Keep the `try‑with‑resources` block open until after `convertEPUB`. |
| **Incorrect page dimensions** | Using pixels that don’t map to desired print size | Convert desired inches to points (`1 inch = 72 points`) and then to pixels using `Length.fromPixels`. |
| **Missing fonts** | Fonts not embedded in EPUB | Ensure the fonts are packaged inside the EPUB or install them on the host machine. |
| **Performance slowdown on large books** | Rendering every page sequentially | Enable multi‑threaded rendering via `PdfSaveOptions.setEnableParallelProcessing(true)` for faster processing of 500+ page EPUBs. |

## 常见问答 (FAQs)

**Q: Aspose.HTML for Java 是免费库吗？**  
A: Aspose.HTML for Java 是商业库，但您可以从他们的[网站](https://releases.aspose.com/)获取免费试用版。

**Q: 支持哪些 EPUB 格式进行转换？**  
A: Aspose.HTML for Java 支持 EPUB 2.0、EPUB 3.0 和 EPUB 3.1，能够处理可重排和固定布局的书籍，并提供完整的 CSS 支持。

**Q: 我可以进一步自定义 PDF 输出吗？**  
A: 可以，您可以通过在 `PdfSaveOptions` 中调整页面设置、背景颜色、压缩级别以及其他设置来自定义 PDF 输出。

**Q: Aspose.HTML for Java 试用版有哪些限制？**  
A: 试用版可能在前几页添加水印，并将最大文件大小限制为 10 MB；购买许可证可移除这些限制。

**Q: 在哪里可以获得 Aspose.HTML for Java 的支持？**  
A: 您可以在 [Aspose.HTML 论坛](https://forum.aspose.com/) 上找到答案并寻求支持。

---

**Last Updated:** 2026-05-30  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose

## 相关教程

- [使用 Aspose.HTML for Java 调整 PDF 页面尺寸](/html/java/advanced-usage/adjust-pdf-page-size/)
- [使用 Aspose.HTML 的 Java 将 EPUB 转换为 PDF 的方法](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [使用 Aspose.HTML for Java 将 EPUB 转换为 PDF 和图像](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}