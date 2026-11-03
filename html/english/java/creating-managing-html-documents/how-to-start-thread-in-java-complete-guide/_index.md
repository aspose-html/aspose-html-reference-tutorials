---
category: general
date: 2026-06-19
description: How to start thread in Java with a reusable Runnable, start multiple
  threads, print thread name, and parse HTML with Java. Step‑by‑step example.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: en
og_description: How to start thread in Java using Runnable, run multiple threads,
  print thread name, and parse HTML with Java in a single, runnable example.
og_title: How to start thread in Java – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: How to start thread in Java – Complete Guide
url: /java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to start thread in Java – Complete Guide

Ever wondered **how to start thread** in Java without drowning in boilerplate code? You're not the only one. Whether you're building a web crawler, a UI updater, or just need to off‑load a heavy calculation, mastering thread creation is a must‑have skill for any Java developer.

In this tutorial we’ll walk through a practical scenario: **parse HTML with Java**, print the current thread’s name, and **start multiple threads** that share the same logic. By the end you’ll know **how to use Runnable**, spin up several workers, and see the output you expect—all in a self‑contained example you can copy‑paste right now.

## What You’ll Learn

- The exact steps **how to start thread** using the `Thread` class and a `Runnable`.
- How to **start multiple threads** that execute the same task without duplicating code.
- The simplest way to **print thread name** alongside your processing results.
- A clean method to **parse HTML with Java** using a lightweight `HTMLDocument` helper (or any parser you prefer).
- Why **how to use runnable** matters for reusable, testable code.

No external libraries are required for the core example, but we’ll note where you might swap in Jsoup or another parser if you need more power.

---

## Step 1: Define a reusable task – **how to use runnable**

The first thing you need to know **how to use runnable** is to encapsulate the work you want each thread to perform. A `Runnable` is just a functional interface with a single `run()` method, which makes it perfect for lambda expressions.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Why this matters:** By keeping the logic inside a `Runnable`, you can hand it to any number of `Thread` objects, a thread pool, or even an executor service later on. This keeps your code DRY and testable.

---

## Step 2: **How to start thread** – create the first worker

Now that we have a `Runnable`, launching a thread is as easy as calling the `Thread` constructor. The **how to start thread** question is answered in a single line:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Notice the second argument, `"Worker-1"`. That name will appear when we later **print thread name**, making debugging far less cryptic.

---

## Step 3: **Start multiple threads** – reuse the same Runnable

Want to process several HTML files at once? Just spin up another `Thread` with the same `Runnable`. This demonstrates **start multiple threads** without copying the task code:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Both `Worker-1` and `Worker-2` will execute the block defined in `extractTextLength` concurrently. Because the task is stateless (it only reads a file), there’s no race condition to worry about.

---

## Step 4: **Print thread name** while parsing HTML

Inside the `Runnable` we already called `Thread.currentThread().getName()`. That’s the canonical way to **print thread name**. The output will look something like this (assuming the HTML body contains 1 234 characters):

```
Worker-1: 1234
Worker-2: 1234
```

If you run the program on a larger file, each line will show the same length because both threads read the same file. Change the path or pass the file name as a parameter to see different results.

---

## Step 5: Full, runnable example – from import to execution

Below is the complete, **self‑contained** program you can drop into a file named `HtmlThreadDemo.java`. It includes a tiny `HTMLDocument` stub so the code compiles even if you don’t have a real parser on hand. Replace the stub with Jsoup or any library you prefer for production use.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Expected output

Assuming `page.html` contains 2 567 characters inside its `<body>` tag, you’ll see something like:

```
Worker-1: 2567
Worker-2: 2567
```

If the file can’t be read, the stack trace will be printed—thanks to the `catch` block.

---

## Common Pitfalls & Pro Tips

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **File not found** | The path `"YOUR_DIRECTORY/page.html"` is relative to where you launch the JVM. | Use an absolute path or `Paths.get("").toAbsolutePath()` to debug. |
| **Race conditions** | If the `Runnable` mutates shared state, threads can clash. | Keep the task stateless, or synchronize access to shared objects. |
| **Too many threads** | Spawning dozens of `Thread`s can exhaust OS resources. | Switch to an `ExecutorService` with a bounded pool after you master the basics. |
| **Incorrect HTML parsing** | The stub `HTMLDocument` is simplistic; complex pages break. | Replace it with Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Extending the Example

Now that you know **how to start thread**, you might want to:

- **Parse different files** by passing the filename into the `Runnable` (use a constructor or a lambda that captures a variable).
- **Collect results** with a `ConcurrentLinkedQueue<Integer>` instead of just printing.
- **Leverage a thread pool** (`Executors.newFixedThreadPool(4)`) for better scalability.
- **Swap the parser** for Jsoup, HtmlUnit, or any library that fits your project's needs.

All of those steps still rely on the core idea we covered: define a reusable task, hand it to one or many threads, and observe which thread is doing the work by **print thread name**.

---

## Conclusion

We’ve covered **how to start thread** in Java, demonstrated **how to use runnable** for reusable work, shown you how to **start multiple threads**, and illustrated a simple way to **parse HTML with Java** while **print thread name** for each worker. The complete code snippet above is ready to run, and the concepts scale to more complex, production‑grade applications.

Feel free to experiment: change the file path, increase the number of workers, or plug in a real HTML parser. The fundamentals stay the same, and you now have a solid foundation for any multithreaded Java project.

Got questions about thread safety, executor services, or HTML parsing libraries? Drop a comment below, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}