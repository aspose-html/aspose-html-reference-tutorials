---
category: general
date: 2026-03-05
description: 如何使用 Java 解析 HTML 并提取文本。学习读取 HTML 文件、将 HTML 转换为文本，以及使用 Aspose.HTML 抽取文章内容。
draft: false
keywords:
- how to parse html
- extract text from html
- how to extract article
- read html file java
- convert html to text
language: zh
og_description: 如何在 Java 中解析 HTML 并提取文章文本。一步一步的教程，涵盖读取 HTML 文件、将 HTML 转换为文本以及提取文章。
og_title: 如何在 Java 中解析 HTML – 完整指南
tags:
- Java
- HTML parsing
- Aspose.HTML
title: 如何在 Java 中解析 HTML – 从 HTML 文章中提取文本
url: /zh/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中解析 HTML – 从 HTML 文章中提取文本

是否曾经想过 **如何解析 HTML**，当你需要原始文章文本用于数据管道或快速内容审计时？你并不是唯一的——开发者经常在读取 HTML 文件、提取主要文章并将其转换为纯文本时卡住。

好消息是？只需几行 Java 代码和 Aspose.HTML 库，你就可以完成所有这些操作，甚至更多。在本指南中，我们将准确展示 **如何解析 HTML**、**从 HTML 中提取文本**，以及 **将 HTML 转换为文本** 以供后续处理。完成后，你将拥有一个可复用的代码片段，读取 HTML 文件，找到 `<article>` 标签，并打印干净、可读的文本——无需额外依赖。

## 你将学到的内容

- 如何使用 `HTMLDocument` **读取 HTML 文件 Java**  
- 使用 CSS 选择器 **提取文章** 内容的最佳方式  
- 快速 **将 HTML 转换为文本**（纯文本提取）技术  
- 常见陷阱（缺失元素、编码问题）以及如何规避  
- 预期的控制台输出，帮助你验证一切正常

### 前置条件

- Java 17 或更高（代码在 Java 8+ 上也能运行，但新版本提供更好的模块支持）  
- Maven 或 Gradle 用于获取 Aspose.HTML for Java 库  
- 一个简单的 HTML 文件（例如 `blog.html`），其中包含 `<article>` 元素

> **专业提示：** 如果你还没有 Aspose.HTML，请添加以下 Maven 坐标：  
> ```xml
> <dependency>
>     <groupId>com.aspose</groupId>
>     <artifactId>aspose-html</artifactId>
>     <version>23.10</version>
> </dependency>
> ```

---

## 第一步 – 加载 HTML 文档（如何解析 HTML）

首先，我们需要 **读取 HTML 文件 Java**，让它能够被解析。`HTMLDocument` 完成繁重的工作：它解析标记，构建 DOM，并让我们后续查询。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;

/**
 * Loads an HTML file from disk and creates a DOM representation.
 */
public class TextExtractionTutorial {
    public static void main(String[] args) throws Exception {

        // Replace with the absolute or relative path to your HTML file.
        String htmlPath = "YOUR_DIRECTORY/blog.html";

        // Step 1: Load the HTML document – this is where we actually parse the HTML.
        HTMLDocument document = new HTMLDocument(htmlPath);
```

**为什么这很重要：** 加载文件会触发解析器，它会规范化空白、解析实体并构建可查询的树。跳过此步骤意味着你必须手动扫描字符串——这是一种脆弱的方法，容易在标记损坏时崩溃。

---

## 第二步 – 查找第一个 `<article>` 元素（如何提取文章）

DOM 准备好后，我们可以使用 CSS 选择器 **提取文章**。`querySelector` 简洁且与浏览器定位元素的方式相同。

```java
        // Step 2: Locate the first <article> element using a CSS selector.
        // This is the most reliable way to pull the main content without regex.
        Element articleElement = document.querySelector("article");

        // Defensive check – what if the page has no <article> tag?
        if (articleElement == null) {
            System.err.println("No <article> element found. Check the HTML structure.");
            return;
        }
```

**为什么使用 `querySelector`？** 它遵循 DOM 层级结构，即使 `<article>` 深度嵌套在其他容器中也能工作。正则表达式会错过这些细微差别，且常返回破碎的片段。

---

## 第三步 – 获取纯文本（将 HTML 转换为文本）

现在我们已经拥有 `<article>` 节点，需要 **将 HTML 转换为文本**。`getTextContent()` 方法会剥除所有标签，返回干净、可读的文本。

```java
        // Step 3: Pull the plain‑text content out of the <article>.
        String articleText = articleElement.getTextContent();

        // Optional: Trim leading/trailing whitespace for a tidy output.
        articleText = articleText.trim();
```

**内部是如何工作的？** `getTextContent()` 遍历子节点，连接文本节点并忽略标记。这相当于你在浏览器中复制文章并粘贴到文本编辑器时看到的内容。

---

## 第四步 – 打印提取的文本（验证结果）

最后，让我们 **从 HTML 中提取文本** 并在控制台显示。这一步确认一切如预期工作。

```java
        // Step 4: Output the extracted article text.
        System.out.println("=== Extracted Article Text ===");
        System.out.println(articleText);
    }
}
```

### 预期输出

假设 `blog.html` 包含：

```html
<article>
  <h1>Welcome to My Blog</h1>
  <p>This is the first paragraph of the article.</p>
  <p>Here's another line with <a href="#">a link</a>.</p>
</article>
```

运行程序后打印：

```
=== Extracted Article Text ===
Welcome to My Blog
This is the first paragraph of the article.
Here's another line with a link.
```

注意所有 HTML 标签都消失了，只剩下可读的句子——这正是 **将 HTML 转换为文本** 的核心。

---

## 边缘情况与技巧（如何安全解析 HTML）

| 情况 | 需要注意的点 | 推荐解决方案 |
|-----------|-------------------|-----------------|
| **缺少 `<article>`** | `articleElement` 为 `null`。 | 添加回退：搜索 `<div class="content">` 或使用 `document.body.getTextContent()`。 |
| **编码字符** (`&amp;`, `&#8217;`) | 文本中出现 HTML 实体。 | `getTextContent()` 已经解码大多数实体；对于少数情况，可使用 `StringEscapeUtils.unescapeHtml4`。 |
| **大文件（>10 MB）** | 解析可能消耗大量内存。 | 使用接受 `InputStream` 的 `HTMLDocument` 重载，并在需要时设置 `maxMemory`。 |
| **多个 `<article>` 标签** | 只会获取第一个。 | 使用 `document.querySelectorAll("article")` 并遍历 `NodeList`，如果需要所有文章。 |

---

## 完整可运行示例（所有步骤合并）

下面是完整程序，可直接复制粘贴到 IDE 中。它包含注释、错误处理以及我们讨论的完整流程。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;

/**
 * Complete example: how to parse HTML, extract text from HTML, and read an HTML file in Java.
 *
 * Prerequisite: Add Aspose.HTML for Java to your project dependencies.
 */
public class TextExtractionTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the HTML document (how to parse HTML)
        String htmlPath = "YOUR_DIRECTORY/blog.html";
        HTMLDocument document = new HTMLDocument(htmlPath);

        // 2️⃣ Find the first <article> element (how to extract article)
        Element articleElement = document.querySelector("article");
        if (articleElement == null) {
            System.err.println("No <article> element found – cannot extract article.");
            return;
        }

        // 3️⃣ Retrieve plain text (convert HTML to text)
        String articleText = articleElement.getTextContent().trim();

        // 4️⃣ Print the extracted text (verify the result)
        System.out.println("=== Extracted Article Text ===");
        System.out.println(articleText);
    }
}
```

将其保存为 `TextExtractionTutorial.java`，将 `YOUR_DIRECTORY/blog.html` 替换为实际路径，编译并运行：

```bash
javac -cp "path/to/aspose-html.jar" TextExtractionTutorial.java
java -cp ".:path/to/aspose-html.jar" TextExtractionTutorial
```

你应该会在控制台看到文章的纯文本版本。

---

## 常见问题

**问：这能处理格式错误的 HTML 吗？**  
答：Aspose.HTML 包含容错解析器，大多数破损的标记（缺少闭合标签、孤立引号）都会自动纠正。不过，干净的 HTML 能获得最可靠的结果。

**问：我可以从同一页面提取多个文章吗？**  
答：完全可以——将 `querySelector` 替换为 `querySelectorAll("article")` 并遍历 `NodeList`。

**问：如果我需要文章的 HTML 源码而不是纯文本怎么办？**  
答：使用 `articleElement.getOuterHTML()`；它返回保留标签的 HTML 片段。

**问：有没有办法保留换行符？**  
答：`getTextContent()` 已经会为块级元素（`<p>`、`<h1>`）插入换行符。如果需要自定义格式，可使用 `replaceAll("\\s+", " ")` 对字符串进行后处理。

---

## 结论

我们已经完整演示了 **如何在 Java 中解析 HTML**、**从 HTML 中提取文本**，以及使用 Aspose.HTML **提取文章** 内容的具体步骤。完整的自包含代码展示了读取 HTML 文件、定位 `<article>` 标签、将该片段转换为纯文本并打印结果的全过程。

掌握此模式后，你可以将文章正文输送到搜索索引、进行情感分析或生成摘要——任何需要 **将 HTML 转换为文本** 的场景都不在话下。

### 后续步骤

- 尝试更改 CSS 选择器以定位其他区域（例如 `".post-body"`）。  
- 将其与批处理器结合，自动处理数十个文件。  
- 如需将修改后的 HTML 写回磁盘，可探索 Aspose.HTML 的 `HTMLDocument.save()`。

对 **read html file java** 有更多疑问或需要帮助扩展方案？在下方留言，祝你解析愉快！

![Screenshot of console output showing extracted article text – how to parse html](/images/parse-html-console.png "How to parse html – console output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}