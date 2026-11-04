---
category: general
date: 2026-06-03
description: Convert markdown to PDF using Java. Learn how to generate PDF from markdown
  with a simple library and create PDF from markdown file in minutes.
draft: false
keywords:
- convert markdown to pdf
- generate pdf from markdown
- create pdf from markdown file
- how to convert markdown to pdf
- convert markdown file to pdf
language: en
og_description: Convert markdown to PDF quickly. This guide shows how to generate
  PDF from markdown, create PDF from markdown file, and answer how to convert markdown
  to PDF.
og_title: Convert Markdown to PDF in Java – Complete Programming Guide
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Convert markdown to PDF using Java. Learn how to generate PDF from
    markdown with a simple library and create PDF from markdown file in minutes.
  headline: Convert Markdown to PDF in Java – Full Step‑by‑Step Guide
  type: TechArticle
tags:
- Java
- Markdown
- PDF
- Document Conversion
title: Convert Markdown to PDF in Java – Full Step‑by‑Step Guide
url: /java/conversion-html-to-other-formats/convert-markdown-to-pdf-in-java-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert Markdown to PDF in Java – Full Step‑by‑Step Guide

Ever wondered **how to convert markdown to pdf** without leaving your IDE? You're not alone. Many developers need to turn README files, blog drafts, or technical specs into nicely‑formatted PDFs for sharing, and doing it programmatically saves a ton of manual copy‑pasting.

In this tutorial we’ll walk through a clean, production‑ready solution that **generates PDF from markdown** using only a couple of Maven dependencies. By the end you’ll be able to **create pdf from markdown file** with just a few lines of Java, and you’ll also see how to handle images, custom CSS, and large documents.  

> **Pro tip:** The same approach works for converting markdown files to other formats (HTML, DOCX) – you only need to swap the final renderer.

## What You’ll Learn

- Set up the required libraries (`flexmark-java` and `openhtmltopdf`).
- Read a markdown file from disk.
- Transform markdown into HTML (the bridge between markdown and PDF).
- Feed the HTML to a PDF renderer and write the output file.
- Tackle common edge cases like relative image paths and Unicode characters.

## Prerequisites

- JDK 17 or newer (the code uses the `var` keyword for brevity, but you can downgrade to 11 if needed).
- Maven or Gradle build tool (Maven example shown).
- A markdown file you want to convert – for demo purposes we’ll use `readme.md` placed in a folder called `YOUR_DIRECTORY`.

---

## Step 1: Add the Conversion Libraries

First, pull in two well‑maintained libraries:

| Library | Why we need it | Maven coordinate |
|---------|----------------|------------------|
| **flexmark‑java** | Parses Markdown and renders it as HTML. | `com.vladsch.flexmark:flexmark-all:0.64.8` |
| **openhtmltopdf‑core** | Takes the HTML and produces a PDF. | `org.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` |

Add them to your `pom.xml`:

```xml
<dependencies>
    <!-- Flexmark – Markdown → HTML -->
    <dependency>
        <groupId>com.vladsch.flexmark</groupId>
        <artifactId>flexmark-all</artifactId>
        <version>0.64.8</version>
    </dependency>

    <!-- OpenHTMLtoPDF – HTML → PDF -->
    <dependency>
        <groupId>org.openhtmltopdf</groupId>
        <artifactId>openhtmltopdf-pdfbox</artifactId>
        <version>1.0.10</version>
    </dependency>
</dependencies>
```

> **Why these two?** Flexmark gives us a faithful Markdown‑to‑HTML conversion (tables, code fences, footnotes, you name it). OpenHTMLtoPDF then renders that HTML using the PDFBox engine, which handles fonts and images out‑of‑the‑box. Together they let us **convert markdown file to pdf** with minimal boilerplate.

---

## Step 2: Read the Markdown Source

We’ll read the file into a `String`. Using `java.nio.file.Files` keeps the code concise and handles Unicode automatically.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.charset.StandardCharsets;
import java.io.IOException;

/**
 * Loads the markdown content from the given path.
 *
 * @param markdownPath absolute or relative path to the .md file
 * @return the file content as a UTF‑8 string
 * @throws IOException if the file cannot be read
 */
static String loadMarkdown(String markdownPath) throws IOException {
    Path path = Path.of(markdownPath);
    return Files.readString(path, StandardCharsets.UTF_8);
}
```

> **Edge case:** If your markdown contains Windows line endings (`\r\n`), `readString` normalises them to `\n`, which is what Flexmark expects.

---

## Step 3: Convert Markdown to HTML

Flexmark does the heavy lifting. You can customise the parser – for example, enable GitHub‑flavoured tables or footnotes – but the default configuration works for most docs.

```java
import com.vladsch.flexmark.html.HtmlRenderer;
import com.vladsch.flexmark.parser.Parser;
import com.vladsch.flexmark.util.ast.Node;

/**
 * Turns raw markdown into HTML.
 *
 * @param markdown the markdown source
 * @return HTML string ready for PDF rendering
 */
static String markdownToHtml(String markdown) {
    Parser parser = Parser.builder().build();
    HtmlRenderer renderer = HtmlRenderer.builder().build();
    Node document = parser.parse(markdown);
    return renderer.render(document);
}
```

**Why we go through HTML:** PDF generators understand layout, CSS, and fonts far better than raw markdown. By converting to HTML first, we gain full control over styling – think custom headers, page numbers, or even a watermark.

---

## Step 4: Render the HTML as PDF

OpenHTMLtoPDF accepts a simple `String` of HTML and writes a PDF to an `OutputStream`. Below is a tiny wrapper that also adds a basic CSS stylesheet (you can replace `style.css` with your own).

```java
import org.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.OutputStream;
import java.io.FileOutputStream;

/**
 * Generates a PDF file from HTML.
 *
 * @param html   the HTML content produced by Flexmark
 * @param pdfPath path where the resulting PDF should be saved
 * @throws IOException if writing the PDF fails
 */
static void htmlToPdf(String html, String pdfPath) throws IOException {
    try (OutputStream os = new FileOutputStream(pdfPath)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.useFastMode();                     // speeds up rendering for large docs
        builder.withHtmlContent(html, null);       // base URI null → relative URLs resolved against working dir
        builder.toStream(os);
        // Optional: add a custom stylesheet
        // builder.withCssFile(new File("style.css"));
        builder.run();
    }
}
```

> **Note on images:** If your markdown references images with relative paths, make sure those files are accessible from the working directory or set a proper base URI in `withHtmlContent(html, baseUri)`.

---

## Step 5: Pull It All Together – The One‑Liner Converter

Now we can implement the exact three‑line conversion shown in the original snippet, but with proper error handling and logging.

```java
public class MarkdownPdfConverter {

    /**
     * Convert a markdown file directly to a PDF file.
     *
     * @param markdownPath path to the source .md file
     * @param pdfPath      desired output .pdf file
     */
    public static void convert(String markdownPath, String pdfPath) {
        try {
            // Step 1: Load markdown
            String markdown = loadMarkdown(markdownPath);

            // Step 2: Transform to HTML
            String html = markdownToHtml(markdown);

            // Step 3: Render PDF
            htmlToPdf(html, pdfPath);

            System.out.println("✅ Successfully created PDF at " + pdfPath);
        } catch (IOException e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps (loadMarkdown, markdownToHtml, htmlToPdf) -----
    // (Copy‑paste the static methods defined earlier here)
}
```

### Running the Converter

```java
public class Main {
    public static void main(String[] args) {
        // Step 1: Define the path to the source Markdown file
        String markdownPath = "YOUR_DIRECTORY/readme.md";

        // Step 2: Define the desired output PDF file path
        String pdfPath = "YOUR_DIRECTORY/readme.pdf";

        // Step 3: Convert the Markdown document directly to PDF
        MarkdownPdfConverter.convert(markdownPath, pdfPath);
    }
}
```

**Expected output on the console**

```
✅ Successfully created PDF at YOUR_DIRECTORY/readme.pdf
```

Open `readme.pdf` – you should see a nicely formatted document that mirrors the original markdown structure, complete with headings, bullet lists, and code blocks.

---

## Handling Common Pitfalls

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Missing images** | Relative image paths are resolved against the JVM’s working directory, not the markdown file location. | Pass the markdown folder as the base URI: `builder.withHtmlContent(html, new File(markdownPath).getParentFile().toURI().toString());` |
| **Unicode gibberish** | The PDF renderer defaults to a limited font set. | Embed a Unicode‑capable font via `builder.useFont(new File("fonts/DejaVuSans.ttf"), "DejaVu Sans", 400, PdfRendererBuilder.FontStyle.NORMAL, true);` |
| **Huge files stall** | Rendering large HTML can be memory‑intensive. | Enable `builder.useFastMode()` (as shown) or split the markdown into sections and generate separate PDFs. |
| **Table styling looks off** | Flexmark’s default HTML lacks CSS for tables. | Add a small CSS snippet: `builder.withCssContent("table { width: 100%; border-collapse: collapse; } th, td { border: 1px solid #ddd; padding: 8px; }");` |

---

## Bonus: Adding a Simple Header/Footer

If you need page numbers or a title on every page, inject a little CSS and an HTML `<header>`/`<footer>` block.

```java
String headerFooterHtml = """
    <html>
    <head>
        <style>
            @page {
                margin: 1in;
                @bottom-center { content: "Page " counter(page)


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/english/java/configuring-environment/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}