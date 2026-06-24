---
category: general
date: 2026-06-19
description: 学习如何使用简单的 Java 示例从 HTML 生成 PDF。本 HTML 转 PDF 教程展示了如何使用 OpenHTMLtoPDF 将
  HTML 文件转换为 PDF。
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: zh
og_description: HTML转PDF教程向您展示如何使用Java从HTML生成PDF。按照步骤快速将HTML文件转换为PDF。
og_title: HTML 转 PDF 教程：Java 转换指南
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: HTML转PDF教程：在Java中将HTML转换为PDF
url: /zh/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf 教程 – 使用 Java 将 HTML 页面转换为 PDF

Ever wondered how to turn a static HTML page into a sleek PDF document without leaving your IDE? You're not alone. In this **html to pdf tutorial** we’ll walk through a complete, ready‑to‑run Java example that **generate pdf from html** in just a few minutes.

We’ll cover everything you need—project setup, adding the right library, writing the conversion code, and even a quick tip for converting a live webpage to PDF. By the end you’ll be able to **convert html file pdf** on your own machine, and you’ll understand how to **create pdf from html** for any future project.

## 你需要的环境

- Java 17 或更高版本（代码适用于任何近期的 JDK）
- Maven 或 Gradle（我们将展示 Maven 代码片段）
- 一个你想转换为 PDF 的小型 HTML 文件（我们会即时创建一个）
- IDE 或简单的文本编辑器——自行选择

那就这么简单。无需重量级服务器，无需付费 SDK，仅使用纯 Java 和一个免费开源的库。

## 步骤 1：html to pdf 教程 – 设置 Maven 项目

First things first. Create a new Maven project (or add to an existing one). The only dependency you really need is **OpenHTMLtoPDF**, which does the heavy lifting of rendering HTML and CSS into a PDF.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** 如果你使用 Gradle，可以在 `build.gradle` 中的 `implementation` 下添加相同的依赖。  

Why this step matters: without the library the JVM has no idea how to translate HTML tags into PDF drawing commands. OpenHTMLtoPDF is lightweight, actively maintained, and works with CSS‑2.1, so your styling stays intact.

## 步骤 2：generate pdf from html – 准备示例 HTML 文件

Let’s create a tiny `input.html` right next to our Java source. This keeps the example self‑contained and demonstrates the **create pdf from html** workflow.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

You can replace the content with anything—tables, images, even JavaScript (though the renderer ignores scripts). The important part is that the file lives on the classpath so the converter can locate it.

## 步骤 3：convert html file pdf – 编写转换工具类

Now the heart of the **html to pdf tutorial**: a tiny `HtmlToPdfConverter` class that reads the HTML and writes a PDF. The code below is a full, runnable example; copy‑paste it into `src/main/java/com/example/HtmlToPdfConverter.java`.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### 为什么这段代码有效

1. **Resource flexibility** – 方法首先检查提供的路径是否指向真实文件；如果不是，则回退到 classpath 资源。这意味着你可以通过传入 URL 字符串来 **convert webpage to pdf**（只需将 `withHtmlContent` 调用替换为 `withUri`）。

2. **Automatic directory creation** – `Files.createDirectories` 确保 `target/` 文件夹存在，避免出现 “No such file or directory” 错误。

3. **Single‑line conversion** – `PdfRendererBuilder` 在内部处理 CSS、字体和页面布局。无需手动管理 PDF 页面；库会为你完成，使示例简短且专注于 **convert html file pdf** 概念。

## 步骤 4：create pdf from html – 运行程序并验证

Open a terminal in the project root and execute:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

If everything is set up correctly you’ll see:

```
✅ PDF successfully created at target/output.pdf
```

Open `target/output.pdf` with any PDF viewer. You should see the styled “Monthly Sales Report” header, the paragraph text, and the same margins you defined in the HTML `<style>` block.

> **What if you don’t see the styling?**  
> 确保 CSS 为内联或与 HTML 位于同一文件夹。OpenHTMLtoPDF 根据你传递给 `withHtmlContent` 的基准 URI 解析相对 URL。上面的代码片段中我们传入了 `null`，这对简单的内联 CSS 有效。对于外部样式表，请将目录路径作为第二个参数提供。

## 步骤 5：convert webpage to pdf – 处理远程 URL（可选）

Sometimes you need to **convert webpage to pdf** directly from the internet—think of archiving an online receipt. The library supports this via `withUri`. Here’s a quick adaptation:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Call it like:



## 接下来你应该学习什么？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [如何使用 Aspose.HTML for Java 将 HTML 转换为 PDF（Java）](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [在 Aspose.HTML 中配置环境以将 HTML 转换为 PDF（Java）](/html/english/java/configuring-environment/)
- [Java 中将 HTML 转换为 PDF – 带页面尺寸设置的逐步指南](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}