---
category: general
date: 2026-01-01
description: 学习如何使用 Java 查询 HTML，如何选择 CSS，以及通过实际示例和节点计数从 HTML 中提取元素。
draft: false
keywords:
- how to query html
- how to select css
- extract elements from html
- select multiple css classes
- how to count nodes
language: zh
og_description: 掌握在 Java 中查询 HTML 的方法，学习如何选择 CSS，从 HTML 中提取元素并使用真实代码示例统计节点。
og_title: 如何在 Java 中查询 HTML – 完整教程
tags:
- Java
- HTML parsing
- Aspose.HTML
title: 如何在 Java 中查询 HTML – 完整教程
url: /zh/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中查询 HTML – 完整教程

有没有想过 **如何在 Java 程序中查询 HTML** 而不抓狂？你并不是唯一的遇到这种困惑的人。许多开发者在需要从静态目录获取数据或抓取一个简单页面时会卡住，而常规的 DOM 技巧显得笨拙。  

好消息是，只需几行代码就能加载 HTML 文件、运行 XPath 或 CSS 选择器，甚至统计你关心的节点——全部在一个整洁的流程中完成。在本指南中，我们将逐步演示 **如何查询 HTML**、**如何选择 CSS**，并展示如何 **从 HTML 中提取元素**、**选择多个 CSS 类**，以及 **如何统计节点**，使用 Aspose.HTML for Java。

## 你将学到

- 从磁盘或 URL 加载 HTML 文档。  
- 使用 XPath 查找符合复杂条件的元素。  
- 应用 CSS 选择器，包括多类查询。  
- 以编程方式统计结果。  
- 实际场景中的技巧、陷阱和变体。

*前置条件*：Java 8 及以上、Maven 或 Gradle，以及 Aspose.HTML for Java 库的副本（免费试用版足以进行实验）。

---

![如何查询 HTML 示例](https://example.com/images/query-html.png "展示如何使用 Java 查询 HTML 的截图")

## 如何查询 HTML – 加载文档

在提出任何查询之前，你需要一个文档对象来进行检查。Aspose.HTML 的 `HTMLDocument` 类负责这项繁重工作。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document you want to query
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");
```

> **为什么这很重要** – 加载文件会在内存中创建一个 DOM 树。之后你可以同时运行 XPath 和 CSS 查询，而无需担心网络延迟或标记错误。如果文件未找到，Aspose 会抛出明确的 `FileNotFoundException`，让调试变得轻松。

### 专业提示
如果你从远程站点获取 HTML，只需将 URL 字符串传递给 `HTMLDocument`——Aspose 会为你抓取并解析。

## 如何选择 CSS – 使用 CSS 选择器

DOM 准备好后，使用 CSS 选择节点只需一行代码。让我们获取所有拥有 `featured` 或 `highlight` 类的元素。

```java
        // Step 2: Locate elements marked as featured or highlighted using a CSS selector
        List<Element> featuredElements = document.selectCss(".featured, .highlight");

        // Step 3: Output the number of elements found by the CSS selector
        System.out.println("Featured elements: " + featuredElements.size());
```

> **解释** – 选择器 `.featured, .highlight` 告诉引擎返回 *任何* `class` 属性包含 `featured` **或** `highlight` 的元素。这是单次查询中 **选择多个 CSS 类** 的标准做法。

### 边缘情况
如果一个元素同时包含这两个类（例如 `<div class="featured highlight">`），它只会在结果列表中出现 **一次**，避免重复计数。

## 从 HTML 中提取元素 – 结合 XPath 与 CSS

当需要关系逻辑时，XPath 大显身手，例如 “所有 `<book>` 节点且价格超过 30”。下面是原示例中的完整代码片段：

```java
        // Step 4: Find all <book> elements with a price greater than 30 using XPath
        List<Element> expensiveBooks = document.selectXPath("//book[price>30]");

        // Step 5: Output the number of books that match the XPath query
        System.out.println("Expensive books count: " + expensiveBooks.size());
```

> **为什么使用 XPath？** – XPath 可以直接评估数值比较（`price>30`），而 CSS 做不到。它还允许你在不写额外代码的情况下遍历父子关系。

### 变体
如果你想获取这些高价书籍的 *标题*，可以再链式执行一次查询：

```java
        List<Element> titles = expensiveBooks.get(0).selectXPath("./title");
        System.out.println("First expensive book title: " + titles.get(0).getTextContent());
```

## 选择多个 CSS 类 – 高级选择器技巧

有时你需要定位 **同时** 拥有多个类的元素，例如 `class="product featured"`。对应的 CSS 语法是没有逗号的串联选择器。

```java
        // Example: select <div> elements that are both .product and .featured
        List<Element> productFeatured = document.selectCss("div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured.size());
```

> **关键点** – 类名之间不能有空格；空格表示“后代”。当你 **选择多个 CSS 类** 并让它们共同作用于组件时，这种模式至关重要。

## 如何统计节点 – 获得精确计数

统计节点通常是数据提取流水线的最后一步。你已经在每次查询后看到使用 `list.size()`，现在让我们把它封装成可复用的帮助方法。

```java
    /**
     * Returns the count of elements that match the given CSS selector.
     */
    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    /**
     * Returns the count of elements that match the given XPath expression.
     */
    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        System.out.println("Expensive books: " + countByXPath(doc, "//book[price>30]"));
        System.out.println("Featured items: " + countByCss(doc, ".featured, .highlight"));
        System.out.println("Product‑featured divs: " + countByCss(doc, "div.product.featured"));
    }
```

> **为什么要封装？** – 将计数逻辑集中可以让代码更易于测试，减少重复，也能为后续阅读者明确 **如何统计节点**。

### 常见陷阱
- **类属性中的空白** – `"featured "`（尾随空格）仍然匹配 `.featured`，因为选择器会去除空白。  
- **大小写敏感** – 在 XML 模式下，HTML 类名区分大小写；确保源 HTML 使用统一的大小写。

## 完整工作示例

将所有内容组合在一起，下面是一个可以直接复制粘贴到 IDE 中的独立程序：

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {

    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        // Load the HTML file (adjust the path as needed)
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        // XPath: books priced over 30
        int expensiveBooks = countByXPath(document, "//book[price>30]");
        System.out.println("Expensive books count: " + expensiveBooks);

        // CSS: featured or highlighted elements
        int featured = countByCss(document, ".featured, .highlight");
        System.out.println("Featured elements: " + featured);

        // CSS: elements that are both .product and .featured
        int productFeatured = countByCss(document, "div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured);
    }
}
```

**预期输出**（假设使用典型的 `catalog.html`）：

```
Expensive books count: 4
Featured elements: 7
Product‑featured divs: 2
```

如果你的文件匹配的节点更少，数字会相应调整——没有意外。

---

## 结论

我们已经介绍了使用 Aspose.HTML for Java **如何查询 HTML**，演示了 **如何选择 CSS**，展示了 **如何从 HTML 中提取元素**，探讨了 **选择多个 CSS 类**，并解释了 **如何可靠地统计节点**。  

关键要点是：文档只需加载一次，然后复用同一个 `HTMLDocument` 实例，就可以在不牺牲性能的前提下混合使用 XPath 与 CSS 查询。  

准备好下一步了吗？尝试链式选择器来获取属性值（`@href`、`@src`），或将结果集导出为 JSON 供下游处理。你也可以探索分页处理，如果你的源 HTML 跨越多个页面。

遇到棘手的选择器或无法解决的边缘情况？在下方留言，让我们一起排查。祝查询愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}