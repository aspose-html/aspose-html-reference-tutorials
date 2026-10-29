---
category: general
date: 2026-05-31
description: 在 Java 中使用 Aspose HTML 将网页渲染为 PNG 时禁用外部图像。学习如何在沙箱中安全加载网页并将 HTML 文档保存为
  PNG。
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: zh
og_description: 在 Java 中将网页渲染为 PNG 时禁用外部图像。本分步指南展示了如何在沙箱中加载网页并将 HTML 文档保存为 PNG。
og_title: 在 Java 中渲染网页为 PNG 时禁用外部图片
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: 在 Java 中将网页渲染为 PNG 时禁用外部图像
url: /zh/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中渲染网页为 PNG 时禁用外部图片

是否曾在 Java 中将网页渲染为 PNG 时**禁用外部图片**？也许你在构建一个必须与公共互联网隔离的缩略图服务，或只是想确保在转换过程中不会泄露任何第三方图片。无论哪种情况，你都来对地方了。

在本教程中，我们将演示如何在沙箱中加载网页、关闭外部图片获取，并最终将 HTML 文档保存为 PNG 文件——全部使用 Aspose.HTML for Java。完成后，你将拥有一个可直接运行的示例，以及一些实用技巧，帮助你规避常见陷阱。

## 你将学到的内容

- 使用 Aspose.HTML 的 `Converter` **将 HTML 渲染为图像（Java）**。
- **在沙箱中加载网页** 的完整步骤，包括自定义视口和 DPI。
- 在渲染页面时 **禁用外部图片** 所需的配置。
- 如何 **将 HTML 文档保存为 PNG**（或其他受支持的格式）到磁盘。
- 边缘情况处理、性能提示以及故障排除建议。

### 前置条件

- 已安装 Java 8 或更高版本（代码同样适用于 JDK 11+）。
- 使用 Maven 或 Gradle 引入 Aspose.HTML for Java 库。
- 具备基本的 Java 语法和异常处理知识。
- 初始页面加载需要网络连接（除非你本地提供 HTML）。

> **专业提示：** 如果你在公司代理后工作，请在运行示例前设置 JVM 的 `http.proxyHost` 和 `http.proxyPort` 属性。

---

## 第一步：设置项目并添加 Aspose.HTML

首先——添加 Aspose.HTML 依赖。如果你使用 Maven，将以下内容放入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle 的等价写法是：

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

库加入类路径后，即可开始编写代码。

---

## 第二步：使用沙箱环境 **禁用外部图片**

解决方案的核心是 `DocumentSandbox`。将 *allowExternalImages* 标志设为 `false`，即可指示 Aspose.HTML 忽略指向沙箱外部的 `<img>` 标签。这正是 **禁用外部图片** 的实现机制。

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **为何重要：** 若不使用沙箱，渲染器会尝试下载页面引用的每一张图片，这可能导致速度慢、可靠性差，甚至带来安全风险。将标志设为 `false` 可保证一次干净、独立的渲染过程。

---

## 第三步：**在沙箱中加载网页**  

现在将 Aspose.HTML 指向我们想要捕获的 URL。`HTMLDocument` 构造函数接受沙箱实例，自动应用我们刚才定义的限制。

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

如果页面大量依赖外部脚本进行布局，你可能会发现内容缺失，因为我们也关闭了脚本。在这种情况下，可将 `allowExternalScripts` 标志设为 `true`，同时保持 `allowExternalImages` 为 `false`。

---

## 第四步：**将网页渲染为 PNG**  

文档加载完成后，使用 `Converter.convert` 只需一行代码即可将其转换为图像。`ImageSaveOptions` 对象让你选择输出格式，这里我们选用 PNG。

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

生成的文件 `sandboxed.png` 包含了页面的快照 **但不包含任何外部图片**——仅保留内联 SVG 或 base64 编码的图形（如果有的话）。

---

## 第五步：验证输出并调试常见问题

运行程序后，用任意图像查看器打开 `sandboxed.png`。你应该能看到页面的布局、文字和 CSS 样式，但所有 `<img src="http://…">` 元素将为空（通常表现为白色矩形或直接省略）。

### 常见故障及解决办法

| 症状 | 可能原因 | 解决方案 |
|---|---|---|
| 页面为空白 | 目标 URL 阻止了请求（如 Cloudflare） | 为沙箱的 user‑agent 添加合适的请求头，或使用代理。 |
| 字体缺失 | 字体文件托管在外部 | 本地安装字体或使用 `@font-face` 并嵌入 data URI。 |
| 布局错位 | CSS 引用了被阻止的外部样式表 | 将 `allowExternalScripts` 设为 `true` 仅用于加载 CSS，然后重新运行。 |
| `java.lang.OutOfMemoryError` | 在高 DPI 下渲染超大页面 | 减小视口尺寸或 DPI，或增大 JVM 堆内存 (`-Xmx2g`)。 |

---

## 第六步：扩展示例 – 保存为其他格式

相同代码同样适用于 JPEG、BMP，甚至 PDF。只需更改 `SaveFormat` 枚举：

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

如果需要 PDF，改用 `PdfSaveOptions` 替代 `ImageSaveOptions`，并相应修改文件扩展名。

---

## 完整可运行示例（复制‑粘贴即用）

下面是 **完整、可直接运行的程序**。新建一个 Java 类，粘贴以下代码，确保 `output` 目录已创建，然后运行。

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**预期输出**（控制台）：

```
PNG image saved to: output/sandboxed.png
```

打开 `sandboxed.png`——你会看到页面已 **在不加载任何外部图片的情况下** 渲染完成。

---

## 常见问答

**问：我还能显示 HTML 中内嵌的图片吗？**  
答：可以。内联的 `data:` URI 或 base64 编码图片被视为文档的一部分，会出现在 PNG 中。

**问：如果只想屏蔽部分外部图片，该怎么办？**  
答：沙箱是全开或全关的开关。若需细粒度控制，请自行下载允许的图片，转为 data URI 后再渲染。

**问：此方法能在无头服务器上运行吗？**  
答：完全可以。Aspose.HTML 是纯 Java 库，无需显示服务器或浏览器引擎。

**问：它与 Selenium 或 Puppeteer 有何区别？**  
答：Selenium 驱动真实浏览器，重量大且难以沙箱化。Aspose.HTML 直接在内存中渲染 HTML，提供确定的性能和更易实现的安全控制，例如 **禁用外部图片**。

---

## 结论

现在，你已经掌握了在 Java 中 **渲染网页为 PNG 时禁用外部图片** 的完整方案。通过 `DocumentSandbox`，你可以严格控制允许的外部资源，确保安全性和可复现性。接下来，你可以尝试不同的视口尺寸、DPI 设置或输出格式——每一次微调都能为生成缩略图、预览图或归档快照打开新思路。

准备好迎接下一个挑战了吗？试着并行渲染一批 URL，或将此逻辑集成到 Spring Boot 微服务中，实现按需返回 PNG。结合 Aspose.HTML 的灵活性和 Java 的并发工具，天地无限。

祝编码愉快，别忘了在评论区分享你的成功案例！

## 接下来你可以学习

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}