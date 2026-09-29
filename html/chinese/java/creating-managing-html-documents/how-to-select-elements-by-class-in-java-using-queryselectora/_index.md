---
category: general
date: 2026-09-29
description: 学习如何按类选择元素、从文件读取HTML，并在 Java 中查找外部链接。本分步指南涵盖高效遍历 NodeList 的方法。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: zh
lastmod: 2026-09-29
og_description: 在 Java 中按类选择元素，从文件读取 HTML，并使用 querySelectorAll 查找外部链接。请参照完整示例遍历 NodeList。
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: 在 Java 中按类选择元素 – 使用 querySelectorAll 的完整指南
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: 如何在 Java 中使用 querySelectorAll 按类选择元素
url: /zh/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 querySelectorAll 按类选择元素

如果您需要在 Java 中处理 HTML 文件时**按类选择元素**，本指南将准确展示如何操作。您将学习如何从文件读取 HTML，使用 `querySelectorAll` 查找外部链接，并安全地遍历得到的 `NodeList`。

在 Java 中处理 HTML 往往感觉笨重，但现代库提供了简洁的基于 CSS 选择器的 API。下面的示例使用 **jsoup**（版本 1.17.2），因为它实现了 `querySelectorAll` 风格的选择器，并返回类似 `NodeList` 的 `Elements` 集合。您可以根据需要将相同逻辑迁移到其他 DOM 实现。

## 前置条件

在开始之前，请确保您具备：

* 已安装 JDK 17 或更高版本。
* 用于依赖管理的 Maven 或 Gradle。
* 对 Java 流和 DOM 模型有基本了解。

将 jsoup 添加到项目中：

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## 步骤 1：从文件读取 HTML

第一步是从磁盘加载 HTML 文档。`Jsoup.parse(Path, Charset)` 读取文件并构建可供查询的 DOM 树。

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*为什么这很重要*：一次性加载文件可避免在后续遍历元素时重复 I/O。`Document` 对象保存完整的 DOM，能够快速执行选择器查询。

## 步骤 2：使用 `querySelectorAll` 按类选择元素

现在文档已在内存中，您可以使用 CSS 选择器**按类选择元素**。选择器 `"a.external"` 匹配带有 `external` 类的 `<a>` 标签——正是您需要的**查找外部链接**方式。

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*为什么这很重要*：使用类选择器既直观又高效。库会将选择器转换为优化的遍历，实现无需手动遍历每个节点。

## 步骤 3：在 Java 中遍历 NodeList（Elements）

`Elements` 实现了 `Iterable<Element>`，因此您可以使用标准的 `for‑each` 循环**遍历 NodeList Java**对象。下面的循环会打印每个链接的 `href` 属性。

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*为什么这很重要*：直接遍历保持代码可读性，并在仅需简单输出时避免将集合转换为流的开销。

## 完整可运行示例

将上述三步组合起来即可得到一个可独立运行的程序，您可以在命令行执行。

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### 预期输出

假设 `input.html` 包含：

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

运行程序后输出：

```
External link: https://example.com
External link: https://openai.com
```

## 专业技巧与常见陷阱

* **编码很重要** – 始终使用 UTF‑8（或与源文件匹配的字符集）读取文件。错误的编码会导致属性值中的字符损坏。
* **多个类** – 如果元素拥有多个类（例如 `class="btn external"`），选择器 `"a.external"` 仍然匹配，因为 CSS 类选择器检查的是 token 是否存在，而不是完整字符串。
* **性能提示** – 若仅需 `href` 属性，可直接使用 `doc.select("a.external[href]").eachAttr("href")` 获取。这避免为每个匹配创建完整的 `Element` 对象。
* **空值安全** – `link.attr("href")` 在属性缺失时返回空字符串，因此在打印前无需进行 null 检查。

## 常见问题

**问：这在缺少 `<html>` 根元素的 HTML 片段上是否有效？**  
答：是的。`Jsoup.parse` 会将输入视为片段并自动添加缺失的根元素，使选择器能够在片段的 body 上工作。

**问：可以在不使用 jsoup 的情况下使用 `querySelectorAll` 吗？**  
答：标准的 Java DOM API（`org.w3c.dom`）不包含 `querySelectorAll`。**HTMLUnit** 或 **jodd-lagarto** 等库提供类似方法。这里展示的模式——加载、使用 CSS 选择、遍历——保持不变。

**问：如果我需要修改链接而不是仅打印它们怎么办？**  
答：获取每个 `Element` 后，您可以调用 `link.attr("href", "newUrl")`，随后使用 `Files.writeString` 将文档写回磁盘。

## 结论

现在您已经掌握了如何使用 `querySelectorAll`‑风格的选择器**按类选择元素**、**从文件读取 HTML**、**查找外部链接**以及**在 Java 中遍历 NodeList**。完整示例展示了一个简洁、可用于生产环境的工作流，您可以将其嵌入更大的爬取或转换流水线中。

接下来，您可以探索相关主题，例如 **使用 HTMLUnit 解析动态内容**、**将修改后的 HTML 写回磁盘**，或 **使用 Java 流将链接 URL 收集到列表**。这些都基于本文演示的基于类的选择核心技术。祝编码愉快！

## 接下来您可以学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何在 Java 中查询 HTML – 选择元素、按属性过滤并获取文本](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [遍历 NodeList Java – 读取 HTML 并获取 Image src](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [在 Aspose.HTML for Java 中从文件加载 HTML 文档](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}