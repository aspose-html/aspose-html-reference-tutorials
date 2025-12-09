---
date: 2025-12-01
description: Узнайте, как изменить размер страницы PDF, преобразовать HTML в PDF и
  создать PDF из HTML с помощью Aspose.HTML для Java. Легко управляйте размерами страниц.
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Настройка размера страницы PDF с помощью Aspose.HTML для Java
url: /ru/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adjust PDF Page Size with Aspose.HTML for Java

Генерация PDF из HTML – распространённая потребность для отчётов, счетов‑фактур и электронных книг. Когда вы **регулируете размер страницы PDF**, вы гарантируете, что конечный документ соответствует макету, созданному в HTML. В этом руководстве вы узнаете, как рендерить HTML в PDF, задавать пользовательские размеры и управлять тем, будет ли страница автоматически расширяться до самой широкой части содержимого. Мы пройдём полный практический пример с использованием Aspose.HTML for Java.

## Quick Answers
- **What does “adjust PDF page size” mean?** It lets you define the width and height of each PDF page or let the renderer automatically fit the widest element.  
- **Which library is used?** Aspose.HTML for Java (latest version).  
- **Do I need a license?** A free trial works for development; a commercial license is required for production.  
- **Can I change dimensions programmatically?** Yes – use `PageSetup` and the `AdjustToWidestPage` property.  
- **Is this compatible with Java 8+?** Absolutely – the API works with any JDK 8 or newer.

## What is “adjust PDF page size”?
Регулирование размера страницы PDF означает настройку размеров каждой страницы, которую создаёт HTML‑рендерер. Вы можете задать фиксированный размер (например, A4, Letter) или позволить рендереру вычислить оптимальную ширину на основе содержимого. Это даёт точный контроль над макетом, разбиением на страницы и визуальной точностью.

## Why adjust PDF page size when converting HTML to PDF?
- **Preserve design intent:** Prevent content from being cut off or stretched.  
- **Optimize for printing:** Match the paper size required by downstream processes.  
- **Improve readability:** Avoid excessive white space or cramped text.  
- **Dynamic documents:** Automatically fit wide tables or images without manual calculations.

## Prerequisites
Before you start, **make sure you have**:

- **Java Development Kit (JDK) 8 or higher** installed **on your** machine.  
- **Aspose.HTML for Java** – download the latest JAR **from the** [official release page](https://releases.aspose.com/html/java/).  
- **An HTML file** you want to convert (we’ll use `FirstFile.html` in the example).  

## Import Packages
First, import the classes we’ll need. The code block below is unchanged from the original tutorial.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## Step 1: Read the HTML Content
We read the source HTML file using a `FileInputStream`. This step prepares the raw markup for later manipulation.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Step 2: Write (and optionally enrich) the HTML
Here we copy the original HTML to a new file and inject a few inline styles to demonstrate **how styling affects the PDF output**. Feel **free** to replace the sample CSS with your own.

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

## Step 3: Render HTML to PDF – Two Scenarios
Now we’ll see how to **generate PDF from HTML** with **two different** page‑size strategies.

### 3.1 Page size NOT adjusted to content width
In this case we fix the page dimensions (100 × 100 points). If any **element** exceeds **these** limits, it will be clipped.

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

### 3.2 Page size ADJUSTED to content width
Here we enable `AdjustToWidestPage`, so the renderer automatically expands the page width **to accommodate the widest element while keeping the height fixed**.

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

## How to set PDF dimensions (how to change PDF page size) in code
The `PageSetup` object is the key:

- `setAnyPage(Page page)`: defines the base **width × height**.  
- `setAdjustToWidestPage(boolean)`: toggles automatic widening.  

By **adjusting** these two properties you can **how to set PDF dimensions** for any scenario, whether **you need** a static A4 page or a dynamic width that follows your HTML layout.

## Common Issues & Tips
| Issue | Why it Happens? | Fix |
|-------|----------------|-----|
| **Content gets cut off** | Fixed size is too small | Increase the `Size` values or enable `AdjustToWidestPage`. |
| **Text looks blurry** | Rendering DPI default is low | Use `PdfRenderingOptions.setResolution(int dpi)` to increase quality. |
| **Styles are missing** | External CSS not loaded | Embed CSS inline or use `HTMLDocument.setBaseUrl()` to point to your stylesheet folder. |
| **Large HTML files cause OutOfMemoryError** | Renderer loads whole document into memory | Process the document in chunks or increase JVM heap (`-Xmx`). |

## Frequently Asked Questions

**Q: What is Aspose.HTML for Java?**  
A: It is a Java library that lets you create, edit, and render HTML documents, including conversion to PDF, PNG, and other formats.

**Q: How can I adjust the PDF page size when converting HTML to PDF with Aspose.HTML for Java?**  
A: Use the `PageSetup` class and set `AdjustToWidestPage` to `true` (auto‑size) or `false` (fixed size). Then assign the desired `Size` via `new Page(new Size(width, height))`.

**Q: Can I customize the styling of HTML content before converting it to PDF?**  
A: Yes – you can inject CSS, modify the DOM, or use external style sheets. The tutorial demonstrates inline CSS injection.

**Q: Where can I find the documentation for Aspose.HTML for Java?**  
A: Comprehensive docs are available [here](https://reference.aspose.com/html/java/).

**Q: Is there a free trial available for Aspose.HTML for Java?**  
A: Absolutely – download a trial from the [release page](https://releases.aspose.com/html/java/).

## Conclusion
You now know how to **adjust PDF page size**, **render HTML as PDF**, and **set custom PDF dimensions** using Aspose.HTML for Java. Experiment with different page sizes, DPI settings, and CSS tweaks to perfect the output for your specific use case. If you run into challenges, refer to the official documentation or the Aspose support forums.

---

**Last Updated:** 2025-12-01  
**Tested With:** Aspose.HTML for Java 24.12 (latest)  
**Author:** Aspose  
**Related Resources:** [API Reference](https://reference.aspose.com/html/java/) | [Download Free Trial](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}