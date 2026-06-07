---
category: general
date: 2026-06-07
description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
  convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
draft: false
keywords:
- convert html to pdf
- save html document as pdf
- shutdown executorservice gracefully
- batch convert html to pdf
language: en
og_description: Convert HTML to PDF using Java's ExecutorService. Master batch conversion,
  saving HTML document as PDF, and graceful shutdown of ExecutorService.
og_title: Convert HTML to PDF with Java – Parallel Batch Guide
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  headline: Convert HTML to PDF with Java – Parallel Batch Guide
  type: TechArticle
- description: Convert HTML to PDF using Java's ExecutorService. Learn how to batch
    convert HTML files, save HTML document as PDF, and shutdown ExecutorService gracefully.
  name: Convert HTML to PDF with Java – Parallel Batch Guide
  steps:
  - name: The HTML file is read into a string.
    text: The HTML file is read into a string.
  - name: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
    text: '`PdfRendererBuilder` parses the markup, applies CSS, and streams the result
      to a PDF file.'
  - name: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
    text: Any `IOException` bubbles up to `convertAndSave`, where we log success or
      failure.
  type: HowTo
tags:
- Java
- Concurrency
- PDF Generation
title: Convert HTML to PDF with Java – Parallel Batch Guide
url: /java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-parallel-batch-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to PDF with Java – Parallel Batch Guide

Ever needed to **convert HTML to PDF** but felt stuck juggling dozens of files? You're not the only one—many devs hit that wall when building report generators or invoice exporters. The good news? With a few lines of Java and a smart thread pool, you can **batch convert HTML to PDF** in a snap, **save HTML document as PDF**, and even **shutdown ExecutorService gracefully** when the work’s done.

In this tutorial we’ll walk through a complete, ready‑to‑run example. You’ll see why a fixed‑size thread pool is the sweet spot for parallel conversion, how the conversion code itself looks, and the exact steps to cleanly terminate the executor. By the end, you’ll have a self‑contained program you can drop into any project—no missing pieces, no vague “see docs” links.

---

## What You’ll Build

- A Java console app that reads a list of local HTML files.  
- Each file is handed off to a worker thread that creates a PDF version.  
- The app uses **ExecutorService** to run conversions in parallel.  
- Once every task is queued, the pool is **shutdown gracefully**, ensuring no thread is left hanging.

**Prerequisites**  
- Java 17 (or any recent JDK).  
- A PDF library that can render HTML, such as **OpenHTMLtoPDF**, **iText**, or **Flying Saucer**. In the code we’ll reference a placeholder `HTMLDocument` class; swap it with your library’s API.  
- Basic knowledge of Java concurrency (nothing fancy).

---

![Diagram showing batch conversion of HTML files to PDF using ExecutorService](batch-convert-diagram.png "Convert HTML to PDF in parallel with ExecutorService")

*Alt text: Diagram illustrating how to convert HTML to PDF using a thread pool for batch processing.*

---

## Convert HTML to PDF in Parallel (Batch Convert HTML to PDF)

When you have dozens—or even thousands—of HTML files, converting them one‑by‑one on the main thread becomes a bottleneck. A fixed‑size thread pool lets the JVM reuse a set number of worker threads, keeping CPU usage high without overwhelming the system.

```java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * Simple demo that batch converts HTML files to PDF using a fixed thread pool.
 * Replace HTMLDocument with the actual class from your chosen PDF library.
 */
public class HtmlToPdfBatch {

    public static void main(String[] args) {
        // 1️⃣ Prepare a list of HTML files to convert
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        // 2️⃣ Create a fixed‑size thread pool – 4 workers is a good starting point
        ExecutorService pool = Executors.newFixedThreadPool(4);

        // 3️⃣ Submit a conversion task for each HTML file
        for (String htmlPath : htmlPaths) {
            pool.submit(() -> convertAndSave(htmlPath));
        }

        // 4️⃣ Shutdown ExecutorService gracefully – no new tasks, wait for running ones
        shutdownGracefully(pool);
    }

    /**
     * Core conversion logic – this is where we **save HTML document as PDF**.
     */
    private static void convertAndSave(String htmlPath) {
        try {
            // Imagine HTMLDocument is from OpenHTMLtoPDF, iText, etc.
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    /**
     * Helper that **shutdowns ExecutorService gracefully**.
     */
    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown(); // stop accepting new tasks
        try {
            // Wait a maximum of 60 seconds for existing tasks to finish
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow(); // cancel currently executing tasks
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            // Preserve interrupt status & force shutdown
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}
```

### Why This Works

- **Parallelism**: Each `submit` call hands the conversion to a worker thread, so four files can be processed simultaneously on a quad‑core machine.  
- **Isolation**: The `convertAndSave` method contains all the logic needed to **save HTML document as PDF**, making it easy to swap the underlying library later.  
- **Graceful termination**: By calling `shutdown()` first, we tell the pool “no more work, please finish what you have.” The `awaitTermination` loop gives those threads a chance to wrap up, and only if they’re stubborn do we invoke `shutdownNow()`. This pattern is the recommended way to **shutdown ExecutorService gracefully**.

---

## Save HTML Document as PDF – Core Conversion Logic

The heart of any **convert HTML to PDF** workflow is the conversion library. While the example uses a dummy `HTMLDocument`, here’s a quick peek at how you might do it with **OpenHTMLtoPDF**:

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HTMLDocument {
    private final String htmlPath;

    public HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    public void save(String pdfPath) throws IOException {
        try (OutputStream os = new FileOutputStream(pdfPath);
             InputStream is = new FileInputStream(htmlPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os);
            builder.run();
        }
    }
}
```

**What’s happening?**  
1. The HTML file is read into a string.  
2. `PdfRendererBuilder` parses the markup, applies CSS, and streams the result to a PDF file.  
3. Any `IOException` bubbles up to `convertAndSave`, where we log success or failure.

Feel free to replace this snippet with iText’s `HtmlConverter.convertToPdf` or Flying Saucer’s `ITextRenderer`. The surrounding thread‑pool code stays exactly the same, which is why we emphasized **save HTML document as PDF** as a separate concern.

---

## Shutdown ExecutorService Gracefully – Best Practices

A common pitfall is calling `shutdownNow()` immediately after submitting tasks. That abruptly interrupts threads, potentially leaving half‑written PDF files on disk. The pattern we used—`shutdown()` → `awaitTermination()` → optional `shutdownNow()`—ensures:

- **No new tasks** are accepted after you’ve queued everything.  
- **Running tasks** get a chance to finish cleanly.  
- **Blocked threads** are only interrupted if they exceed a reasonable timeout (here, 60 seconds).  

If you expect very large PDFs or a slow rendering engine, bump the timeout or use `executor.invokeAll(tasks, timeout, unit)` for tighter control.

---

## Full Working Example (All Pieces Together)

Below is the entire program you can copy‑paste into a single `HtmlToPdfBatch.java` file. Just add the OpenHTMLtoPDF dependency (or your preferred library) to your `pom.xml` or Gradle build, and you’re good to go.

```java
// HtmlToPdfBatch.java
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HtmlToPdfBatch {

    public static void main(String[] args) {
        List<String> htmlPaths = List.of(
            "src/main/resources/page1.html",
            "src/main/resources/page2.html",
            "src/main/resources/page3.html"
        );

        ExecutorService pool = Executors.newFixedThreadPool(4);
        for (String path : htmlPaths) {
            pool.submit(() -> convertAndSave(path));
        }
        shutdownGracefully(pool);
    }

    private static void convertAndSave(String htmlPath) {
        try {
            HTMLDocument doc = new HTMLDocument(htmlPath);
            String pdfPath = htmlPath.replace(".html", ".pdf");
            doc.save(pdfPath);
            System.out.println("✅ Converted: " + htmlPath + " → " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Failed to convert " + htmlPath + ": " + e.getMessage());
        }
    }

    private static void shutdownGracefully(ExecutorService executor) {
        executor.shutdown();
        try {
            if (!executor.awaitTermination(60, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("⚠️ Pool didn’t terminate in time – forcing shutdown");
                executor.shutdownNow();
            } else {
                System.out.println("🛑 All tasks completed – executor shut down cleanly.");
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }
}

// Helper class – replace with your real PDF library calls
class HTMLDocument {
    private final String htmlPath;

    HTMLDocument(String htmlPath) {
        this.htmlPath = htmlPath;
    }

    void save(String pdfPath) throws IOException {
        try (InputStream is = new FileInputStream(htmlPath);
             OutputStream os = new FileOutputStream(pdfPath)) {

            PdfRendererBuilder builder = new PdfRendererBuilder();
            builder.withHtmlContent(new String(is.readAllBytes()), null);
            builder.toStream(os


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/english/java/configuring-environment/)
- [Convert HTML to PDF in Java – Step‑by‑Step Guide with Page Size Settings](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}