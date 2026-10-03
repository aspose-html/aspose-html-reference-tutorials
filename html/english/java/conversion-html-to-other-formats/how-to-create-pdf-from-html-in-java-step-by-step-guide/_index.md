---
category: general
date: 2026-10-02
description: Create pdf from html in Java with a single call. This tutorial shows
  how to convert html to pdf, configure options, and handle common issues.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- how to convert html to pdf
- html to pdf conversion java
- convert html file to pdf
language: en
lastmod: 2026-10-02
og_description: Create pdf from html in Java using HtmlConverter. Follow this complete
  guide to convert html to pdf, set options, and avoid pitfalls.
og_image_alt: Diagram showing create pdf from html process in Java
og_title: Create pdf from html in Java – quick, reliable conversion
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Create pdf from html in Java with a single call. This tutorial shows
    how to convert html to pdf, configure options, and handle common issues.
  headline: How to create pdf from html in Java – step‑by‑step guide
  type: TechArticle
- description: Create pdf from html in Java with a single call. This tutorial shows
    how to convert html to pdf, configure options, and handle common issues.
  name: How to create pdf from html in Java – step‑by‑step guide
  steps:
  - name: Why this approach works
    text: '* **Single responsibility** – the `convertHtmlToPdf` method isolates the
      conversion logic, making the code easy to test. * **Resource safety** – `try‑with‑resources`
      guarantees that the `PDDocument` is closed, preventing file‑handle leaks. *
      **Flexibility** – you can swap `HtmlRenderer` for another '
  - name: 1️⃣ Specify the source HTML file and the target PDF file
    text: '```java private static final String INPUT_PATH = "YOUR_DIRECTORY/input.html";
      private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf"; ``` *Replace
      `YOUR_DIRECTORY` with an absolute or relative path that your Java process can
      read/write.*'
  - name: 2️⃣ Load the HTML content
    text: '```java String html = Files.readString(Path.of(INPUT_PATH)); ``` Reading
      the file as a `String` preserves the original markup and makes it easy to feed
      the converter. The method assumes UTF‑8; if your HTML uses a different charset,
      use `Files.readAllBytes` and decode accordingly.'
  - name: 3️⃣ Convert the HTML document to PDF
    text: '```java byte[] pdfBytes = convertHtmlToPdf(html); ``` `convertHtmlToPdf`
      encapsulates **how to convert html to pdf**. Inside, `HtmlRenderer` parses the
      markup, applies CSS, and draws the result onto a PDF page. This is the heart
      of the **html to pdf conversion java** process.'
  - name: 4️⃣ Write the PDF file
    text: '```java Files.write(Path.of(OUTPUT_PATH), pdfBytes, StandardOpenOption.CREATE,
      StandardOpenOption.TRUNCATE_EXISTING); ``` The `Files.write` call creates the
      output file if it does not exist, or overwrites it otherwise. The method throws
      `IOException` if the directory is missing or the process lacks '
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: How to create pdf from html in Java – step‑by‑step guide
url: /java/conversion-html-to-other-formats/how-to-create-pdf-from-html-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create pdf from html in Java – step‑by‑step guide

If you need to **create pdf from html** in a Java application, this guide shows you a complete, ready‑to‑run solution. You’ll see how to **convert html to pdf** with a single method call, configure the conversion, and handle typical edge cases.

We’ll cover everything you need to know: required dependencies, a full source file, and tips for troubleshooting. By the end you’ll be able to **convert html file to pdf** reliably in any Java project.

## Prerequisites

Before you start, make sure you have:

* JDK 17 or newer installed  
* Maven 3.8+ (or Gradle) to manage dependencies  
* Basic familiarity with Java I/O  

The example uses the open‑source **HtmlConverter** class from the *pdfbox‑layout* library, which wraps Apache PDFBox for HTML rendering. If you prefer another library, the same steps apply—just adjust the import statements.

## Add the required dependency

Add the following Maven coordinates to your `pom.xml`. This pulls in PDFBox and the HTML‑to‑PDF helper.

```xml
<dependency>
    <groupId>org.apache.pdfbox</groupId>
    <artifactId>pdfbox</artifactId>
    <version>3.0.2</version>
</dependency>
<dependency>
    <groupId>com.github.jhonnymertz</groupId>
    <artifactId>pdfbox-layout</artifactId>
    <version>1.0.0</version>
</dependency>
```

If you use Gradle, the equivalent is:

```gradle
implementation "org.apache.pdfbox:pdfbox:3.0.2"
implementation "com.github.jhonnymertz:pdfbox-layout:1.0.0"
```

> **Pro tip:** Keep your dependencies up to date; newer versions fix rendering bugs and add CSS support.

## Create pdf from html – overall workflow

The conversion consists of three logical steps:

1. **Read the source HTML file** – ensure the path is correct and the file is UTF‑8 encoded.  
2. **Invoke the converter** – the library parses the HTML, applies CSS, and generates a PDF document.  
3. **Write the PDF to disk** – handle I/O exceptions and confirm that the file was created.

Below is a complete, self‑contained Java class that implements this workflow.

```java
package com.example.pdfconverter;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

import org.apache.pdfbox.pdmodel.PDDocument;
import org.apache.pdfbox.pdmodel.PDPage;
import org.apache.pdfbox.pdmodel.PDPageContentStream;
import org.apache.pdfbox.pdmodel.common.PDRectangle;
import org.apache.pdfbox.layout.Document;
import org.apache.pdfbox.layout.element.Paragraph;
import org.apache.pdfbox.layout.renderer.HtmlRenderer;

/**
 * Simple utility that demonstrates how to create pdf from html in Java.
 *
 * The class reads an HTML file, converts it to PDF, and saves the result.
 * It uses Apache PDFBox together with the pdfbox‑layout HtmlRenderer.
 *
 * Adjust INPUT_PATH and OUTPUT_PATH to match your environment.
 */
public class HtmlToPdfConverter {

    // --------------------------------------------------------------------
    // 1️⃣  Define input and output locations
    // --------------------------------------------------------------------
    private static final String INPUT_PATH  = "YOUR_DIRECTORY/input.html";
    private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf";

    public static void main(String[] args) {
        try {
            // --------------------------------------------------------------
            // 2️⃣  Load the HTML content (UTF‑8 is assumed)
            // --------------------------------------------------------------
            String html = Files.readString(Path.of(INPUT_PATH));

            // --------------------------------------------------------------
            // 3️⃣  Perform the conversion
            // --------------------------------------------------------------
            byte[] pdfBytes = convertHtmlToPdf(html);

            // --------------------------------------------------------------
            // 4️⃣  Write the PDF file to disk
            // --------------------------------------------------------------
            Files.write(Path.of(OUTPUT_PATH), pdfBytes,
                    StandardOpenOption.CREATE,
                    StandardOpenOption.TRUNCATE_EXISTING);

            System.out.println("✅ PDF created successfully at " + OUTPUT_PATH);
        } catch (IOException e) {
            System.err.println("❌ Failed to convert HTML to PDF: " + e.getMessage());
            e.printStackTrace();
        }
    }

    /**
     * Core conversion logic.
     *
     * @param html the raw HTML string
     * @return a byte array containing the generated PDF
     * @throws IOException if PDF generation fails
     */
    private static byte[] convertHtmlToPdf(String html) throws IOException {
        // Create a new PDFBox document – this is the container for the output.
        try (PDDocument pdDocument = new PDDocument()) {

            // The HtmlRenderer parses the HTML and draws it onto a PDF page.
            HtmlRenderer renderer = new HtmlRenderer(pdDocument);
            renderer.renderHtml(html);

            // Save the document into a byte array so we can write it later.
            return toByteArray(pdDocument);
        }
    }

    /**
     * Helper that converts a PDDocument into a byte array.
     *
     * @param document the populated PDFBox document
     * @return PDF content as a byte array
     * @throws IOException if writing fails
     */
    private static byte[] toByteArray(PDDocument document) throws IOException {
        try (java.io.ByteArrayOutputStream out = new java.io.ByteArrayOutputStream()) {
            document.save(out);
            return out.toByteArray();
        }
    }
}
```

### Why this approach works

* **Single responsibility** – the `convertHtmlToPdf` method isolates the conversion logic, making the code easy to test.  
* **Resource safety** – `try‑with‑resources` guarantees that the `PDDocument` is closed, preventing file‑handle leaks.  
* **Flexibility** – you can swap `HtmlRenderer` for another implementation (e.g., *OpenHTMLtoPDF*) without touching the surrounding I/O code, which is useful when you need **html to pdf conversion java** that supports advanced CSS.

## Step‑by‑step explanation

### 1️⃣ Specify the source HTML file and the target PDF file
```java
private static final String INPUT_PATH  = "YOUR_DIRECTORY/input.html";
private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf";
```
*Replace `YOUR_DIRECTORY` with an absolute or relative path that your Java process can read/write.*

### 2️⃣ Load the HTML content
```java
String html = Files.readString(Path.of(INPUT_PATH));
```
Reading the file as a `String` preserves the original markup and makes it easy to feed the converter. The method assumes UTF‑8; if your HTML uses a different charset, use `Files.readAllBytes` and decode accordingly.

### 3️⃣ Convert the HTML document to PDF
```java
byte[] pdfBytes = convertHtmlToPdf(html);
```
`convertHtmlToPdf` encapsulates **how to convert html to pdf**. Inside, `HtmlRenderer` parses the markup, applies CSS, and draws the result onto a PDF page. This is the heart of the **html to pdf conversion java** process.

### 4️⃣ Write the PDF file
```java
Files.write(Path.of(OUTPUT_PATH), pdfBytes,
        StandardOpenOption.CREATE,
        StandardOpenOption.TRUNCATE_EXISTING);
```
The `Files.write` call creates the output file if it does not exist, or overwrites it otherwise. The method throws `IOException` if the directory is missing or the process lacks write permission.

## Handling common pitfalls

| Issue | Symptoms | Fix |
|-------|----------|-----|
| **Missing input file** | `java.nio.file.NoSuchFileException` | Verify `INPUT_PATH` points to an existing file. Use `Files.exists(Path)` for a pre‑flight check. |
| **Unsupported CSS** | Layout looks plain or broken | Use a more feature‑rich engine such as *OpenHTMLtoPDF* (add its Maven dependency and replace `HtmlRenderer` with `PdfRendererBuilder`). |
| **Large HTML causing memory pressure** | `OutOfMemoryError` | Stream the HTML in chunks or increase the JVM heap (`-Xmx2g`). |
| **Unicode characters appear as �** | Garbled text in the PDF | Ensure the HTML file is saved as UTF‑8 and that the renderer’s font supports the required glyphs (embed a font via `renderer.setDefaultFont("Arial Unicode MS")`). |

## Full working example

Save the class above as `src/main/java/com/example/pdfconverter/HtmlToPdfConverter.java`, adjust the paths, and run:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.pdfconverter.HtmlToPdfConverter"
```

If everything is set up correctly, you’ll see:

```
✅ PDF created successfully at YOUR_DIRECTORY/output.pdf
```

Open `output.pdf` with any PDF viewer—you should see the rendered HTML page exactly as it appears in a browser.

## Conclusion

You now know how to **create pdf from html** in Java using a concise, production‑ready pattern. The tutorial covered:

* Adding the necessary Maven dependencies  
* Reading an HTML file safely  
* Performing the **convert html file to pdf** operation with `HtmlRenderer`  
* Writing the resulting PDF and handling I/O errors  

From here you can explore advanced topics such as **convert html to pdf** with custom headers/footers, streaming large documents, or switching to a different rendering engine for richer CSS support.

**Next steps**

* Try **how to convert html to pdf** with *OpenHTMLtoPDF* for better CSS3 handling.  
* Experiment with adding a cover page or table of contents using PDFBox directly.  
* Look into server‑side PDF generation for web services, where you return the PDF bytes in an HTTP response.

Happy coding, and enjoy the smooth workflow of turning HTML into high‑quality PDFs!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Create PDF from HTML in Java – Complete Step‑by‑Step Guide](/html/english/java/conversion-html-to-other-formats/create-pdf-from-html-in-java-complete-step-by-step-guide/)
- [html to pdf tutorial: Convert HTML to PDF in Java in One Line](/html/english/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java-in-one-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}