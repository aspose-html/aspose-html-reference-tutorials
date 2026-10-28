---
category: general
date: 2026-10-28
description: 如何在 Java 中读取 HTML 并从 HTML 文件中提取文本。学习使用 Jsoup 将 HTML 转换为文本，涵盖从文件读取 HTML
  和 Java 中的 HTML 转文本技术。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: zh
lastmod: 2026-10-28
og_description: 如何在 Java 中读取 HTML 并从 HTML 文件中提取文本。本教程展示了使用 Jsoup 将 HTML 转换为文本的完整解决方案。
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: 如何在 Java 中读取 HTML 并提取文本 – 快速指南
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: 如何在 Java 中读取 HTML 并提取文本——一步一步的指南
url: /zh/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中读取 HTML 并提取文本 – 步骤指南

如果你需要 **how to read html**（从本地文件读取 HTML），本指南提供完整的解决方案。你将学习如何加载 HTML 文档、提取纯文本，并可选地在细粒度控制下将 HTML 转换为文本。教程结束时，你可以运行示例代码并在控制台看到提取的文本。

读取 HTML 文件是处理网页抓取数据、生成报告或清理用户生成内容时的常见任务。下面的步骤涵盖了你需要的全部内容，从添加所需库到处理诸如标记损坏或字符编码问题等边缘情况。

## 你需要的环境

- Java 17 或更高版本（代码在更早的版本也能编译）
- Maven 或 Gradle 用于依赖管理，或手动添加 Jsoup JAR
- 一个名为 `input.html` 的 HTML 文件，放在项目的 `src/main/resources` 目录下（后续可更改路径）

## 设置 Jsoup 库

Jsoup 是一个轻量级、文档完善的库，可将 HTML 解析为类似 DOM 的结构。它能够优雅地处理破损的 HTML，非常适合 **extract text from html**（从 HTML 中提取文本）的任务。

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

如果你更喜欢手动下载，只需将 JAR 放入类路径，并在源码文件中导入 `org.jsoup.*`。

## 从文件加载 HTML

第一步是将文件读取为 `Document` 对象。Jsoup 提供了接受 `File` 和字符集名称的静态 `parse` 方法。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**为什么重要：** `Jsoup.parse(File, String)` 会读取原始字节，按照提供的字符集解码，并构建干净的 DOM。相比自行将文件读取为字符串，这种方式更安全，因为 Jsoup 会自动规范换行并修复常见的标记错误。

## 从 HTML 中提取纯文本

拥有 `Document` 后，获取可见文本只需一次方法调用。`text()` 方法会连接所有元素的文本内容，同时丢弃标签、脚本和样式。

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

`body()` 调用将提取范围限制在 `<body>` 元素，这通常是你 **read html from file**（从文件读取 HTML）进行内容分析时的目标。得到的字符串会将空白折叠为单个空格，模拟浏览器渲染文本的效果。

### 预期输出

假设 `input.html` 内容如下：

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

运行程序后打印：

```
Extracted text:
Hello World This is a demo page.
```

## 使用额外选项将 HTML 转换为文本

有时你需要比 `text()` 提供的更细粒度的控制——例如保留换行、保持列表编号，或忽略特定标签。Jsoup 的 `NodeTraversor` 配合自定义 `NodeVisitor` 能实现这些需求。

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

将简单的 `doc.body().text()` 调用替换为：

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**为什么可行：** 访问者以深度优先方式遍历 DOM，在每个块级元素（如 `<p>`、`<div>`、`<h1>`）前追加换行。这保持了段落分隔，对于 **convert html to text**（将 HTML 转换为文本）以提升可读性或供后续 NLP 流程使用非常有帮助。

## 常见陷阱与最佳实践

| 问题 | 产生原因 | 推荐解决方案 |
|------|----------|--------------|
| 错误的字符集 | 文件以 ISO‑8859‑1 保存，但按 UTF‑8 解析会导致字符乱码。 | 从文件的 meta 标签（`<meta charset="...">`）检测字符集，或将正确的字符集名称传给 `Jsoup.parse`。 |
| 大文件 | 将非常大的 HTML 文件一次性加载到内存会导致 `OutOfMemoryError`。 | 使用 `Jsoup.parse(File, String, String baseUri)` 流式解析并增量处理节点，或增大 JVM 堆大小。 |
| 不想要的 script/style 文本 | `text()` 会移除 script 和 style 内容，但自定义访问者可能不小心包含它们。 | 在访问者的 `head` 方法中跳过标签名为 `script` 或 `style` 的节点。 |
| 保留空白 | 空格折叠可能会丢失用于 markdown 转换的格式。 | 使用 `Element.wholeText()` 获取原始文本节点，然后手动后处理空白。 |

解决这些问题可确保你的 **html to text java** 方案在各种输入下都能可靠运行。

## 完整可运行示例

下面是一个独立程序，演示完整工作流——从依赖配置到输出验证。将代码复制到名为 `HtmlToTextDemo.java` 的文件中，旁边放置一个 `input.html` 文件，然后按示例方式执行 `javac && java`。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### 运行程序

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

控制台会同时显示简单提取的结果和详细的

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在已有技巧的基础上进一步深入。每个资源都提供完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方式。

- [How to Use XPath in Java – Read HTML and Extract Text](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Extract text from HTML with Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}