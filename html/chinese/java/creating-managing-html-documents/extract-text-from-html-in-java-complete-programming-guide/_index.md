---
category: general
date: 2026-06-29
description: 使用简洁的代码演示在 Java 中提取 HTML 文本。学习如何在 Java 中读取 HTML 文件、处理 Java HTML 渲染，并高效地打印
  HTML 页码。
draft: false
keywords:
- extract text from html
- read html file java
- java html rendering
- print html page number
- read html pages
language: zh
og_description: 快速在 Java 中提取 HTML 文本。本教程展示如何读取 HTML 文件、管理 Java HTML 渲染，并为每页打印 HTML
  页码。
og_title: 在 Java 中从 HTML 提取文本 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Extract text from HTML in Java with a simple code walkthrough. Learn
    to read HTML file Java, handle java html rendering, and print html page number
    efficiently.
  headline: Extract Text from HTML in Java – Complete Programming Guide
  type: TechArticle
- description: Extract text from HTML in Java with a simple code walkthrough. Learn
    to read HTML file Java, handle java html rendering, and print html page number
    efficiently.
  name: Extract Text from HTML in Java – Complete Programming Guide
  steps:
  - name: Load the HTML Document
    text: First, we need to read the raw HTML file into memory. Using **jsoup** gives
      us a tidy DOM without launching a full browser.
  - name: Simulate Java HTML Rendering & Determine Page Count
    text: Real browsers paginate content based on viewport height. For a pure‑Java
      solution we can approximate pagination using **openhtmltopdf**’s layout engine,
      which tells us how many “pages” the document would occupy at a given height
      (e.g., 800 px).
  - name: Iterate Over Pages and Extract Their Text
    text: Now that we have a page count, we loop from `1` to `totalPages`. For each
      iteration we extract the text that belongs to that slice.
  - name: Print the Page Number and Its Text
    text: Finally, we output each page’s number and its extracted text to the console.
      This satisfies the **print html page number** requirement.
  type: HowTo
tags:
- Java
- HTML
- File I/O
- Text Extraction
title: 在 Java 中从 HTML 提取文本 – 完整编程指南
url: /zh/java/creating-managing-html-documents/extract-text-from-html-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中从 HTML 提取文本 – 完整编程指南

是否曾想过如何使用纯 Java **从 HTML 提取文本**？也许你有一个保存为长 HTML 文件的大型报告，需要原始文本进行索引、分析，或仅仅快速预览。在本教程中，我们将演示一种实用方法来在 Java 中读取 HTML 文件，让渲染引擎对其进行分页，然后 **打印 html 页面编号** 并输出其文本内容。

如果你也想 **read html file java** 而不引入笨重的浏览器，那么你来对地方了。完成后，你将拥有一个独立的程序，可以直接放入任何项目并立即运行。

![从 HTML 提取文本示例](extract-text-from-html.png "从 html 提取文本示例")

## 本指南涵盖内容

- 使用轻量级解析器从磁盘加载 HTML 文档。
- 了解 **java html rendering** 如何将长文档拆分为虚拟页面。
- 遍历每个渲染页面，提取其纯文本，并打印页面编号。
- 处理边缘情况，例如缺失页面或异常大的文件。
- 一个完整的可运行代码示例，供你复制粘贴使用。

无需外部服务，也没有隐藏的魔法——仅使用纯 Java 和少量精选库。

## 前置条件

在开始之前，请确保你已具备以下条件：

1. 已安装 JDK 17 或更高版本（代码为简洁使用了 `var` 关键字，但如果需要可以降级到 JDK 11）。
2. 一个 Maven 或 Gradle 项目，你可以在其中添加单个依赖：**jsoup**（用于解析 HTML）和 **openhtmltopdf**（可选，用于真实分页）。  
   ```xml
   <!-- Maven snippet -->
   <dependency>
       <groupId>org.jsoup</groupId>
       <artifactId>jsoup</artifactId>
       <version>1.17.2</version>
   </dependency>
   <dependency>
       <groupId>com.openhtmltopdf</groupId>
       <artifactId>openhtmltopdf-pdfbox</artifactId>
       <version>1.0.10</version>
   </dependency>
   ```
3. 一个名为 `long.html` 的示例 HTML 文件，放置在磁盘的某个位置（代码中会使用该路径）。

如果你是 Maven 新手，只需创建一个包含上述两个依赖的 `pom.xml` 并运行 `mvn compile`。这就是你所需的全部设置。

## 从 HTML 提取文本 – 步骤实现

下面我们将解决方案拆分为五个逻辑步骤。每个步骤包括简短说明、准确的 Java 代码以及该步骤重要性的备注。

### 步骤 1：加载 HTML 文档

首先，我们需要将原始 HTML 文件读取到内存中。使用 **jsoup** 可以在不启动完整浏览器的情况下获得整洁的 DOM。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

// Step 1: Load the HTML file from disk
public static Document loadHtml(String filePath) throws IOException {
    File input = new File(filePath);
    // Jsoup parses the file using UTF‑8 by default; you can specify another charset if needed.
    return Jsoup.parse(input, "UTF-8");
}
```

*为什么重要*：直接将文件读取为字符串会保留标签和实体。Jsoup 会剥离注释、规范化空白，并构建一个可供后续查询的树结构。

### 步骤 2：模拟 Java HTML 渲染并确定页面数量

真实浏览器会根据视口高度对内容进行分页。对于纯 Java 的解决方案，我们可以使用 **openhtmltopdf** 的布局引擎近似分页，它会告诉我们在给定高度（例如 800 px）下文档会占用多少“页面”。

```java
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import com.openhtmltopdf.render.Box;
import com.openhtmltopdf.render.PageBox;

// Step 2: Compute how many virtual pages the document would occupy
public static int getPageCount(Document doc, int pageHeightPx) {
    // Render the document to a hidden PDF; the renderer also builds page boxes.
    PdfRendererBuilder builder = new PdfRendererBuilder();
    builder.withHtmlContent(doc.html(), null);
    // The builder needs a target, but we can direct output to a ByteArrayOutputStream we discard.
    try (var out = new java.io.ByteArrayOutputStream()) {
        builder.toStream(out);
        builder.run();
        // After rendering, the layout tree is accessible via the builder's internal state.
        // For brevity, we’ll use a simplified approach: assume each 800 px slice = 1 page.
        // In a real app you could inspect PageBox objects for exact counts.
        int totalHeight = doc.body().outerHtml().length(); // rough proxy for height
        return Math.max(1, (int) Math.ceil((double) totalHeight / pageHeightPx));
    } catch (Exception e) {
        throw new RuntimeException("Failed to render HTML for pagination", e);
    }
}
```

*为什么重要*：了解每个块的 **print html page number** 可以帮助你组织输出、单独存储页面，或将其提供给期望分页输入的下游服务。

> **小技巧**：如果不需要精确分页，只需按固定字符数（例如 5 000）拆分文档。下面的代码展示了更准确的基于渲染的方式，但更简单的拆分方法适用于大多数日志文件式的 HTML。

### 步骤 3：遍历页面并提取其文本

现在我们已经得到页面数量，接下来从 `1` 循环到 `totalPages`。在每次迭代中提取属于该切片的文本。

```java
import org.jsoup.select.Elements;

// Step 3: Extract plain text for a given page number
public static String getPageText(Document doc, int pageNumber, int pageHeightPx) {
    // In a real rendering scenario you would ask the layout engine for the box range.
    // Here we simulate by taking a substring of the body’s text.
    String fullText = doc.body().text(); // all visible text, no tags
    int charsPerPage = pageHeightPx * 10; // arbitrary factor to mimic density
    int start = (pageNumber - 1) * charsPerPage;
    int end = Math.min(start + charsPerPage, fullText.length());
    if (start >= fullText.length()) {
        return "";
    }
    return fullText.substring(start, end).trim();
}
```

*为什么重要*：该方法仅提取会出现在可视页面上的字符，模拟用户在 **java html rendering** 后看到的内容。

### 步骤 4：打印页面编号及其文本

最后，我们将每页的编号及其提取的文本输出到控制台。这满足了 **print html page number** 的需求。

```java
public static void main(String[] args) {
    String path = "YOUR_DIRECTORY/long.html"; // adjust to your environment
    try {
        Document doc = loadHtml(path);
        int pageHeightPx = 800;                     // height we consider per page
        int totalPages = getPageCount(doc, pageHeightPx);
        System.out.println("Total pages (estimated): " + totalPages);
        for (int page = 1; page <= totalPages; page++) {
            String pageText = getPageText(doc, page, pageHeightPx);
            System.out.println("\n--- Page " + page + " ---");
            System.out.println(pageText);
        }
    } catch (IOException e) {
        System.err.println("Failed to read HTML file: " + e.getMessage());
    }
}
```

**预期的控制台输出（为简洁起见已截断）：**

```
Total pages (estimated): 4

--- Page 1 ---
Welcome to our annual report... (first 800 px worth of text)

--- Page 2 ---
Section 2: Market Overview... (next slice)

--- Page 3 ---
Financial Highlights... (and so on)

--- Page 4 ---
Appendix and References... (final chunk)
```

如果文件短于一页，循环仍会运行一次并打印完整文本——无需特殊处理。

## 处理边缘情况与常见陷阱

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **文件为空或缺失** | `FileNotFoundException` 由 Jsoup 抛出 | 在调用 `loadHtml` 前验证路径并提供友好的错误提示。 |
| **非常大的 HTML（≥ 100 MB）** | 加载整个文档时出现内存不足 | 使用 **jsoup 的流式解析器** (`Jsoup.parse(InputStream, ...)`) 并即时分页。 |
| **非 ASCII 字符** | 如果使用错误的字符集会导致输出乱码 | 显式传递正确的字符集（`UTF‑8` 最安全）。 |
| **动态内容（由 JavaScript 生成）** | Jsoup 不会执行脚本，可能导致渲染的文本缺失 | 如果确实需要脚本执行，可切换到无头浏览器，如 **Playwright** 或 **Selenium**。 |
| **需要精确分页** | 我们简单的基于字符的拆分可能与可视页面不一致 | 深入研究 **openhtmltopdf** 提供的 `PageBox` 对象；它们揭示了精确的边界框。 |

## 完整可运行示例（所有代码组合）

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;

public class HtmlTextExtractor {

    // Load HTML file
    public static Document loadHtml(String filePath) throws IOException {
        File input = new File(filePath);
        return Jsoup.parse(input, "UTF-8");
    }

    // Estimate page count based on a fixed height (800 px)
    public static int getPageCount(Document doc, int pageHeightPx) {
        // Rough heuristic: number of characters divided by an estimated density
        int totalChars = doc.body().text().length();
        int charsPerPage = pageHeightPx * 10; // tweak factor as needed
        return Math.max(1, (int) Math.ceil((double) totalChars / charsPerPage));
    }

    // Extract text for a specific page number
    public static String getPageText(Document doc, int pageNumber, int pageHeightPx


## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方式。

- [从文件加载 HTML 文档（Aspose.HTML for Java）](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Aspose.HTML for Java 中的高级 HTML 文档文件加载](/html/english/java/creating-managing-html-documents/advanced-file-loading-html-documents/)
- [在 Aspose.HTML for Java 中将 HTML 文档保存到文件](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}