---
category: general
date: 2026-06-19
description: 如何在 Java 中使用可复用的 Runnable 启动线程，启动多个线程，打印线程名称，并使用 Java 解析 HTML。一步一步的示例。
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: zh
og_description: 如何在 Java 中使用 Runnable 启动线程，运行多个线程，打印线程名称，并在一个可运行的示例中使用 Java 解析 HTML。
og_title: Java 中如何启动线程 – 完整指南
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
title: Java 中如何启动线程——完整指南
url: /zh/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中启动线程 – 完整指南

有没有想过 **如何在 Java 中启动线程** 而不被大量样板代码淹没？你并不是唯一的。无论是构建网页爬虫、UI 更新器，还是仅仅需要把繁重的计算卸载出去，掌握线程创建都是每个 Java 开发者必备的技能。

在本教程中，我们将通过一个实用场景来演示：**使用 Java 解析 HTML**，打印当前线程的名称，并 **启动多个共享相同逻辑的线程**。完成后，你将了解 **如何使用 Runnable**，启动多个工作者，并看到预期的输出——所有代码都是可直接复制粘贴的完整示例。

## 你将学到

- 使用 `Thread` 类和 `Runnable` **如何启动线程** 的完整步骤。
- **如何启动多个线程** 来执行相同任务，而无需复制代码。
- **打印线程名称** 的最简方法，配合你的处理结果一起输出。
- 使用轻量级 `HTMLDocument` 辅助类（或你喜欢的任何解析器）**在 Java 中解析 HTML** 的清晰方法。
- 为什么 **如何使用 runnable** 对于可复用、可测试的代码至关重要。

核心示例不需要外部库，但我们会标注如果需要更强大功能时如何替换为 Jsoup 或其他解析器。

---

## 第一步：定义可复用任务 – **如何使用 runnable**

首先，你需要了解 **如何使用 runnable**，即将每个线程要执行的工作封装起来。`Runnable` 只是一个只有 `run()` 方法的函数式接口，非常适合 lambda 表达式。

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

**为什么重要：** 将逻辑放在 `Runnable` 中后，你可以把它交给任意数量的 `Thread` 对象、线程池，甚至以后交给 executor service。这让代码保持 DRY 且易于测试。

---

## 第二步：**如何启动线程** – 创建第一个工作者

有了 `Runnable`，启动线程只需调用 `Thread` 构造函数。一行代码即可回答 **如何启动线程** 的问题：

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

注意第二个参数 `"Worker-1"`。该名称将在我们后面 **打印线程名称** 时出现，使调试不再神秘。

---

## 第三步：**启动多个线程** – 重用同一个 Runnable

想一次处理多个 HTML 文件吗？只需使用相同的 `Runnable` 再创建一个 `Thread`。这演示了 **启动多个线程** 而无需复制任务代码：

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

`Worker-1` 和 `Worker-2` 将并发执行 `extractTextLength` 中定义的代码块。由于任务是无状态的（仅读取文件），不存在竞争条件。

---

## 第四步：**打印线程名称** 同时解析 HTML

在 `Runnable` 中我们已经调用了 `Thread.currentThread().getName()`。这是 **打印线程名称** 的标准做法。输出大致如下（假设 HTML body 包含 1 234 个字符）：

```
Worker-1: 1234
Worker-2: 1234
```

如果在更大的文件上运行程序，每行仍会显示相同的长度，因为两个线程读取的是同一个文件。更改路径或将文件名作为参数传入即可看到不同结果。

---

## 第五步：完整可运行示例 – 从导入到执行

下面是完整的 **自包含** 程序，你可以直接保存为 `HtmlThreadDemo.java`。它包含一个极简的 `HTMLDocument` 存根，即使没有真实解析器也能编译。生产环境请用 Jsoup 或其他库替换该存根。

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

### 预期输出

假设 `page.html` 的 `<body>` 标签内有 2 567 个字符，输出类似：

```
Worker-1: 2567
Worker-2: 2567
```

如果文件读取失败，`catch` 块会打印堆栈跟踪。

---

## 常见坑点 & 专业建议

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **文件未找到** | 路径 `"YOUR_DIRECTORY/page.html"` 是相对于 JVM 启动目录的相对路径。 | 使用绝对路径或 `Paths.get("").toAbsolutePath()` 来调试。 |
| **竞争条件** | 如果 `Runnable` 修改共享状态，线程会冲突。 | 保持任务无状态，或对共享对象进行同步。 |
| **线程过多** | 创建大量 `Thread` 会耗尽操作系统资源。 | 掌握基础后，改用带有界限的 `ExecutorService` 线程池。 |
| **HTML 解析不正确** | 存根 `HTMLDocument` 过于简陋，复杂页面会出错。 | 替换为 Jsoup：`Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## 扩展示例

既然你已经掌握 **如何启动线程**，可以进一步：

- 通过构造函数或捕获变量的 lambda 将文件名传入 `Runnable`，**解析不同文件**。
- 使用 `ConcurrentLinkedQueue<Integer>` **收集结果**，而不是仅打印。
- 使用线程池（`Executors.newFixedThreadPool(4)`）提升可扩展性。
- 将解析器换成 Jsoup、HtmlUnit 或其他适合项目需求的库。

所有这些步骤仍然基于我们讨论的核心思想：定义可复用任务，交给一个或多个线程，并通过 **打印线程名称** 观察是哪条线程在工作。

---

## 结论

我们已经覆盖了 **如何在 Java 中启动线程**，演示了 **如何使用 runnable** 进行可复用工作，展示了 **如何启动多个线程**，并用一个简单示例说明了 **在 Java 中解析 HTML** 的同时 **打印线程名称**。上面的完整代码片段已可直接运行，概念也能扩展到更复杂的生产级应用。

尽情实验吧：更改文件路径、增加工作者数量，或接入真实的 HTML 解析器。基础不变，而你已经拥有了任何多线程 Java 项目的坚实基石。

对线程安全、executor 服务或 HTML 解析库有疑问吗？在下方留言，祝编码愉快！

## 接下来该学习什么？

以下教程与本指南紧密相关，帮助你在已有技术上进一步深入。每篇资源都提供完整可运行的代码示例以及逐步解释，帮助你掌握更多 API 功能并探索替代实现方式。

- [固定线程池 Java – 使用 ExecutorService 并行 HTML 清理](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [如何使用 Aspose.HTML for Java 编辑 HTML](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [如何使用 Aspose.HTML for Java 将 HTML 转换为 PDF](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}