---
date: 2025-12-01
description: 学习如何使用 Aspose.HTML for Java 调整 PDF 页面大小、将 HTML 渲染为 PDF 并从 HTML 生成 PDF。轻松控制页面尺寸。
language: zh
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: 使用 Aspose.HTML for Java 调整 PDF 页面大小
url: /java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.HTML for Java 调整 PDF 页面大小

从 HTML 生成 PDF 是报告、发票和电子书等常见需求。**调整 PDF 页面大小** 可以确保最终文档与您在 HTML 中设计的布局保持一致。在本教程中，您将学习如何将 HTML 渲染为 PDF、设置自定义尺寸，以及控制页面是否自动扩展以适应最宽的内容。我们将通过一个完整的实战示例，使用 Aspose.HTML for Java 来演示。

## 快速答案
- **“adjust PDF page size” 是什么意思？** 它允许您定义每个 PDF 页面的宽度和高度，或让渲染器自动适配最宽的元素。  
- **使用的库是哪一个？** Aspose.HTML for Java（最新版本）。  
- **需要许可证吗？** 免费试用可用于开发；生产环境需要商业许可证。  
- **可以在代码中动态更改尺寸吗？** 可以——使用 `PageSetup` 和 `AdjustToWidestPage` 属性。  
- **是否兼容 Java 8+？** 完全兼容——API 可在任何 JDK 8 或更高版本上运行。

## 什么是 “adjust PDF page size”？
调整 PDF 页面大小指的是为 HTML 渲染器创建的每一页设置尺寸。您可以指定固定尺寸（例如 A4、Letter），也可以让渲染器根据内容自动计算最佳宽度。这样可以精确控制布局、分页以及视觉保真度。

## 为什么在将 HTML 转换为 PDF 时要调整页面大小？
- **保持设计意图：** 防止内容被截断或拉伸。  
- **优化打印：** 与下游流程所需的纸张尺寸匹配。  
- **提升可读性：** 避免过多空白或文字过于拥挤。  
- **动态文档：** 自动适配宽表格或图片，无需手动计算。

## 前置条件
在开始之前，请确保您已具备以下条件：

- **Java Development Kit (JDK) 8 或更高版本** 已安装在本机。  
- **Aspose.HTML for Java** – 从[官方发布页面](https://releases.aspose.com/html/java/)下载最新 JAR 包。  
- **要转换的 HTML 文件**（本示例使用 `FirstFile.html`）。

## 导入包
首先导入我们需要的类。下面的代码块保持原样。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## 第 1 步：读取 HTML 内容
使用 `FileInputStream` 读取源 HTML 文件，为后续操作准备原始标记。

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## 第 2 步：写入（并可选地丰富）HTML
这里我们将原始 HTML 复制到新文件，并注入少量内联样式，以演示样式对 PDF 输出的影响。您可以自行替换示例 CSS。

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
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

## 第 3 步：将 HTML 渲染为 PDF – 两种场景
下面展示 **从 HTML 生成 PDF** 的两种不同页面尺寸策略。

### 3.1 页面尺寸未根据内容宽度调整
此情况下我们固定页面尺寸为 100 × 100 points。如果有元素超出此范围，将被裁剪。

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 页面尺寸已根据内容宽度调整
这里启用 `AdjustToWidestPage`，渲染器会自动扩展页面宽度以容纳最宽元素，同时保持高度不变。

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## 如何在代码中设置 PDF 尺寸（如何更改 PDF 页面大小）
`PageSetup` 对象是关键：

- `setAnyPage(Page page)`: 定义基础宽度 × 高度。  
- `setAdjustToWidestPage(boolean)`: 切换自动宽度扩展。

通过调整这两个属性，您可以 **设置 PDF 尺寸**，无论是静态的 A4 页面，还是随 HTML 布局动态变化的宽度。

## 常见问题与技巧
| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| 内容被截断 | 固定尺寸过小 | 增大 `Size` 值或启用 `AdjustToWidestPage`。 |
| 文字模糊 | 默认渲染 DPI 较低 | 使用 `PdfRenderingOptions.setResolution(int dpi)` 提高分辨率。 |
| 样式缺失 | 外部 CSS 未加载 | 将 CSS 内联或使用 `HTMLDocument.setBaseUrl()` 指向样式文件夹。 |
| 大型 HTML 导致 OutOfMemoryError | 渲染器一次性加载整个文档 | 将文档分块处理或增大 JVM 堆内存 (`-Xmx`)。 |

## 常见问答

**Q: 什么是 Aspose.HTML for Java？**  
A: 这是一款 Java 库，可创建、编辑和渲染 HTML 文档，支持转换为 PDF、PNG 等多种格式。

**Q: 如何在使用 Aspose.HTML for Java 将 HTML 转换为 PDF 时调整 PDF 页面大小？**  
A: 使用 `PageSetup` 类并将 `AdjustToWidestPage` 设置为 `true`（自动）或 `false`（固定），然后通过 `new Page(new Size(width, height))` 指定所需的 `Size`。

**Q: 在转换为 PDF 之前，我可以自定义 HTML 内容的样式吗？**  
A: 可以——您可以注入 CSS、修改 DOM，或使用外部样式表。教程中演示了内联 CSS 注入的方式。

**Q: 在哪里可以找到 Aspose.HTML for Java 的文档？**  
A: 完整文档请访问[此处](https://reference.aspose.com/html/java/)。

**Q: Aspose.HTML for Java 有免费试用吗？**  
A: 有——可从[发布页面](https://releases.aspose.com/html/java/)下载试用版。

## 结论
现在，您已经掌握了 **调整 PDF 页面大小**、**将 HTML 渲染为 PDF** 以及 **在代码中设置自定义 PDF 尺寸** 的方法。请尝试不同的页面尺寸、DPI 设置和 CSS 调整，以获得最适合您业务场景的输出效果。如遇到问题，请参考官方文档或 Aspose 支持论坛。

---

**Last Updated:** 2025-12-01  
**Tested With:** Aspose.HTML for Java 24.12 (latest)  
**Author:** Aspose  
**Related Resources:** [API Reference](https://reference.aspose.com/html/java/) | [Download Free Trial](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}