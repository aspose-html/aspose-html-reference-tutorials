---
category: general
date: 2026-06-03
description: 在 Java 中按类选择 HTML 元素，学习如何在 Java 中加载 HTML 文件，解析 HTML 文档，并提取 CSS 属性值，例如元素颜色。
draft: false
keywords:
- select html element by class
- load html file java
- how to get element color
- parse html document java
- extract css property value
language: zh
og_description: 在 Java 中按类选择 HTML 元素，加载 HTML 文件，并通过逐步代码提取 CSS 属性值（如元素颜色）。
og_title: 在 Java 中按类选择 HTML 元素 – 完整编程教程
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Select HTML element by class in Java, learn how to load HTML file Java,
    parse HTML document Java, and extract CSS property value like element color.
  headline: Select HTML Element by Class in Java – Complete Guide
  type: TechArticle
- description: Select HTML element by class in Java, learn how to load HTML file Java,
    parse HTML document Java, and extract CSS property value like element color.
  name: Select HTML Element by Class in Java – Complete Guide
  steps:
  - name: Add jsoup Dependency
    text: 'If you’re using Maven, pop this into your `pom.xml`:'
  - name: Load the Document
    text: '```java import org.jsoup.Jsoup; import org.jsoup.nodes.Document; import
      java.io.File; import java.io.IOException;'
  - name: 3A. Inline Styles (Fast Path)
    text: 'If the element defines `color` directly:'
  - name: 3B. External Stylesheets (Full‑Featured)
    text: 'If the color comes from an external CSS file, you’ll need to load that
      stylesheet and apply the cascade rules yourself. Below is a **simplified** approach
      that works for most static pages:'
  type: HowTo
tags:
- Java
- HTML Parsing
- CSS Extraction
title: 在 Java 中按类选择 HTML 元素 – 完整指南
url: /zh/java/css-html-form-editing/select-html-element-by-class-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中按类选择 HTML 元素 – 完整指南

是否曾经需要 **在 Java 中按类选择 HTML 元素**，却不知从何入手？你并不孤单——许多开发者在编写爬虫、测试 UI 组件或从静态页面生成报告时都会遇到这个难题。在本教程中，我们将加载一个 HTML 文件，解析文档，并 **提取目标元素的 CSS color 属性**，全部使用纯 Java 代码实现。

我们会从配置合适的库开始，直到处理缺失样式或内联覆盖等边缘情况。完成后，你将能够轻松回答 *“如何获取元素颜色”* 这类问题，并拥有一段可在任何项目中直接使用的代码片段。没有废话，只有实用、可直接运行的解决方案。

## 前置条件

在开始之前，请确保你具备以下条件：

- **Java 11+**（代码在任何近期 JDK 上均可运行）
- **Maven** 或 **Gradle** 用于管理依赖（示例中使用 Maven）
- 基本的 HTML 与 CSS 概念
- 一个简单的 HTML 文件（我们将其命名为 `sample.html`），放置在已知目录下

如果上述任意一点你不熟悉，请先停下来完成相应准备——等代码顺利运行时，你会感谢自己的细致。

## 第一步：在 Java 中加载 HTML 文件

首先需要 **以 Java 方式加载 HTML 文件**，即将文件读取到内存并交给解析器。完成此任务的事实标准库是 **jsoup**，它是一个轻量级、MIT 许可证的 HTML 解析器，能够优雅地处理不规范的标记。

### 添加 jsoup 依赖

如果使用 Maven，在 `pom.xml` 中加入以下内容：

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

对于 Gradle，则添加：

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

### 加载文档

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlColorExtractor {

    public static void main(String[] args) {
        // Adjust the path to point to your actual sample.html location
        File input = new File("YOUR_DIRECTORY/sample.html");
        try {
            // Parse the file using UTF-8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Proceed to element selection...
            extractColor(doc);
        } catch (IOException e) {
            System.err.println("Failed to load HTML file: " + e.getMessage());
        }
    }
```

**为什么这样做很重要：** `Jsoup.parse(File, String)` 会读取文件并构建一个类似 DOM 的 `Document` 对象，这是任何 **parse html document java** 操作的基础。它还会对 HTML 进行规范化，免去因标签错位导致的逻辑错误。

## 第二步：按类选择 HTML 元素

有了 `Document` 后，我们可以使用 CSS‑style 查询选择器 **按类选择 html element**。这与浏览器查询 DOM 的方式相同，使代码直观易懂。

```java
import org.jsoup.nodes.Element;

private static void extractColor(Document doc) {
    // Example: pick the first <p> with class "intro"
    Element para = doc.selectFirst("p.intro");
    if (para == null) {
        System.out.println("No <p class=\"intro\"> element found.");
        return;
    }
    // Continue to CSS extraction...
    getComputedColor(para);
}
```

**解释：**  
- `doc.selectFirst("p.intro")` 直接对应 “查找 class 属性包含 `intro` 的 `<p>` 元素”。  
- 如果选择器返回 `null`，我们会优雅地中止——这是 HTML 结构变化时常见的边缘情况。

## 第三步：获取元素颜色（提取 CSS 属性值）

jsoup 本身并不会为你计算样式，因为它不是浏览器引擎。不过，我们仍然可以通过读取 `style` 属性或手动加载外部样式表来实现 **how to get element color**。

### 3A. 内联样式（快速路径）

如果元素直接在 `style` 中定义了 `color`：

```java
private static void getComputedColor(Element element) {
    // Check for an inline style first
    String inlineStyle = element.attr("style"); // e.g., "color: #222; font-weight: bold;"
    String color = extractColorFromStyle(inlineStyle);
    if (color != null) {
        System.out.println("Computed color (inline): " + color);
        return;
    }
    // Fallback to external stylesheet parsing...
    System.out.println("No inline color found; attempting stylesheet lookup.");
}
```

从原始 style 字符串中提取 `color` 声明的辅助方法：

```java
private static String extractColorFromStyle(String style) {
    if (style == null || style.isEmpty()) return null;
    // Split by semicolon, then look for "color:"
    for (String part : style.split(";")) {
        String trimmed = part.trim().toLowerCase();
        if (trimmed.startsWith("color:")) {
            return trimmed.substring(6).trim(); // Return everything after "color:"
        }
    }
    return null;
}
```

### 3B. 外部样式表（完整功能）

如果颜色来源于外部 CSS 文件，则需要加载该样式表并自行实现层叠规则。下面是一种 **简化** 的实现方式，适用于大多数静态页面：

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;
import java.util.HashMap;
import java.util.Map;

private static void getComputedColor(Element element) {
    // Inline check as before...
    String inlineColor = extractColorFromStyle(element.attr("style"));
    if (inlineColor != null) {
        System.out.println("Computed color (inline): " + inlineColor);
        return;
    }

    // Load all linked CSS files (naïve approach)
    Document doc = element.ownerDocument();
    Elements links = doc.select("link[rel=stylesheet]");
    Map<String, String> cssRules = new HashMap<>();

    for (Element link : links) {
        String href = link.absUrl("href");
        try {
            String css = Jsoup.connect(href).ignoreContentType(true).execute().body();
            parseCssRules(css, cssRules);
        } catch (IOException e) {
            System.err.println("Failed to load stylesheet: " + href);
        }
    }

    // Resolve the most specific rule for the element’s class
    String className = element.className(); // e.g., "intro"
    String selector = "." + className; // ".intro"
    String color = cssRules.get(selector);
    if (color != null) {
        System.out.println("Computed color (external): " + color);
    } else {
        System.out.println("Color not found in inline style or linked stylesheets.");
    }
}
```

**解析 CSS – 一个小型辅助（并非完整解析器）：**

```java
private static void parseCssRules(String css, Map<String, String> map) {
    // Very basic: split on '}' then on '{' to get selector and declarations
    String[] blocks = css.split("}");
    for (String block : blocks) {
        String[] parts = block.split("\\{");
        if (parts.length != 2) continue;
        String selector = parts[0].trim(); // e.g., ".intro"
        String declarations = parts[1].trim(); // e.g., "color: rgb(34,34,34);"
        String color = extractColorFromStyle(declarations);
        if (color != null) {
            map.put(selector, color);
        }
    }
}
```

**为什么可行：**  
- 我们通过 `Jsoup.connect(...).ignoreContentType(true)` 获取每个链接的样式表，将 CSS 当作纯文本处理。  
- `parseCssRules` 会构建一个 selector → `color` 值的映射表。  
- 最后，我们在该映射表中查找元素的类选择器（`.intro`）。这在简单场景下模拟了层叠效果；若需处理复杂选择器，则需要完整的 CSS 引擎，这超出本演示的范围。

## 第四步：将计算得到的颜色输出到控制台

将上述所有步骤组合起来，最终的 `main` 方法会打印出发现的颜色：

```java
    public static void main(String[] args) {
        File input = new File("YOUR_DIRECTORY/sample.html");
        try {
            Document doc = Jsoup.parse(input, "UTF-8");
            Element para = doc.selectFirst("p.intro");
            if (para == null) {
                System.out.println("Target element not found.");
                return;
            }
            // Try inline first, then external CSS
            String color = extractColorFromStyle(para.attr("style"));
            if (color != null) {
                System.out.println("Computed color: " + color);
                return;
            }
            // Load external stylesheets (simplified)
            Map<String, String> cssMap = new HashMap<>();
            for (Element link : doc.select("link[rel=stylesheet]")) {
                String href = link.absUrl("href");
                String css = Jsoup.connect(href).ignoreContentType(true).execute().body();
                parseCssRules(css, cssMap);
            }
            String classSelector = "." + para.className();
            String externalColor = cssMap.get(classSelector);
            System.out.println("Computed color: " + (externalColor != null ? externalColor : "unknown"));
        } catch (IOException e) {
            System.err.println("Error: " + e.getMessage());
        }
    }
}
```

**预期输出**（假设 `sample.html` 包含 `<p class="intro" style="color: #222;">`）：

```
Computed color: #222
```

或者，若颜色定义在外部样式表中：

```
Computed color: rgb(34, 34, 34)
```

## 专业技巧与常见陷阱

- **相对 URL：** `link.absUrl("href")` 会自动根据文档所在位置解析相对路径——务必使用，否则可能抓取到错误的资源。

## 接下来该学习什么？

以下教程与本指南紧密相关，能够帮助你在已有技术之上进一步扩展。每篇资源都提供完整可运行的代码示例，并配有逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方式。

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}