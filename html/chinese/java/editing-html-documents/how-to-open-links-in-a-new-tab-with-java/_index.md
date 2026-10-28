---
category: general
date: 2026-10-28
description: 学习如何通过在 Java 中解析 HTML、查找外部链接并添加 target="_blank" 来在新标签页打开链接。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: zh
lastmod: 2026-10-28
og_description: 使用 Java 在新标签页打开链接：解析 HTML，查找外部链接，添加 target="_blank"，并保存修改后的 HTML。
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: 使用 Java 在新标签页打开链接——一步一步指南
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: 如何使用 Java 在新标签页中打开链接
url: /zh/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Java 在新标签页打开链接

如果你需要 **在新标签页打开链接**，并且文件是静态 HTML，本指南将一步步教你如何实现。你将学习 **在 Java 中解析 HTML**、**查找外部链接**、**添加 target="_blank"**，以及 **保存修改后的 HTML**，全部在 IDE 中完成。

在新浏览器标签页打开外部链接可以提升用户体验，并且让访客仍然停留在原页面。下面的解决方案适用于任何 HTML 文档，只需使用流行的 jsoup 库，且可在 Java 8 或更高版本上运行。

## 前置条件

在开始之前，请确保你已经：

* 安装了 JDK 8 或以上  
* 有一个构建工具（Maven 或 Gradle）来引入 **jsoup** 依赖  
* 拥有一个包含 `external` 类的 `<a>` 标签的 HTML 文件

你不需要 Web 服务器或额外的框架——jsoup 在本地即可完成所有工作。

## 第一步：在项目中配置 jsoup

将 jsoup 添加为依赖。如果使用 Maven，请在 `pom.xml` 中加入：

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

如果使用 Gradle，请在 `build.gradle` 中添加以下行：

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

这些坐标会拉取截至 2026 年 10 月的最新稳定版本。同步后，你就可以在 Java 源文件中导入 `org.jsoup` 包了。

## 第二步：解析 HTML 文档

解析文件是实现 **在新标签页打开链接** 的第一步。`Jsoup.parse` 方法会把文件读取为可变的类似 DOM 的结构。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*为什么重要*：`Document` 提供了 CSS 样式的选择器，使得定位所需元素变得非常简单。

## 第三步：查找外部链接

现在定位所有带有 `external` 类的 `<a>` 元素。这正对应 **查找外部链接** 的需求。

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` 是匹配节点的集合。如果选择器返回空集合，说明你的 HTML 要么没有该类，要么使用了不同的命名约定——请相应地调整选择器。

## 第四步：为每个链接添加 `target="_blank"`

对 **查找外部链接** 返回的每个节点，设置 `target` 属性为 `_blank`。这完成了 **添加 target blank** 的步骤，并确保浏览器在新标签页中打开链接。

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

`attr` 方法会覆盖任何已有的 `target` 值，保证所有外部锚点的行为一致。

## 第五步：保存修改后的 HTML

在更新 DOM 后，将更改写回文件。这就完成了教程中的 **保存修改后的 html** 部分。

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` 会序列化整个文档，保留 jsoup 最初解析时的缩进和格式。

## 完整可运行示例

将所有步骤组合在一起，即可得到一个可直接复制、粘贴并运行的独立程序。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### 预期输出

假设 `sample.html` 内容如下：

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

运行程序后，`updated.html` 将会是：

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

只有外部链接被添加了 `target="_blank"` 属性，这意味着浏览器现在会在新标签页中打开它。

## 专业提示与常见陷阱

* **专业提示**：如果你希望将所有以 `http://` 或 `https://` 开头的链接视为外部链接，即使它们没有 CSS 类，也可以扩展选择器：`doc.select("a[href^=http]")`。  
* **边缘情况**：某些页面已经指定了 `target="_self"`；`attr` 调用会覆盖它，确保行为统一。  
* **性能**：对于非常大的 HTML 文件，考虑使用流式解析（`Jsoup.parse(File, String, String, Parser.htmlParser())`）以降低内存占用。  
* **测试**：在浏览器中打开 `updated.html` 并使用开发者工具检查链接——确认 `target` 属性已正确添加。

## 结论

现在，你已经拥有一个完整、可运行的 **在新标签页打开链接** 的 Java 解决方案。教程涵盖了 **在 Java 中解析 HTML**、**查找外部链接**、**添加 target blank**、以及 **保存修改后的 html**，全部依赖轻量级的 jsoup 库。

接下来，你可以：

* 将选择器扩展到处理其他链接模式（例如 `rel="external"`）。  
* 将此逻辑与构建步骤结合，批量处理项目中的所有 HTML 文件。  
* 将代码集成到更大的内容管理流水线中。

欢迎尝试不同的选择器或输出格式，并将你的成果分享给社区！

## 接下来你可以学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，提供完整的代码示例和逐步解释，帮助你进一步掌握 API 功能并探索替代实现方式。

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}