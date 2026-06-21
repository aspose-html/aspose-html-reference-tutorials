---
category: general
date: 2026-04-05
description: Java 多线程教程，展示如何使用固定线程池并行运行任务以及安全地关闭 ExecutorService。
draft: false
keywords:
- java multithreading tutorial
- fixed thread pool java
- shutdown executorservice
- print thread name
- run tasks parallel
language: zh
og_description: Java 多线程教程，手把手教你并行运行任务、创建固定线程池、打印线程名称，以及干净地关闭 ExecutorService。
og_title: Java 多线程教程 – 固定线程池的并行执行
tags:
- Java
- Concurrency
- ExecutorService
title: Java 多线程教程：使用固定线程池并行运行任务
url: /zh/java/advanced-usage/java-multithreading-tutorial-run-tasks-parallel-with-fixed-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# java multithreading tutorial – 并行执行简易指南

是否曾想过在 Java 中 **并行运行任务**，却不想陷入底层线程管理的泥潭？在本 **java multithreading tutorial** 中，我们将手把手教你如何使用 **fixed thread pool java**，打印每个线程的名称，并在工作完成后干净利落地 **shutdown executorservice**。

如果你曾写过一个在网络 I/O 上阻塞的循环，或需要一次性抓取多个网页，那么下面的模式将为你省下大量时间和头疼的调试。

我们将覆盖所有你需要的内容——无需外部文档，只要纯粹的 Java 代码，复制‑粘贴即可运行并看到结果。阅读完本教程后，你将明白为什么固定线程池往往是有界并行的最佳选择，如何安全地终止它，以及如何通过打印线程名称让日志更易读。

> **先决条件**：Java 8+（`java.util.concurrent` 包多年来一直很稳定），一个 IDE 或简单的 `javac`/`java` 命令行，以及对面向对象编程的基本了解。除你已有的 Aspose HTML for Java jar 外，无需额外库。

---

![java 多线程教程示意图，展示线程池分配任务](https://example.com/images/java-multithreading-tutorial.png "java 多线程教程示意图")

## java multithreading tutorial – 设置固定线程池

**固定线程池** 限制了并发运行的线程数量，防止你的应用生成过多 OS 线程而耗尽资源。这里我们创建一个拥有四个工作线程的池：

```java
import java.util.concurrent.*;

public class ParallelProcessingTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a fixed-size thread pool for parallel execution
        ExecutorService executor = Executors.newFixedThreadPool(4);
```

*为什么是四个？* 这与我们要抓取的 URL 数量相匹配，但你可以根据 CPU 核心数、I/O 强度或内存限制来调节。`Executors` 工厂帮你摆脱低层的 `Thread` 构造器，并提供一个干净的 `ExecutorService` 引用，稍后你将 **shutdown executorservice**。

## 准备 URL 并定义并行任务

接下来列出我们要处理的页面。在真实的爬虫中，你可能会从文件或数据库读取这些 URL，但这里使用静态数组可以让示例保持自包含：

```java
        // Step 2: List the web pages to process
        String[] pageUrls = {
            "https://example.com/a.html",
            "https://example.com/b.html",
            "https://example.com/c.html",
            "https://example.com/d.html"
        };
```

现在进入 **run tasks parallel** 环节。对每个 URL 我们提交一个 lambda，加载文档并打印其标题。注意使用 `Thread.currentThread().getName()` —— 这就是我们的 **print thread name** 小技巧，让调试更加轻松：

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

> **专业提示**：将 `HTMLDocument` 包裹在 try‑with‑resources 语句中，可确保底层流在页面加载失败时也能被关闭。

## 优雅地关闭 ExecutorService

在工作完成后仍让线程池存活会导致 JVM 卡住。正确的做法是 **shutdown executorservice**，随后等待终止：

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

*为什么要设超时？* 这可以防止出现永不返回的顽固任务（例如卡住的网络调用）。如果线程池在一分钟内未结束，我们会调用 `shutdownNow()` 来中断所有残留线程。

### 预期输出

运行程序后会打印类似以下内容：

```
pool-1-thread-1 – Example A
pool-1-thread-3 – Example C
pool-1-thread-2 – Example B
pool-1-thread-4 – Example D
```

具体顺序可能会变化——毕竟任务是真正并行执行的。保持不变的是 **print thread name** 前缀，它明确告诉你是哪一个工作线程处理了对应的 URL。

---

## 常见变体与边缘情况

| 情形 | 需要更改的内容 | 原因 |
|-----------|----------------|--------|
| **URL 数量多于线程数** | 保持相同的池大小；多余的任务会自动排队。 | 固定线程池会为你处理背压。 |
| **CPU 密集型工作** | 将池大小设为 `Runtime.getRuntime().availableProcessors()`，而不是硬编码的 4。 | 在不超额订阅的前提下最大化 CPU 利用率。 |
| **需要取消特定任务** | 保留 `executor.submit()` 返回的 `Future<?>`，并调用 `future.cancel(true)`。 | 对单个任务实现细粒度控制。 |
| **处理大文件** | 适度增大池大小 *或* 在预期出现突发时切换到 `newCachedThreadPool()`。 | 缓存池按需创建线程，但要注意防止无限增长。 |

---

## 结论

现在你已经掌握了一套完整的 **java multithreading tutorial**，演示了如何使用 **fixed thread pool java** 实现 **run tasks parallel**，通过 **print thread name** 获得清晰日志，并且能够 **shutdown executorservice** 干净收尾。完整、可运行的代码仅在一个类中，你可以把它直接放入任何项目，立刻开始扩展你的 I/O‑密集型工作。

接下来可以尝试将 `HTMLDocument` 换成自己的 HTTP 客户端，实验不同的池大小，或使用 `CompletionService` 在任务完成时收集结果。若需要更高级的背压处理，还可以探索 `java.util.concurrent.Flow` 进行响应式流编程。

祝编码愉快，记住：选对线程池策略， 并发就会变成 **轻而易举**，而不是 bug 的温床。如有疑问，欢迎留言——我随时乐于聊聊 Java 并发！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}