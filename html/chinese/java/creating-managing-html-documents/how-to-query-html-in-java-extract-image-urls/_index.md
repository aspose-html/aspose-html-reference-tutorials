---
category: general
date: 2026-03-05
description: 如何在 Java 中查询 HTML，读取 HTML 文件并提取图像。学习使用 Java 读取 HTML 文件、获取图像 URL，以及遍历
  NodeList。
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: zh
og_description: 如何在 Java 中查询 HTML 并检索图像 URL。本指南展示了如何读取 HTML 文件、定位图像以及遍历 NodeList。
og_title: 如何在 Java 中查询 HTML – 提取图片 URL
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: 如何在 Java 中查询 HTML —— 提取图片 URL
url: /zh/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中查询 HTML – 提取图片 URL

有没有想过 **如何在 Java 中查询 HTML** 并提取页面上的每张图片？你并不是唯一有此需求的开发者——大家经常需要读取 HTML 文件、抓取图片，然后对这些 URL 做进一步处理。在本教程中，我们将通过一个实用示例，完整演示 **如何查询 HTML**、以 Java 方式读取 HTML 文件，并以 Java 方式获取图片 URL。

我们使用 Aspose.HTML for Java，但其中的概念——XPath、CSS 选择器以及遍历 `NodeList`——同样适用于任何 DOM 库。阅读完本指南后，你将熟悉 **如何提取图片**、了解 **如何遍历 NodeList Java**，并拥有一段可以直接放入项目的可运行代码片段。

![How to query HTML in Java example](https://example.com/placeholder.png "How to query HTML in Java")

---

## 你将学到

- 从磁盘加载 HTML 文档（read HTML file Java）
- 使用 XPath 与 CSS 选择器定位 `<img>` 标签（how to extract images）
- 遍历得到的 `NodeList`（iterate over NodeList Java）
- 打印每张图片的 `src` 属性（get image URLs Java）

无需外部服务，也不需要复杂的构建工具——只需纯 Java 加上一个 Maven 依赖。

---

## 前置条件

- 已安装 Java 8 或更高版本
- 使用 Maven 或 Gradle 管理依赖
- 对 HTML 结构有基本了解
- 可选但有帮助：准备一个包含若干 `<figure><img …></figure>` 元素的简单 HTML 文件（`sample.html`）

满足上述条件后，即可开始。

---

## 步骤 1：Read HTML File Java – 加载文档

首先要把 HTML 加载到内存中。Aspose.HTML 的 `HTMLDocument` 类负责这项工作。可以把它想象成打开一本书，以便随时翻到任意页面。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**为什么这很重要：** 加载文件后会得到一个可以查询的 DOM 树。如果路径错误，会抛出 `FileNotFoundException`，因此在运行前请再次确认文件位置。

---

## 步骤 2：使用 XPath 定位图片 – How to Extract Images

XPath 是一种强大的查询语言，能够精准定位节点。这里我们查询每个带有 `alt` 属性的 `<figure>` 下的 `<img>`。

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**为什么使用 XPath？** 它简洁且即使 HTML 结构混乱也能工作。表达式 `//figure/img[@alt]` 的含义是：“在 `<figure>` 元素下的所有带有 `alt` 属性的 `<img>`”。如果需要根据其他属性过滤，只需修改方括号内的内容即可。

---

## 步骤 3：使用 CSS 选择器定位图片 – Alternative Way to Extract Images

有时你更喜欢 CSS 语法，因为它与样式表中的写法一致。`querySelectorAll` 接受的就是浏览器中使用的同样选择器。

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**为什么两种方式都演示？** 展示两者可以让你根据自己的习惯选择工具。实际项目中通常只会选用一种，但提供两种示例能让教程更完整。

---

## 步骤 4：Iterate Over NodeList Java – 获取图片 URL Java

现在我们已经得到一个集合，需要遍历它。这正是 **iterate over NodeList Java** 用武之地。我们将提取每张图片的 `src` 属性并打印出来。

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**为什么使用经典的 `for` 循环？** Aspose 的 `NodeList` 并未实现 `Iterable` 接口，增强的 `for‑each` 语法无法编译。使用索引循环是可靠的 **iterate over NodeList Java** 方式。

---

## 预期输出

将程序运行在如下示例 HTML 上：

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

将产生类似以下的输出：

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

如果你的文件中符合条件的 `<img>` 标签更多，输出的数量会相应增加。

---

## 常见坑点 & 专业提示

- **文件路径问题：** 使用绝对路径或将 `sample.html` 放在项目工作目录的相对位置。  
- **缺少 `alt` 属性：** 我们的 XPath/CSS 查询使用了 `[@alt]` 过滤。如果需要获取 *所有* 图片，请去掉属性过滤（`//figure/img` 或 `figure img`）。  
- **性能考虑：** 对于超大文档，可考虑使用流式解析器，但对于大多数网页抓取任务，DOM 方式已足够。  
- **编码问题：** Aspose.HTML 会遵循 HTML 中声明的字符集。如果出现乱码，请确保文件保存为 UTF‑8 编码。  

---

## 示例扩展

既然已经能够 **get image URLs Java**，接下来可以进一步：

1. 使用 `java.net.URL` 和 `Files.copy` **下载图片**。  
2. 将 URL **存入数据库**，以便后续处理。  
3. 根据文件扩展名进行过滤（`src.endsWith(".png")`）。  

这些都是在第 4 步循环基础上轻松实现的扩展。

---

## 结论

本指南从头到尾演示了 **如何在 Java 中查询 HTML**：加载文件、使用 XPath 与 CSS 选择器定位图片、以及 **遍历 NodeList Java** 并打印每张图片的 `src`。现在，你已经掌握了 **如何提取图片** 的核心技巧，并且了解了 **如何读取 HTML 文件 Java** 的完整流程。

欢迎根据自己的抓取需求自行改造代码——无论是提取其他属性、处理 `<a>` 标签，还是将 URL 交给下载器，模式都是相同的：加载 → 查询 → 遍历 → 操作。

有问题或想分享有趣的使用案例？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}