---
category: general
date: 2026-04-19
description: 使用 Java 快速从 MHTML 中提取 HTML。了解如何将 MHTML 转换为 HTML、提取邮件正文、将字符串写入文件以及处理 MHT
  转换。
draft: false
keywords:
- extract html from mhtml
- convert mhtml to html
- extract email body
- write string to file
- convert mht to html
language: zh
og_description: 在 Java 中从 MHTML 提取 HTML。本指南展示如何将 MHTML 转换为 HTML，提取邮件正文，并将字符串写入文件。
og_title: 从 MHTML 中提取 HTML – Java 步骤指南
tags:
- Java
- Aspose.HTML
- Email Processing
title: 从 MHTML 中提取 HTML – 完整的 Java 指南
url: /zh/java/creating-managing-html-documents/extract-html-from-mhtml-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 MHTML 提取 HTML – 完整 Java 指南

是否曾需要 **从 MHTML 提取 HTML**，却不知道从何入手？也许你收到了一封归档邮件（`.mht`），想要获取干净的正文用于网页预览，或者你正在编写一个迁移脚本，将旧版归档转换为现代 HTML 页面。无论哪种情况，问题都是一样的：你拥有一个单文件的网页归档，需要从中拿到原始的 HTML 标记。

好消息是？只需几行 Java 代码和 Aspose.HTML 库，你就可以 **将 MHTML 转换为 HTML**，提取邮件正文，甚至将该字符串写入文件——全部在 IDE 中完成。在本教程中，我们将完整演示整个过程，解释每一步的意义，并展示如何处理常见的边缘情况，如资源缺失或非 UTF‑8 编码。

> **快速回顾：** 完成本指南后，你将能够 **提取邮件正文**、**将 MHTML 转换为 HTML**，以及 **将字符串写入文件**，并拥有一段干净、可复用的代码片段，适用于任何 `.mht` 或 `.mhtml` 文件。

---

## 需要的准备

在开始之前，请确保你具备以下环境：

- **Java 17+**（代码使用了 try‑with‑resources 语法，自 Java 7 起可用，但推荐使用当前 LTS 的 Java 17）。
- **Aspose.HTML for Java** JAR 包已加入类路径。你可以从 [Aspose 网站](https://products.aspose.com/html/java/) 下载，或通过 Maven 引入：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

- 一个待处理的 **`.mht` 或 `.mhtml`** 示例文件。演示中我们将其命名为 `email.mht`，并放置在 `YOUR_DIRECTORY` 下。

就这些——无需额外框架，也不需要重量级解析器。只要纯 Java 加上一套文档完善的库即可。

---

## 第 1 步 – 将 MHTML 文件以流的方式打开

首先，我们将归档邮件作为 `InputStream` 打开。使用流可以在处理大型 `.mht` 文件（可能包含嵌入图片或 CSS）时保持低内存占用。

```java
// Step 1: Open the MHTML file as a stream
try (InputStream mhtmlStream = new FileInputStream("YOUR_DIRECTORY/email.mht")) {
    // Subsequent steps go inside this block
}
```

**为什么使用流？**  
流让 `MhtmlDocument` 能够边读取边解析，这意味着即使归档文件有几兆大小，也不会触发 `OutOfMemoryError`。此外，使用流还能让你以后轻松从其他来源读取（例如，从数据库的 `ByteArrayInputStream`）。

---

## 第 2 步 – 从流中加载 MHTML 文档

接下来，将流交给 Aspose 的 `MhtmlDocument` 类。该类会解析 MIME 编码的归档，并构建一个类似 DOM 的内部表示，包含嵌入的 HTML。

```java
// Step 2: Load the MHTML document from the stream
MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);
```

**内部工作原理：**  
Aspose 会提取每个 MIME 部分（HTML、图片、CSS），并在内部重新组装。这就是为什么随后可以仅请求 HTML 部分，而不必担心嵌入资源。

---

## 第 3 步 – 获取主 HTML 内容

文档加载完成后，获取原始 HTML 只需一行代码。`getHtmlContent()` 方法返回正文的 `String`，并保留原始标记。

```java
// Step 3: Retrieve the main HTML content as a string
String htmlContent = mhtmlDoc.getHtmlContent();
```

**返回内容：**  
`htmlContent` 包含完整的 HTML 页面——包括 `<head>` 和 `<body>` 标签——完全与邮件保存时的样子一致。如果只需要可视部分，后续可以使用 Jsoup 解析并去除 `<head>`。

---

## 第 4 步 – 将提取的 HTML 写入独立文件

使用 `java.nio.file` API 将字符串写入磁盘非常直接。此步骤演示了适用于任何平台的 **write string to file** 模式。

```java
// Step 4: Save the extracted HTML to a separate file
Files.writeString(Path.of("YOUR_DIRECTORY/email_body.html"), htmlContent);
```

**小贴士：**  
如果需要特定字符集，可使用 `Files.writeString(Path, CharSequence, Charset)`。默认是 UTF‑8，适用于大多数现代邮件。

---

## 第 5 步 – 确认提取成功

一个简短的 `System.out.println` 可以让你验证程序是否顺利运行且未抛异常。在生产环境中，你可以改为使用正式的日志框架。

```java
// Step 5: Indicate successful extraction
System.out.println("HTML extracted.");
```

运行程序后，控制台应显示 `HTML extracted.`，并且 `email_body.html` 文件会出现在 `YOUR_DIRECTORY` 中。

---

## 完整、可直接运行的示例

将所有步骤整合在一起，以下是完整的、独立的 Java 类。复制粘贴到 IDE 中，点击 **Run** 即可。

```java
import com.aspose.html.MhtmlDocument;
import java.io.FileInputStream;
import java.io.InputStream;
import java.nio.file.Files;
import java.nio.file.Path;

public class MhtmlToHtmlConverter {

    public static void main(String[] args) {
        // Adjust the path to point to your .mht/.mhtml file
        String sourcePath = "YOUR_DIRECTORY/email.mht";
        String targetPath = "YOUR_DIRECTORY/email_body.html";

        // Try-with-resources ensures the stream is closed automatically
        try (InputStream mhtmlStream = new FileInputStream(sourcePath)) {

            // Load the MHTML document
            MhtmlDocument mhtmlDoc = new MhtmlDocument(mhtmlStream);

            // Extract the HTML content
            String htmlContent = mhtmlDoc.getHtmlContent();

            // Write the HTML string to a new file
            Files.writeString(Path.of(targetPath), htmlContent);

            // Simple confirmation output
            System.out.println("HTML extracted to " + targetPath);
        } catch (Exception e) {
            // In real code you might want to log this instead of printing
            System.err.println("Failed to extract HTML: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### 预期输出

运行程序后会打印类似如下内容：

```
HTML extracted to YOUR_DIRECTORY/email_body.html
```

`email_body.html` 将包含原始邮件的完整 HTML 源码。用浏览器打开它，你应当看到与归档邮件相同的视觉渲染（除去未打包的外部资源）。

---

## 常见边缘情况处理

### 1. 缺失的嵌入资源

有时 MHTML 文件会引用未随归档保存的外部图片。此时 `getHtmlContent()` 仍会返回 `<img src="...">` 标记，但 URL 指向原始网络位置。如果需要完全自包含的 HTML 文件，你可以：

- 使用 `MhtmlDocument.save(Path, SaveFormat.HTML)` 让 Aspose 将所有资源提取到一个文件夹中。
- 或者使用 **Jsoup** 等库后处理 HTML，将远程 URL 替换为 base64 编码的 data URI。

### 2. 非 UTF‑8 编码

如果邮件使用了其他字符集（例如 `windows-1252`），返回的字符串可能出现乱码。写入文件时可以强制指定字符集：

```java
Files.writeString(
    Path.of(targetPath),
    htmlContent,
    StandardCharsets.ISO_8859_1
);
```

### 3. 大文件

对于几百兆以上的归档，建议直接将 HTML 输出流式写入 `BufferedWriter`，而不是先将整个字符串加载到内存。Aspose 还提供了直接 **`save`** 到文件的方法，省去中间 `String` 步骤。

---

## 专业技巧与最佳实践

- **复用 `MhtmlDocument` 实例**，如果需要提取多个部分（如 CSS、图片），只需解析一次归档。
- **使用 HTML 验证器**（W3C 验证器或 `jsoup.isValid()`）检查输出的有效性，尤其在将 HTML 交给下游系统时。
- **生产环境使用日志而非打印**。将 `System.out.println` 替换为 SLF4J 等日志框架，以记录时间戳和日志级别。
- **对依赖进行版本控制**。Aspose 更新频繁，在 `pom.xml` 中锁定版本，避免意外的破坏性变更。

---

## 结论

我们已经完整演示了使用 Java **从 MHTML 提取 HTML** 的实用端到端方案。通过流式打开归档、使用 Aspose.HTML 加载、获取 HTML 字符串，再 **将字符串写入文件**，你现在拥有了一种可靠的方式来 **将 MHTML 转换为 HTML**、**提取邮件正文**，以及 **将 MHT 转换为 HTML** 以供后续处理。

欢迎根据实际需求改造代码：如果归档存储在数据库中，可将 `FileInputStream` 替换为 `ByteArrayInputStream`；或者将代码集成到批处理作业中，一次性处理数十封邮件。核心思路不变——让专门的库完成繁重工作，随后自行处理纯文本。

**后续可探索的方向：**

- 使用 Jsoup **清理提取的 HTML**（去除跟踪像素、内联 CSS 等）。
- 通过遍历目录实现 **批量转换** `.mht` 文件。
- 将清理后的 HTML 与 **Apache POI** 结合，嵌入到 Word 或 PDF 文档中。

有关于特定边缘情况的疑问，或想分享你对脚本的扩展？欢迎在下方留言——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}