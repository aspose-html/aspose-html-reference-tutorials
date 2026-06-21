---
category: general
date: 2026-06-07
description: 使用 Java 的 ExecutorService 将 HTML 转换为 PDF。了解如何批量转换 HTML 文件、将 HTML 文档保存为
  PDF，以及如何优雅地关闭 ExecutorService。
draft: false
keywords:
- convert html to pdf
- save html document as pdf
- shutdown executorservice gracefully
- batch convert html to pdf
language: zh
og_description: 使用 Java 的 ExecutorService 将 HTML 转换为 PDF。掌握批量转换、将 HTML 文档保存为 PDF，以及优雅地关闭
  ExecutorService。
og_title: 使用 Java 将 HTML 转换为 PDF – 并行批处理指南
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
title: 使用 Java 将 HTML 转换为 PDF – 并行批处理指南
url: /zh/java/conversion-html-to-other-formats/convert-html-to-pdf-with-java-parallel-batch-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 将 HTML 转换为 PDF – 并行批处理指南

是否曾经需要 **将 HTML 转换为 PDF**，却因为要处理大量文件而感到束手无策？你并不是唯一遇到这种情况的开发者——在构建报表生成器或发票导出器时，很多人都会碰到这道墙。好消息是，只需几行 Java 代码加上一个聪明的线程池，就能 **批量将 HTML 转换为 PDF**，**将 HTML 文档保存为 PDF**，并且在工作完成后 **优雅地关闭 ExecutorService**。

在本教程中，我们将一步步演示一个完整、可直接运行的示例。你将了解为什么固定大小的线程池是并行转换的最佳选择，转换代码本身的写法，以及如何干净利落地终止执行器。完成后，你将拥有一个可以直接放入任何项目的自包含程序——无需缺失的部件，也没有模糊的 “参考文档” 链接。

---

## 你将构建的内容

- 一个读取本地 HTML 文件列表的 Java 控制台应用。  
- 每个文件都会交给工作线程生成对应的 PDF。  
- 应用使用 **ExecutorService** 并行执行转换。  
- 当所有任务都已加入队列后，线程池会 **优雅地关闭**，确保没有线程悬挂。

**先决条件**  
- Java 17（或任意近期 JDK）。  
- 能够渲染 HTML 的 PDF 库，例如 **OpenHTMLtoPDF**、**iText** 或 **Flying Saucer**。代码中我们使用占位的 `HTMLDocument` 类；请替换为你所使用库的 API。  
- 基本的 Java 并发知识（不需要高级技巧）。

---

![Diagram showing batch conversion of HTML files to PDF using ExecutorService](batch-convert-diagram.png "Convert HTML to PDF in parallel with ExecutorService")

*Alt text: 使用线程池进行批量处理，将 HTML 转换为 PDF 的示意图。*

---

## 并行转换 HTML 为 PDF（批量转换 HTML 为 PDF）

当你手头有几十甚至上千个 HTML 文件时，在主线程上逐个转换会成为瓶颈。固定大小的线程池让 JVM 重复使用一定数量的工作线程，既保持 CPU 高利用率，又不会让系统负荷过重。

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

### 为什么这样可行

- **并行性**：每次 `submit` 调用都会把转换任务交给工作线程，因此在四核机器上可以同时处理四个文件。  
- **隔离性**：`convertAndSave` 方法封装了所有 **将 HTML 文档保存为 PDF** 所需的逻辑，后期替换底层库时只需修改此处。  
- **优雅终止**：先调用 `shutdown()`，告诉线程池 “不再接受新任务，请完成已有任务”。随后 `awaitTermination` 循环为线程提供收尾的机会，只有在它们顽固不化时才会调用 `shutdownNow()`。这种模式是 **优雅地关闭 ExecutorService** 的推荐做法。

---

## 将 HTML 文档保存为 PDF – 核心转换逻辑

任何 **将 HTML 转换为 PDF** 工作流的核心都是转换库。虽然示例使用了一个虚拟的 `HTMLDocument`，下面给出使用 **OpenHTMLtoPDF** 的快速示例：

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

**发生了什么？**  
1. 将 HTML 文件读取为字符串。  
2. `PdfRendererBuilder` 解析标记，应用 CSS，并将结果流式写入 PDF 文件。  
3. 任意 `IOException` 会向上抛到 `convertAndSave`，在那里记录成功或失败。

如果你更倾向于使用 iText 的 `HtmlConverter.convertToPdf` 或 Flying Saucer 的 `ITextRenderer`，只需替换这段代码即可，线程池的其余部分保持不变，这也是我们将 **将 HTML 文档保存为 PDF** 作为独立关注点的原因。

---

## 优雅关闭 ExecutorService – 最佳实践

一个常见的陷阱是提交任务后立即调用 `shutdownNow()`。这会突然中断线程，导致磁盘上出现半写入的 PDF 文件。我们采用的模式——`shutdown()` → `awaitTermination()` → 可选的 `shutdownNow()`——能够确保：

- **不再接受新任务**，在所有任务入队后即生效。  
- **正在运行的任务** 有机会干净利落地完成。  
- **被阻塞的线程** 只有在超过合理超时时（此处为 60 秒）才会被强制中断。

如果你预期 PDF 文件非常大或渲染引擎较慢，可以适当延长超时时间，或使用 `executor.invokeAll(tasks, timeout, unit)` 实现更细粒度的控制。

---

## 完整可运行示例（所有代码整合）

下面是完整的程序代码，你可以直接复制粘贴到 `HtmlToPdfBatch.java` 文件中。只需在 `pom.xml` 或 Gradle 构建文件中加入 OpenHTMLtoPDF（或你偏好的库）依赖，即可运行。



## 接下来你应该学习什么？

以下教程涵盖了与本指南紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方式。每篇资源都提供完整的可运行代码示例以及逐步解释。

- [如何使用 Aspose.HTML for Java 将 HTML 转换为 PDF](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [在 Aspose.HTML 中配置环境 – Java 版](/html/english/java/configuring-environment/)
- [Java 中的 HTML 转 PDF – 带页面尺寸设置的逐步指南](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}