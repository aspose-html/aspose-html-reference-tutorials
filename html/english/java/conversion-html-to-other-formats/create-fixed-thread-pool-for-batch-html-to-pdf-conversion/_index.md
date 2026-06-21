---
category: general
date: 2026-02-22
description: Create fixed thread pool to efficiently batch HTML to PDF conversion
  in Java. Learn a thread pool Java example that saves HTML as PDF quickly.
draft: false
keywords:
- create fixed thread pool
- convert html to pdf
- batch html to pdf
- thread pool java example
- save html as pdf
language: en
og_description: Create fixed thread pool to batch HTML to PDF conversion. This guide
  walks you through a thread pool Java example that saves HTML as PDF efficiently.
og_title: Create Fixed Thread Pool for Batch HTML to PDF Conversion
tags:
- Java
- Concurrency
- PDF Generation
title: Create Fixed Thread Pool for Batch HTML to PDF Conversion
url: /java/conversion-html-to-other-formats/create-fixed-thread-pool-for-batch-html-to-pdf-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Fixed Thread Pool for Batch HTML to PDF Conversion

Ever wondered how to **create fixed thread pool** that turns a pile of HTML files into PDFs without choking your CPU? You're not the only one. When you have dozens—or even hundreds—of pages to process, running them one‑by‑one is a drag, but firing up an unbounded thread pool can quickly exhaust memory.  

In this tutorial we’ll solve that dilemma by showing you a **thread pool Java example** that **batch HTML to PDF**, saves each result, and shuts down cleanly. By the end you’ll be able to **convert HTML to PDF** in parallel, and you’ll understand why a fixed thread pool is the sweet spot for most batch jobs.

## What You’ll Walk Away With

- A complete, runnable Java program that creates a fixed thread pool.
- Step‑by‑step explanation of each line, so you know **why** we do what we do.
- Guidance on picking a PDF library (so you can **save HTML as PDF** without hunting for code snippets).
- Tips for handling errors, tweaking pool size, and extending the solution to larger batches.

**Prerequisites** – Java 8+ installed, a basic IDE (IntelliJ, Eclipse, or VS Code), and a PDF conversion library on your classpath (we’ll use *OpenHTMLtoPDF* in the example). No other frameworks required.

---

## Create Fixed Thread Pool – Why It Matters

When you **create fixed thread pool**, you tell the JVM exactly how many worker threads are allowed to run concurrently. This prevents thread‑creation storms, keeps memory usage predictable, and lets the OS schedule work efficiently.  

Think of it like a checkout lane at a grocery store: you open a set number of lanes, let customers line up, and close the lanes when the line disappears. A `FixedThreadPool` works the same way—tasks wait their turn, but no extra threads are spawned on the fly.

```java
// Step 1: Build a fixed‑size thread pool with 4 workers
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

The number `4` is a good starting point on a quad‑core laptop; you can adjust it based on your CPU cores and I/O characteristics.

## Batch HTML to PDF: Converting Each Page

Now that the pool exists, we need to feed it tasks that **convert HTML to PDF**. Each task will:

1. Load an HTML document from disk.
2. Hand it off to the PDF library.
3. Write the resulting PDF back to the same directory.

Because the work is I/O‑heavy (reading files, writing PDFs), a small pool often outperforms a larger one that just sits idle waiting for the disk.

```java
// Step 2: Submit a conversion job for every HTML file you have
for (int i = 0; i < 4; i++) {
    final int pageIndex = i;               // capture loop variable for the lambda
    threadPool.submit(() -> {
        // Load the HTML file
        Path htmlPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".html");
        String html = Files.readString(htmlPath, StandardCharsets.UTF_8);

        // Convert and save as PDF
        Path pdfPath = Paths.get("YOUR_DIRECTORY/page" + pageIndex + ".pdf");
        convertHtmlToPdf(html, pdfPath);
    });
}
```

> **Pro tip:** If you have more than four pages, just increase the loop bound or read the file list dynamically—`Files.list(Paths.get("YOUR_DIRECTORY")).filter(p -> p.toString().endsWith(".html"))` makes it painless.

## Thread Pool Java Example Explained

Let’s unpack the **thread pool Java example** line by line so you’re not just copying code, but actually understanding the flow.

| Line | What It Does | Why It’s Important |
|------|--------------|--------------------|
| `ExecutorService threadPool = Executors.newFixedThreadPool(4);` | Instantiates a pool with exactly four threads. | Guarantees a bounded number of concurrent conversions, avoiding out‑of‑memory errors. |
| `for (int i = 0; i < 4; i++) { … }` | Iterates over the pages you want to process. | The loop drives task creation; you can replace the static bound with a dynamic list. |
| `final int pageIndex = i;` | Captures the loop index for use inside the lambda. | Without `final` (or effectively final) the lambda would see a changing variable, leading to wrong file names. |
| `threadPool.submit(() -> { … });` | Hands a `Runnable` to the pool for asynchronous execution. | The pool schedules the runnable on an idle worker thread, freeing the main thread to continue queuing work. |
| `Files.readString(htmlPath, …);` | Reads the HTML file into a `String`. | Needed because most PDF libraries accept HTML as a string or stream. |
| `convertHtmlToPdf(html, pdfPath);` | Calls a helper method that does the actual conversion. | Keeps the lambda tidy and isolates library‑specific code. |

Below is the full helper method using **OpenHTMLtoPDF**, a lightweight library that **save HTML as PDF** with a single call.

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

private static void convertHtmlToPdf(String html, Path outputPdf) throws IOException {
    try (OutputStream os = Files.newOutputStream(outputPdf)) {
        PdfRendererBuilder builder = new PdfRendererBuilder();
        builder.withHtmlContent(html, null);     // base URI is null because we use absolute paths
        builder.toStream(os);
        builder.run();                           // blocks until PDF is written
    } catch (Exception e) {
        // Wrap any checked exception as an unchecked one so the lambda can compile
        throw new RuntimeException("Failed to convert HTML to PDF for " + outputPdf, e);
    }
}
```

> **Why OpenHTMLtoPDF?** It’s pure Java, no native dependencies, and it respects CSS, which makes the resulting PDFs look much like the original web pages. If you prefer iText or Flying Saucer, just swap the implementation inside `convertHtmlToPdf`.

## Save HTML as PDF – Choosing a Library

You might ask, “Which library should I **convert HTML to PDF** with?” Here’s a quick comparison:

| Library | Maven Coordinates | Pros | Cons |
|---------|-------------------|------|------|
| OpenHTMLtoPDF | `com.openhtmltopdf:openhtmltopdf-pdfbox:1.0.10` | Pure Java, good CSS support, lightweight | Limited advanced PDF features (e.g., encryption) |
| iText 7 + html2pdf | `com.itextpdf:html2pdf:3.0.6` | Rich feature set, commercial support | Requires a paid license for many use‑cases |
| Flying Saucer | `org.xhtmlrenderer:flying-saucer-pdf:9.1.22` | Mature, works with older Java versions | Slower on large documents, less CSS coverage |

Pick the one that matches your project’s needs. For a **batch HTML to PDF** job, OpenHTMLtoPDF usually hits the sweet spot: fast, simple, and free.

## Graceful Shutdown and Error Handling

Leaving the executor running can prevent your JVM from exiting, and uncaught exceptions inside a thread can be hard to spot. The following pattern ensures a tidy shutdown:

```java
// Step 5: Initiate an orderly shutdown after all tasks are queued
threadPool.shutdown();                     // No new tasks accepted
try {
    // Wait up to 60 seconds for existing tasks to finish
    if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
        threadPool.shutdownNow();          // Force shutdown if tasks linger
    }
} catch (InterruptedException ex) {
    threadPool.shutdownNow();              // Preserve interrupt status
    Thread.currentThread().interrupt();
}
```

- `shutdown()` tells the pool to finish what it’s doing but reject new work.
- `awaitTermination` blocks until either everything finishes or the timeout expires.
- `shutdownNow()` attempts to cancel running tasks—useful for a forced stop.

If any conversion fails, the `RuntimeException` we threw bubbles up to the executor, which logs it to the console by default. In production you’d attach a custom `ThreadPoolExecutor` with an overridden `afterExecute` method to log to a file or monitoring system.

## Full Working Example

Putting it all together, here’s a self‑contained Java class you can copy‑paste into `src/main/java/com/example/BatchPdfConverter.java`. Make sure the OpenHTMLtoPDF dependency is on your classpath.

```java
package com.example;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;
import java.util.concurrent.*;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;

/**
 * Demonstrates how to create a fixed thread pool to batch HTML to PDF conversion.
 * Adjust POOL_SIZE and DIRECTORY constants to fit your environment.
 */
public class BatchPdfConverter {

    private static final int POOL_SIZE = 4;                     // Number of parallel workers
    private static final Path DIRECTORY = Paths.get("YOUR_DIRECTORY"); // Change to your folder

    public static void main(String[] args) {
        ExecutorService threadPool = Executors.newFixedThreadPool(POOL_SIZE);

        // Discover all *.html files in the target directory
        try (DirectoryStream<Path> stream = Files.newDirectoryStream(DIRECTORY, "*.html")) {
            for (Path htmlPath : stream) {
                threadPool.submit(() -> processFile(htmlPath));
            }
        } catch (IOException e) {
            System.err.println("Failed to list HTML files: " + e.getMessage());
        }

        // Graceful shutdown
        thread

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}