---
category: general
date: 2026-05-28
description: 如何在 Java 中使用固定线程池的 Executor，从 HTML 中提取文本并加速处理——完整的 Java 线程池示例。
draft: false
keywords:
- how to use executor
- fixed thread pool java
- extract text from html
- java thread pool example
- create fixed thread pool
language: zh
og_description: 如何在 Java 中使用固定线程池的 Executor。学习一个完整的 Java 线程池示例，高效地从 HTML 文件中提取文本。
og_title: 如何在 Java 中使用 Executor – 固定线程池指南
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
title: 如何在 Java 中使用 Executor – 固定线程池指南
url: /zh/java/advanced-usage/how-to-use-executor-in-java-fixed-thread-pool-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Executor – 固定线程池指南

有没有想过 **如何使用 executor** 来一次运行大量任务而不耗尽内存？你并不孤单。在许多真实场景的应用中，你需要遍历一个 HTML 文件夹，提取正文文本，并且要快速完成——这正是本教程要解决的情形。

我们将逐步演示一个 **fixed thread pool java** 实现，它从 HTML 中提取文本，打印每个文件的字符数，并且干净地关闭。完成后，你将拥有一个可直接放入任何项目的 **java thread pool example**，以及一些关于自定义线程池大小和处理边缘情况的技巧。

> **你需要的条件**  
> * Java 17（或任何近期的 JDK）  
> * 一个轻量级的 HTML 解析库——我们将使用 *jsoup*，因为它经过实战检验且零配置。  
> * 若干示例 *.html* 文件，放在你选择的目录中。

---

## 使用固定线程池的 Executor 方法

任何并发密集的 Java 程序的核心都是 `ExecutorService`。通过创建 **fixed thread pool**，我们告诉 JVM 恰好保持 N 个工作线程存活，从而避免线程创建开销并限制资源使用。

```java
// Step 1: Build a fixed‑size thread pool (4 workers in this case)
ExecutorService executor = Executors.newFixedThreadPool(4);
```

*为什么这很重要：*  
如果为每个 HTML 文件启动一个新的 `Thread`，操作系统需要在普通笔记本上调度数十个线程，导致上下文切换频繁。固定线程池会复用同样的四个线程，让 CPU 使用更可预测。

## 定义要处理的 HTML 文件 – Fixed Thread Pool Java

接下来我们列出要提交给线程池的文件。在真实的应用中，你可能会遍历目录树；这里我们保持简单。

```java
// Step 2: List the HTML documents you want to parse
List<String> htmlFilePaths = List.of(
        "YOUR_DIRECTORY/a.html",
        "YOUR_DIRECTORY/b.html",
        "YOUR_DIRECTORY/c.html",
        "YOUR_DIRECTORY/d.html"
);
```

*提示：* `List.of` 返回不可变列表，可安全地在多个线程间共享，无需额外同步。

## 为每个 HTML 文件提交单独任务

现在我们把每个路径交给 executor。我们提交的 lambda 将在四个工作线程中的一个上 **并行** 运行。

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

**为什么要把逻辑封装到方法中**（`extractBodyText`），在下一节会更清楚——它让 lambda 更简洁，并且可以在其他地方复用提取代码。

## 从 HTML 中提取文本 – 核心逻辑

下面是可复用的辅助方法，使用 Jsoup 实际 **从 html 中提取文本**。它打开文件，解析 DOM，并返回纯正文文本。

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

*为什么选择 Jsoup？* 它轻量、能够优雅地处理错误的标记，并且不需要完整的浏览器引擎。该方法会抛出 `IOException`，让调用者决定如何记录或恢复——这对于线程池场景非常合适，因为你不希望单个错误文件导致整个 executor 终止。

## 优雅地关闭 Executor – 创建 Fixed Thread Pool

在提交完所有任务后，我们必须告诉线程池停止接受新工作并完成已排队的任务。

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

*解释：* `shutdown()` 阻止新的提交，而 `awaitTermination` 会阻塞，直到所有解析任务结束（或超时）。如果出现卡死，`shutdownNow()` 会尝试取消正在运行的任务。此模式是安全 **create fixed thread pool** 的推荐做法。

## 完整、可运行的示例

将所有内容整合在一起，这里提供一个可以编译运行的单文件示例。它包含必要的 import、`main` 方法以及上面描述的辅助方法。

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

**预期输出**（假设每个文件的正文约有 1 200 个字符）：

```
YOUR_DIRECTORY/a.html → 1234 chars
YOUR_DIRECTORY/b.html → 1198 chars
YOUR_DIRECTORY/c.html → 1305 chars
YOUR_DIRECTORY/d.html → 1120 chars
```

如果某个文件缺失或格式错误，你会在 `stderr` 中看到堆栈跟踪，但其他任务仍会继续执行——这正是一个表现良好的 **java thread pool example** 应该具备的行为。

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| *如果我有超过四个文件怎么办？* | 线程池会将多余的任务排队，并在有线程空闲时立即执行。无需额外代码。 |
| *我应该改用 `newCachedThreadPool` 吗？* | `newCachedThreadPool` 会按需创建线程，且可能无限增长，这对 I/O 密集型任务风险较大。**fixed thread pool** 能提供可预测的内存和 CPU 使用。 |
| *如何根据 CPU 核心数更改线程池大小？* | `int cores = Runtime.getRuntime().availableProcessors(); ExecutorService exec = Executors.newFixedThreadPool(cores);` 是常用模式。 |
| *如果某个文件的解析失败怎么办？* | lambda 中的 `catch (IOException e)` 会将失败隔离，记录日志，并让线程池的其余任务继续工作。 |
| *我可以把提取的文本返回给调用者吗？* | 可以——使用 `Future<String>` 替代 `submit(Runnable)`。代码示例为 `Future<String> f = executor.submit(() -> extractBodyText(path));`，随后 `String result = f.get();`。 |

## 结论

我们已经介绍了 **如何使用 executor** 来启动一个 **fixed thread pool java**，并行处理一组 HTML 文件，提取正文文本并报告字符数。完整的 **java thread pool example** 展示了正确的资源管理、错误处理以及可复用的提取方法。

接下来可以做什么？尝试将 `extractBodyText` 实现替换为更复杂的爬虫，实验更大的线程池规模，或将结果写入数据库。你也可以探索 `CompletionService`，以在结果就绪时立即获取，这在文件大小差异较大时非常有用。

随意修改目录路径、添加更多文件，或将此代码片段集成到更大的爬取框架中。核心模式——创建线程池、提交独立任务、优雅关闭——始终不变，无论工作负载多么复杂。

祝编码愉快，愿你的线程永远活跃（当然，直到你关闭它们为止）！

## 相关教程

- [Fixed thread pool java – 使用 ExecutorService 并行 HTML 清理](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [如何在 Java 中查询 HTML – 完整教程](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [如何在 Java 中使用 Aspose.HTML - 精通 HTML5 Canvas 渲染](/html/english/java/html5-canvas-rendering/html5-canvas/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}