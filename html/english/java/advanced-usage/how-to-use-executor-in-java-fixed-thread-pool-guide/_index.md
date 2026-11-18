---
category: general
date: 2026-05-28
description: how to use executor in Java with a fixed thread pool, extract text from
  HTML and speed up processing – a complete java thread pool example.
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: en
og_description: how to use executor in Java with a fixed thread pool. Learn a complete
  java thread pool example that extracts text from HTML files efficiently.
og_title: How to Use Executor in Java – Fixed Thread Pool Guide
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: how to use executor in Java with a fixed thread pool, extract text
    from HTML and speed up processing – a complete java thread pool example.
  headline: How to Use Executor in Java – Fixed Thread Pool Guide
  type: TechArticle
tags:
- Java
- Concurrency
- HTML Parsing
title: How to Use Executor in Java – Fixed Thread Pool Guide
url: /java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use Executor in Java – Fixed Thread Pool Guide

Ever wondered **how to use executor** to run many tasks at once without blowing up your memory? You’re not alone. In many real‑world apps you’ll need to crawl a folder of HTML files, pull out the body text, and do it fast—exactly the scenario this tutorial solves.

We’ll walk through a **fixed thread pool java** implementation that extracts text from HTML, prints each file’s character count, and shuts down cleanly. By the end you’ll have a self‑contained **java thread pool example** you can drop into any project, plus a few tips on customizing the pool size and handling edge cases.

> **What you’ll need**  
> * Java 17 (or any recent JDK)  
> * A tiny HTML‑parsing library – we’ll use *jsoup* because it’s battle‑tested and zero‑config.  
> * A handful of sample *.html* files in a directory of your choice.

---

## How to Use Executor with a Fixed Thread Pool

The heart of any concurrency‑heavy Java program is the `ExecutorService`. By creating a **fixed thread pool** we tell the JVM to keep exactly N worker threads alive, which prevents thread‑creation overhead and caps resource usage.

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Why this matters:*  
If you launched a new `Thread` for every HTML file, the OS would have to schedule dozens of threads on a modest laptop, leading to context‑switch thrashing. A fixed pool reuses the same four threads, giving you predictable CPU usage.

---

## Define the HTML Files to Process – Fixed Thread Pool Java

Next we list the files we want to feed into the pool. In a real app you’d probably walk a directory tree; here we keep it simple.

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*Tip:* `List.of` returns an immutable list, which is safe to share across threads without extra synchronization.

---

## Submit a Separate Task for Each HTML File

Now we hand each path to the executor. The lambda we submit will run **in parallel** on one of the four worker threads.

```java
// Step 3: Dispatch a parsing job for every file
for (String htmlFilePath : htmlFilePaths) {
    executor.submit(() -> {
        // Each lambda runs on a thread from the pool
        try {
            // Step 4: Open the document, extract its text, and display the length
            String text = extractBodyText(htmlFilePath);
            System.out.println(htmlFilePath + " → " + text.length() + " chars");
        } catch (IOException e) {
            System.err.println("Failed to read " + htmlFilePath);
            e.printStackTrace();
        }
    });
}
```

**Why we wrap the logic in a method** (`extractBodyText`) will become clear in the next section—it keeps the lambda tidy and lets us reuse the extraction code elsewhere.

---

## Extract Text from HTML – The Core Logic

Here’s the reusable helper that actually **extracts text from html** using Jsoup. It opens the file, parses the DOM, and returns the plain body text.

```java
/**
 * Reads an HTML file and returns the plain text inside the <body>.
 *
 * @param path absolute or relative path to the .html file
 * @return body text without tags
 * @throws IOException if the file cannot be read
 */
private static String extractBodyText(String path) throws IOException {
    // Jsoup parses the file into a Document object.
    org.jsoup.nodes.Document doc = org.jsoup.Jsoup.parse(new java.io.File(path), "UTF-8");
    // getBody() gives us the <body> element; text() strips all tags.
    return doc.body().text();
}
```

*Why Jsoup?* It’s lightweight, handles malformed markup gracefully, and doesn’t require a full browser engine. The method throws `IOException` so the caller can decide how to log or recover—perfect for a thread‑pool scenario where you don’t want a single bad file to terminate the whole executor.

---

## Gracefully Shut Down the Executor – Create Fixed Thread Pool

After we’ve submitted every job, we must tell the pool to stop accepting new work and to finish what’s already queued.

```java
// Step 5: Initiate an orderly shutdown once all tasks are queued
executor.shutdown();
try {
    // Wait up to 30 seconds for all tasks to finish
    if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
        System.err.println("Timed out waiting for tasks; forcing shutdown.");
        executor.shutdownNow();
    }
} catch (InterruptedException ie) {
    // Preserve interrupt status and force shutdown
    Thread.currentThread().interrupt();
    executor.shutdownNow();
}
```

*Explanation:* `shutdown()` prevents new submissions, while `awaitTermination` blocks until every parsing job ends (or the timeout expires). If something hangs, `shutdownNow()` attempts to cancel running tasks. This pattern is the recommended way to **create fixed thread pool** safely.

---

## Full, Runnable Example

Putting everything together, here’s a single file you can compile and run. It includes the necessary imports, the `main` method, and the helper described above.

```java
import java.io.IOException;
import java.util.List;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

/**
 * Demonstrates how to use executor with a fixed thread pool to
 * extract text from multiple HTML files concurrently.
 */
public class HtmlThreadPoolDemo {

    public static void main(String[] args) {
        // 1️⃣ Build a fixed‑size pool (adjust the size for your hardware)
        ExecutorService executor = Executors.newFixedThreadPool(4);

        // 2️⃣ Define the files we want to process
        List<String> htmlFilePaths = List.of(
                "YOUR_DIRECTORY/a.html",
                "YOUR_DIRECTORY/b.html",
                "YOUR_DIRECTORY/c.html",
                "YOUR_DIRECTORY/d.html"
        );

        // 3️⃣ Submit a parsing task for each file
        for (String htmlFilePath : htmlFilePaths) {
            executor.submit(() -> {
                try {
                    String text = extractBodyText(htmlFilePath);
                    System.out.println(htmlFilePath + " → " + text.length() + " chars");
                } catch (IOException e) {
                    System.err.println("Error processing " + htmlFilePath);
                    e.printStackTrace();
                }
            });
        }

        // 5️⃣ Shut down the pool cleanly
        executor.shutdown();
        try {
            if (!executor.awaitTermination(30, java.util.concurrent.TimeUnit.SECONDS)) {
                System.err.println("Tasks took too long; forcing shutdown.");
                executor.shutdownNow();
            }
        } catch (InterruptedException ie) {
            Thread.currentThread().interrupt();
            executor.shutdownNow();
        }
    }

    /**
     * Reads an HTML file and returns the plain text inside the <body>.
     *
     * @param path path to the .html file
     * @return body text without markup
     * @throws IOException if file cannot be read
     */
    private static String extractBodyText(String path) throws IOException {
        Document doc = Jsoup.parse(new java.io.File(path), "UTF-8");
        return doc.body().text();
    }
}
```

**Expected output** (assuming each file contains roughly 1 200 characters of body text):

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

If any file is missing or malformed, you’ll see a stack trace printed to `stderr`, but the other tasks will continue unaffected—exactly what a well‑behaved **java thread pool example** should do.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if I have more than four files?* | The pool will queue the extra tasks and run them as soon as a thread becomes free. No extra code needed. |
| *Should I use `newCachedThreadPool` instead?* | `newCachedThreadPool` creates threads on demand and can grow unbounded, which is risky for I/O‑heavy jobs. A **fixed thread pool** gives you predictable memory and CPU usage. |
| *How do I change the pool size based on CPU cores?* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` is a common pattern. |
| *What if parsing fails for one file?* | The `catch (IOException e)` inside the lambda isolates the failure, logs it, and lets the rest of the pool keep working. |
| *Can I return the extracted text to the caller?* | Yes—use `Future<String>` instead of `submit(Runnable)`. The code would look like `Future<String> f = executor.submit(() -> extractBodyText(path));` and later `String result = f.get();`. |

---

## Conclusion

We’ve covered **how to use executor** to spin up a **fixed thread pool java** that processes a collection of HTML files in parallel, extracts their body text, and reports the character count. The complete **java thread pool example** demonstrates proper resource management, error handling, and a reusable extraction method.

Next steps? Try swapping the `extractBodyText` implementation for a more sophisticated scraper, experiment with a larger pool size, or feed the results into a database. You could also explore `CompletionService` to retrieve results as soon as they’re ready, which is handy when file sizes vary widely.

Feel free to tweak the directory path, add more files, or integrate this snippet into a larger crawling framework. The core pattern—create a pool, submit independent tasks, and shut down gracefully—remains the same, no matter how complex your workload gets.

Happy coding, and may your threads always stay alive (until you shut them down, of course)!


## Related Tutorials

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Use Aspose.HTML for Java - Mastering HTML5 Canvas Rendering](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}