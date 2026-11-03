---
category: general
date: 2026-06-19
description: Learn how to generate pdf from html using a simple Java example. This
  html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: en
og_description: html to pdf tutorial shows you how to generate PDF from HTML using
  Java. Follow the steps to convert HTML file PDF quickly.
og_title: 'html to pdf tutorial: Java conversion guide'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'html to pdf tutorial: Convert HTML to PDF in Java'
url: /java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf tutorial – Turn an HTML page into a PDF with Java

Ever wondered how to turn a static HTML page into a sleek PDF document without leaving your IDE? You're not alone. In this **html to pdf tutorial** we’ll walk through a complete, ready‑to‑run Java example that **generate pdf from html** in just a few minutes.

We’ll cover everything you need—project setup, adding the right library, writing the conversion code, and even a quick tip for converting a live webpage to PDF. By the end you’ll be able to **convert html file pdf** on your own machine, and you’ll understand how to **create pdf from html** for any future project.

## What you’ll need

- Java 17 or newer (the code works with any recent JDK)
- Maven or Gradle (we’ll show the Maven snippet)
- A tiny HTML file you want to turn into a PDF (we’ll create one on the fly)
- An IDE or a simple text editor—your call

That’s it. No heavyweight servers, no paid SDKs, just pure Java and a free open‑source library.

## Step 1: html to pdf tutorial – Set up a Maven project

First things first. Create a new Maven project (or add to an existing one). The only dependency you really need is **OpenHTMLtoPDF**, which does the heavy lifting of rendering HTML and CSS into a PDF.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** If you’re using Gradle, the same dependencies can be added under `implementation` in `build.gradle`.  

Why this step matters: without the library the JVM has no idea how to translate HTML tags into PDF drawing commands. OpenHTMLtoPDF is lightweight, actively maintained, and works with CSS‑2.1, so your styling stays intact.

## Step 2: generate pdf from html – Prepare a sample HTML file

Let’s create a tiny `input.html` right next to our Java source. This keeps the example self‑contained and demonstrates the **create pdf from html** workflow.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

You can replace the content with anything—tables, images, even JavaScript (though the renderer ignores scripts). The important part is that the file lives on the classpath so the converter can locate it.

## Step 3: convert html file pdf – Write the conversion utility

Now the heart of the **html to pdf tutorial**: a tiny `HtmlToPdfConverter` class that reads the HTML and writes a PDF. The code below is a full, runnable example; copy‑paste it into `src/main/java/com/example/HtmlToPdfConverter.java`.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Why this code works

1. **Resource flexibility** – the method first checks if the supplied path points to a real file; if not, it falls back to a classpath resource. That means you can **convert webpage to pdf** later by feeding a URL string (just replace the `withHtmlContent` call with `withUri`).

2. **Automatic directory creation** – `Files.createDirectories` guarantees the `target/` folder exists, so you won’t get a “No such file or directory” error.

3. **Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and page layout internally. No need to manually manage PDF pages; the library does it for you, keeping the example short and focused on the **convert html file pdf** concept.

## Step 4: create pdf from html – Run the program and verify

Open a terminal in the project root and execute:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

If everything is set up correctly you’ll see:

```
✅ PDF successfully created at target/output.pdf
```

Open `target/output.pdf` with any PDF viewer. You should see the styled “Monthly Sales Report” header, the paragraph text, and the same margins you defined in the HTML `<style>` block.

> **What if you don’t see the styling?**  
> Make sure the CSS is inline or located in the same folder as the HTML. OpenHTMLtoPDF resolves relative URLs based on the base URI you pass to `withHtmlContent`. In the snippet above we passed `null`, which works for simple inline CSS. For external stylesheets, supply the directory path as the second argument.

## Step 5: convert webpage to pdf – Handling remote URLs (optional)

Sometimes you need to **convert webpage to pdf** directly from the internet—think of archiving an online receipt. The library supports this via `withUri`. Here’s a quick adaptation:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Call it like:

```java
convertUrl("https://example.com/report.html", "target/web-report.pdf


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/english/java/configuring-environment/)
- [Convert HTML to PDF in Java – Step‑by‑Step Guide with Page Size Settings](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}