---
category: general
date: 2026-09-29
description: 使用 Java 在 HTML 文件中更改背景颜色的 JavaScript。学习在 Java 中加载 HTML、在 HTML 中运行 JS，并使用
  Java 修改 HTML 以实现新页面背景。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: zh
lastmod: 2026-09-29
og_description: 使用 Java 在 HTML 页面中更改背景颜色的 JavaScript。本教程展示了如何在 Java 中加载 HTML、在 HTML
  中运行 JS，以及以编程方式设置页面背景。
og_image_alt: Screenshot of Java code that changes the page background color
og_title: 使用 Java 更改 JavaScript 背景颜色 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: 如何使用 Java 更改 JavaScript 背景颜色
url: /zh/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Java 更改背景颜色（javascript）

如果您需要在现有的 HTML 文件中 **change background color javascript**，可以完全在 Java 中完成，而无需打开浏览器。本教程向您展示如何 **load html in java**，执行一小段 JavaScript 代码，然后 **modify html with java**，以更新页面的背景。

该解决方案使用开源的 **HTMLUnit** 库，它提供了一个无头浏览器，能够像真实浏览器一样评估 JavaScript。阅读完本指南后，您将拥有一个可复用的方法，能够 **sets page background** 为任意您选择的颜色。

## 前置条件

| 您需要的内容 | 为什么重要 |
|---------------|----------------|
| Java 8 或更高版本 | HTMLUnit 至少需要 Java 8。 |
| Maven 或 Gradle 构建工具 | 自动获取 HTMLUnit 依赖。 |
| 您想编辑的 HTML 文件（例如 `input.html`） | 将被加载并修改的源文档。 |

将 HTMLUnit 添加到您的项目中：

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **专业提示：** 使用最新的稳定版 HTMLUnit，以获得最准确的 JavaScript 引擎。

## 更改背景颜色（javascript）– 在 Java 中加载 HTML

第一步是将 HTML 文档加载到 `HTMLPage` 对象中。这为您提供类似 DOM 的 API 和 JavaScript 执行上下文。

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*为什么重要*：`WebClient` 创建了一个沙盒环境，JavaScript 可以在其中运行，因此您可以 **run js in html**，完全像用户的浏览器一样。

## 在 html 中运行 js 以设置页面背景

页面加载后，您可以评估任意 JavaScript 表达式。下面的代码片段会更改 `<body>` 元素的 `backgroundColor` 样式。

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*解释*：  
- `document.body.style.backgroundColor` 是页面背景的标准 DOM 属性。  
- 通过调用 `eval`，我们 **run js in html**，无需真实的浏览器窗口。  
- 该方法可复用于任何颜色，满足 **set page background** 的需求。

## 使用 Java 修改 html 并保存结果

脚本运行后，DOM 会反映新的样式。您现在可以将更新后的 HTML 写回磁盘。

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

将所有内容组合在一起，即可得到一个可运行的完整程序：

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### 预期输出

运行程序会输出：

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

在任意浏览器中打开 `js_modified.html`，页面会显示淡蓝色背景，确认 **change background color javascript** 操作成功。

## 常见变体和边缘情况

| 情况 | 处理方式 |
|-----------|------------------|
| **不同的颜色格式** | 传入任意 CSS 兼容的值（`"red"`、`"#ff0000"`、`"rgb(255,0,0)"`）。 |
| **缺少 `<body>` 标签** | 脚本会静默失败；您可以先使用 `page.getFirstByXPath("//body")` 确保 `<body>` 存在。 |
| **大型 HTML 文件** | 禁用 CSS（`setCssEnabled(false)`），仅启用所需的 JavaScript 功能，以降低内存使用。 |
| **运行多个脚本** | 反复调用 `changeBackground`，或创建接受 JavaScript 命令列表的实用方法。 |

## 结论

现在，您已经了解如何通过在 Java 中加载 HTML 文件来 **change background color javascript**，**run js in html**，以及 **modify html with java**，从而 **set page background** 为任意您选择的颜色。上述完整示例使用最新的 HTMLUnit 库，可集成到更大的自动化流水线中，例如批量处理 HTML 报告或准备电子邮件模板。

**下一步**  
- 探索其他 DOM 操作（例如，插入元素、移除脚本）。  
- 将此方法与 PDF 渲染器结合，以生成带样式页面的 PDF。  
- 如果需要完整的浏览器兼容性，可尝试使用 Selenium WebDriver 等其他无头引擎。

祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [获取计算样式 Java – 从 HTML 中提取背景颜色](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [如何加载 HTML、设置设备 DPI 并读取背景颜色](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [在 Java 中从 JavaScript 生成 HTML – 完整分步指南](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}