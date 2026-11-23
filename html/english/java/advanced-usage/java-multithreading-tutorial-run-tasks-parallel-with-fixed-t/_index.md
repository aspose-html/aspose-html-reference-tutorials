---
category: general
date: 2026-04-05
description: java multithreading tutorial showing how to run tasks parallel using
  a fixed thread pool java and shutdown executorservice safely.
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: en
og_description: java multithreading tutorial that walks you through running tasks
  parallel, creating a fixed thread pool java, printing thread name, and cleanly shutting
  down executorservice.
og_title: java multithreading tutorial – Parallel Execution with Fixed Thread Pool
tags:
- Java
- Concurrency
- ExecutorService
title: 'java multithreading tutorial: Run Tasks Parallel with Fixed Thread Pool'
url: /java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – Parallel Execution Made Simple

Ever wondered how to **run tasks parallel** in Java without drowning in low‑level thread management? In this **java multithreading tutorial** we’ll walk you through exactly that: using a **fixed thread pool java**, printing each thread’s name, and cleanly **shutdown executorservice** when work is done.  

If you’ve ever written a loop that blocks on network I/O or you need to scrape several web pages at once, the pattern we cover below will save you both time and headaches.  

We’ll cover everything you need—no external docs, just pure Java code you can copy‑paste, run, and see results. By the end you’ll understand why a fixed thread pool is often the sweet spot for bounded parallelism, how to safely terminate it, and how to make your logs more readable by printing the thread name.  

> **Prerequisites**: Java 8+ (the `java.util.concurrent` package has been stable for years), an IDE or simple `javac`/`java` command line, and a basic grasp of OOP. No additional libraries are required beyond the Aspose HTML for Java jar you already have.

---

![java multithreading tutorial diagram showing a thread pool feeding tasks](https://example.com/images/java-multithreading-tutorial.png "java multithreading tutorial diagram")

## java multithreading tutorial – Set Up a Fixed Thread Pool

A **fixed thread pool** caps the number of concurrently running threads, preventing your application from spawning too many OS threads and exhausting resources. Here we create a pool with four workers:

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*Why four?* It matches the number of URLs we’ll fetch, but you can tune this number based on CPU cores, I/O intensity, or memory limits. The `Executors` factory shields you from the low‑level `Thread` constructor and gives you a clean `ExecutorService` reference that you’ll later **shutdown executorservice**.

## Prepare URLs and Define Parallel Tasks

Next, we list the pages we want to process. In a real scraper you’d probably read these from a file or database, but a static array keeps the example self‑contained:

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

Now comes the **run tasks parallel** part. For each URL we submit a lambda that loads the document and prints its title. Notice the use of `Thread.currentThread().getName()` – that’s our **print thread name** trick which makes debugging far easier:

```java
        // Step 3: Submit a task for each URL that loads the document and prints its title
        for (String url : pageUrls) {
            executor.submit(() -> {
                try (HTMLDocument doc = new HTMLDocument(url)) {
                    String title = doc.getTitle();
                    // Print the thread name alongside the title
                    System.out.println(Thread.currentThread().getName() + " – " + title);
                } catch (Exception e) {
                    System.err.println(Thread.currentThread().getName() + " failed: " + e.getMessage());
                }
            });
        }
```

> **Pro tip**: Wrapping the `HTMLDocument` in a try‑with‑resources block guarantees the underlying stream is closed, even if the page fails to load.

## Gracefully Shutdown the ExecutorService

Leaving a thread pool alive after its work is finished can keep your JVM hanging. The proper way is to **shutdown executorservice**, then await termination:

```java
        // Step 4: Shut down the pool and wait for all tasks to finish
        executor.shutdown();                         // No new tasks will be accepted
        if (!executor.awaitTermination(1, TimeUnit.MINUTES)) {
            // Force shutdown if tasks exceed the timeout
            executor.shutdownNow();
        }
    }
}
```

*Why the timeout?* It protects you from a rogue task that never returns (e.g., a network call that hangs). If the pool doesn’t finish in one minute we invoke `shutdownNow()` to interrupt any lingering threads.

### Expected Output

Running the program prints something similar to:

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

The exact order may vary—after all, the tasks are truly parallel. What stays constant is the **print thread name** prefix, which tells you exactly which worker handled each URL.

---

## Common Variations & Edge Cases

| Situation | What to Change | Reason |
|-----------|----------------|--------|
| **More URLs than threads** | Keep the same pool size; extra tasks will queue automatically. | The fixed pool handles back‑pressure for you. |
| **CPU‑bound work** | Set the pool size to `Runtime.getRuntime().availableProcessors()` instead of a hard‑coded 4. | Maximizes CPU utilization without oversubscribing. |
| **Need to cancel a specific task** | Keep a `Future<?>` reference from `executor.submit()` and call `future.cancel(true)`. | Gives fine‑grained control over individual jobs. |
| **Processing large files** | Increase the pool size modestly *or* switch to `newCachedThreadPool()` if you expect bursts. | Cached pools create threads on demand, but beware of unbounded growth. |

---

## Conclusion

You now have a solid **java multithreading tutorial** that demonstrates how to **run tasks parallel** using a **fixed thread pool java**, **print thread name** for clear logging, and **shutdown executorservice** cleanly. The complete, runnable code lives in a single class, so you can drop it into any project and start scaling your I/O‑bound work instantly.

What’s next? Try swapping `HTMLDocument` for your own HTTP client, experiment with different pool sizes, or integrate a `CompletionService` to collect results as they finish. You might also explore `java.util.concurrent.Flow` for reactive streams if you need back‑pressure handling beyond a simple queue.

Happy coding, and remember: with the right thread‑pool strategy, concurrency becomes a *piece of cake*, not a source of bugs. If you have questions, feel free to drop a comment—I'm always up for a chat about Java concurrency!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}