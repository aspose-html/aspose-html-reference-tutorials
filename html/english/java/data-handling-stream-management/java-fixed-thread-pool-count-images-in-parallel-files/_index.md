---
category: general
date: 2026-02-10
description: Learn how to use a java fixed thread pool to count images in HTML files,
  run tasks concurrently java, and properly shutdown executor service.
draft: false
keywords:
- java fixed thread pool
- how to count images
- shutdown executor service
- java parallel file processing
- run tasks concurrently java
language: en
og_description: Master java fixed thread pool usage to count images, process files
  in parallel, and shut down executor service safely.
og_title: 'java fixed thread pool: Count Images in Parallel Files'
tags:
- Java
- Concurrency
- Aspose.HTML
title: 'java fixed thread pool: Count Images in Parallel Files'
url: /java/data-handling-stream-management/java-fixed-thread-pool-count-images-in-parallel-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java fixed thread pool – Parallel Image Counting Tutorial

Ever wondered how to **java fixed thread pool** your way through dozens of HTML files and get a quick image count? Maybe you’ve stared at a directory of pages, thought “I need to know how many `<img>` tags each file has”, and then realized a single‑threaded loop would take forever.  

The good news is you don’t need to write a custom thread manager or wrestle with low‑level `Thread` objects. In this guide we’ll show you exactly **how to count images** using a *java fixed thread pool*, run tasks concurrently java, and gracefully **shutdown executor service** when the work is done.  

We’ll cover everything from setting up the pool, preparing the file list, submitting parallel tasks, handling edge cases, to verifying the output. By the end you’ll have a ready‑to‑run program that demonstrates **java parallel file processing** in a clean, maintainable way.  

## Prerequisites

Before we dive in, make sure you have:

- Java 17 or newer (the code uses the `var` keyword for brevity, but you can downgrade if needed).
- Aspose.HTML for Java on your classpath – you can grab it from Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- A handful of HTML files you’d like to analyse (the tutorial assumes they live in `YOUR_DIRECTORY/`).
- An IDE or build tool you’re comfortable with – IntelliJ IDEA, VS Code, or plain `javac` works fine.

That’s it. No extra servers, no Docker, just plain Java and a tiny third‑party library.

## Step 1: Create a java fixed thread pool

A *java fixed thread pool* gives you a bounded set of worker threads that reuse themselves for every submitted task. This prevents the overhead of constantly creating new threads and caps the concurrency level, which is crucial when you’re reading files from disk.

```java
import java.util.concurrent.*;

public class ParallelImageCounter {
    // A pool of 4 threads – adjust based on your CPU cores and I/O profile
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);
}
```

**Why 4?** If you have a quad‑core laptop, four threads keep each core busy without oversubscribing. On a server with more cores you can bump the number up, but remember that each thread will open a file handle, so too many may exhaust OS limits.

## Step 2: List the HTML files you want to analyse

The next piece of **java parallel file processing** is simply building an array (or `List`) of file paths. In a real project you might walk a directory recursively, filter by extension, or read paths from a database. Here’s the straightforward approach:

```java
String[] htmlFiles = {
    "YOUR_DIRECTORY/a.html",
    "YOUR_DIRECTORY/b.html",
    "YOUR_DIRECTORY/c.html",
    "YOUR_DIRECTORY/d.html"
};
```

If you need to handle a dynamic set, replace the static array with something like:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
String[] htmlFiles = Files.list(dir)
                         .filter(p -> p.toString().endsWith(".html"))
                         .map(Path::toString)
                         .toArray(String[]::new);
```

That snippet demonstrates **java parallel file processing** for any number of files without changing the rest of the code.

## Step 3: Submit tasks to **run tasks concurrently java**

Now comes the heart of the tutorial – we’ll **run tasks concurrently java** by submitting a lambda for each file. Each task loads the HTML document with Aspose.HTML, queries all `<img>` elements, and prints the count.

```java
import com.aspose.html.HTMLDocument;

public static void main(String[] args) throws InterruptedException {
    for (String filePath : htmlFiles) {
        executor.submit(() -> {
            // Load the document – Aspose.HTML does the heavy lifting
            HTMLDocument document = new HTMLDocument(filePath);
            // querySelectorAll returns a NodeList; its length is the image count
            int imageCount = document.querySelectorAll("img").length;
            System.out.println(filePath + " contains " + imageCount + " images.");
        });
    }

    // Step 4 is next – gracefully shut down the pool
    shutdownAndAwaitTermination();
}
```

**Why use a lambda?** It keeps the code concise and avoids creating a separate `Runnable` class. The lambda captures `filePath` automatically, so each task works on its own file.

### How to **count images** efficiently

Aspose.HTML parses the file once, builds a DOM, and then `querySelectorAll("img")` runs in O(n) where *n* is the number of nodes. For most HTML pages this is negligible. If you needed a faster, streaming‑only approach (e.g., for gigabyte‑size files), you could switch to a SAX parser, but that would sacrifice the simplicity we’re aiming for.

## Step 4: Properly **shutdown executor service**

Never forget to shut down the pool, or your JVM will keep running forever. The pattern below is the recommended way to **shutdown executor service** while waiting for all tasks to finish:

```java
private static void shutdownAndAwaitTermination() {
    executor.shutdown(); // Disable new tasks from being submitted
    try {
        // Wait a while for existing tasks to terminate
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            executor.shutdownNow(); // Cancel currently executing tasks
            // Wait a second for tasks to respond to being cancelled
            if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                System.err.println("Pool did not terminate");
        }
    } catch (InterruptedException ie) {
        // (Re-)Cancel if current thread also interrupted
        executor.shutdownNow();
        // Preserve interrupt status
        Thread.currentThread().interrupt();
    }
}
```

**What if a task hangs?** The `shutdownNow()` call attempts to interrupt running threads. If your image‑counting logic respects interruption (which Aspose.HTML does not block on I/O), the pool will terminate cleanly. This pattern is the gold standard for any **java fixed thread pool** usage.

## Step 5: Verify the output

Run the program from your IDE or via the command line:

```bash
javac -cp "path/to/aspose-html.jar" ParallelImageCounter.java
java -cp ".:path/to/aspose-html.jar" ParallelImageCounter
```

Typical output looks like:

```
YOUR_DIRECTORY/a.html contains 5 images.
YOUR_DIRECTORY/b.html contains 0 images.
YOUR_DIRECTORY/c.html contains 12 images.
YOUR_DIRECTORY/d.html contains 3 images.
```

If you see the counts printed in any order, that’s expected – threads finish at different times. The important thing is that every file is accounted for and the program exits cleanly after the shutdown sequence.

## Full Working Example (Copy‑Paste Ready)

```java
import com.aspose.html.HTMLDocument;
import java.util.concurrent.*;

public class ParallelImageCounter {
    // 1️⃣ Fixed thread pool – change size based on your hardware
    private static final ExecutorService executor = Executors.newFixedThreadPool(4);

    public static void main(String[] args) throws InterruptedException {
        // 2️⃣ List of HTML files – replace with your own directory
        String[] htmlFiles = {
            "YOUR_DIRECTORY/a.html",
            "YOUR_DIRECTORY/b.html",
            "YOUR_DIRECTORY/c.html",
            "YOUR_DIRECTORY/d.html"
        };

        // 3️⃣ Submit a counting task for each file
        for (String filePath : htmlFiles) {
            executor.submit(() -> {
                HTMLDocument document = new HTMLDocument(filePath);
                int imageCount = document.querySelectorAll("img").length;
                System.out.println(filePath + " contains " + imageCount + " images.");
            });
        }

        // 4️⃣ Gracefully shut down the pool
        shutdownAndAwaitTermination();
    }

    // 5️⃣ Helper method to cleanly stop the executor
    private static void shutdownAndAwaitTermination() {
        executor.shutdown(); // Disable new tasks
        try {
            if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
                executor.shutdownNow(); // Cancel currently executing tasks
                if (!executor.awaitTermination(30, TimeUnit.SECONDS))
                    System.err.println("Pool did not terminate");
            }
        } catch (InterruptedException ie) {
            executor.shutdownNow();
            Thread.currentThread().interrupt();
        }
    }
}
```

### Expected Result

Running the snippet prints each file path followed by the number of `<img>` tags it contains, then the JVM exits. No lingering threads, no memory leaks.

## Common Pitfalls & Pro Tips

- **Pitfall:** Using `newCachedThreadPool()` instead of a *fixed* pool. That creates unbounded threads, which can exhaust file descriptors on large batches. Stick with `newFixedThreadPool`.
- **Pro tip:** If your HTML files are huge, consider increasing the heap (`-Xmx2g`) or switching to a streaming parser. For most marketing pages, the default heap is fine.
- **Pitfall:** Forgetting to call `shutdown()` – your app will hang after printing results. The `shutdownAndAwaitTermination` method above handles it robustly.
- **Pro tip:** Log the start and end time of each task if you need performance metrics. Simple `System.nanoTime()` before and after the `HTMLDocument` construction tells you how long the parse took.
- **Pitfall:** Hard‑coding the thread count. Use `Runtime.getRuntime().availableProcessors()` to pick a sensible default:

```java
int cores = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(cores);
```

## Related Topics You Might Explore Next

- **run tasks concurrently java** with `CompletableFuture` for more expressive pipelines.
- Persisting image counts to a database for analytics dashboards.
- Using **java parallel file processing** with the `java.nio.file.Files.walk` API combined with streams.
- Implementing a custom `ThreadFactory` to give threads meaningful names (helps debugging).

## Conclusion

We’ve just walked through a complete, self‑contained example that shows how a **java fixed thread pool** can be leveraged to **how to count images** across multiple HTML files, while also demonstrating the proper way to **shutdown executor service**. The pattern scales nicely—swap the file array for a dynamic list, bump the pool size, and you’ve got a robust solution for any **java parallel file processing** workload.  

Give it a spin, tweak the thread count, and maybe add a CSV export of the results. The sky’s the limit when you combine a solid concurrency foundation with a handy library like Aspose.HTML. Happy coding!  

![java fixed thread pool diagram](image.png){alt="java fixed thread pool diagram"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}