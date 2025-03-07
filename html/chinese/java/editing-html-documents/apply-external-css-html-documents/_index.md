---
title: 在 Aspose.HTML for Java 中将外部 CSS 应用于 HTML 文档
linktitle: 在 Aspose.HTML for Java 中将外部 CSS 应用于 HTML 文档
second_title: 使用 Aspose.HTML 进行 Java HTML 处理
description: 了解如何使用 Aspose.HTML for Java 将外部 CSS 应用于 HTML 文档！按照本分步指南获取完整教程。
weight: 12
url: /zh/java/editing-html-documents/apply-external-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.HTML for Java 中将外部 CSS 应用于 HTML 文档

## 介绍
处理 HTML 文档时，应用样式会对演示和用户体验产生重大影响。如果您正在深入研究 Java，并想学习如何使用 Aspose.HTML 库将外部 CSS 样式应用于 HTML 文档，那么您来对地方了！本指南旨在逐步说明该过程，即使是 Java 或 CSS 新手也可以轻松掌握。
## 先决条件
在深入研究代码之前，您需要做好以下几件事：
### 1.Java 开发工具包（JDK）
确保你的机器上安装了 JDK。你可以从以下网址下载最新版本[Oracle 的 Java 网站](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Java 版 Aspose.HTML
您需要设置 Aspose.HTML for Java。如果您尚未完成此操作，请前往[Aspose 下载页面](https://releases.aspose.com/html/java/)并抓住图书馆。
### 3. IDE 或文本编辑器
选择一个集成开发环境（IDE）如 IntelliJ IDEA、Eclipse 或甚至一个简单的文本编辑器来编写 Java 代码。
### 4. Java基础知识
熟悉 Java 编程和 CSS 基础知识肯定能帮助您更轻松地跟进。
## 导入包
一切设置完成后，下一步就是在 Java 项目中导入必要的包。以下是您需要的内容：
```java
import com.aspose.html.HTMLDocument;
```
这些导入将允许您操作 HTML 文档并将其呈现为不同的格式，例如 PDF。

我们将把本教程分解为易于管理的步骤。每个步骤都将指导您使用 Aspose.HTML for Java 将外部 CSS 样式应用于 HTML 文档的过程。
## 步骤 1：创建 HTML 文档
首先，我们需要创建 HTML 文档。首先，我们用简单的 HTML 结构定义内容。
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

在这里，我们定义了一个基本的 HTML 结构，包括一个`<div>`两段文字。`HTMLDocument`类用于创建我们的 HTML 内容的文档表示。
## 第 2 步：创建样式元素
接下来我们将创建一个`style`元素来保存我们的 CSS 规则。
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

使用`createElement`方法`HTMLDocument`，我们创建一个新的`<style>`元素并设置其内容以包含两个类的 CSS 定义：`frame1`和`frame2`。这些类定义边距、填充、尺寸、背景颜色、字体系列和文本颜色。
## 步骤 3：将样式附加到文档页眉
现在我们已经有了 CSS，我们需要将样式元素附加到文档的头部。
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

我们检索文档的头部并附加我们新创建的`style`元素。此操作有效地将我们的 CSS 集成到 HTML 文档中，从而允许其为我们的 HTML 内容设置样式。
## 步骤 4：将类应用于 HTML 元素
接下来，我们将之前定义的 CSS 类应用到段落元素。
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

在这里，我们访问文档中的第一个和最后一个段落元素，并为它们分配我们创建的 CSS 类。此分配可确保它们遵循我们在 CSS 中定义的样式。
## 步骤 5：设置其他样式属性
为了进一步增强外观，我们将为段落设置额外的样式属性。
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

在此步骤中，我们将微调样式。第一段的字体大小增加并居中，而最后一段的颜色、字体大小和字体系列则已定义。这种改进对于可读性和美观性至关重要。
## 步骤 6：保存 HTML 文档
一旦应用了样式，就该保存 HTML 文档了。
```java
document.save("edit-internal-css.html");
```

在这里，我们利用`save`方法`HTMLDocument`类将修改后的 HTML 内容写入文件，从而保留我们的样式和更改。
## 步骤 7：将文档渲染为 PDF
最后，我们将文档渲染为 PDF 格式以供输出。
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

使用`PdfDevice`类中，我们设置了将 HTML 文档渲染为 PDF。当您想要以通用格式共享样式化文档时，此步骤至关重要。
## 结论
就是这样 — 使用 Aspose.HTML for Java 将外部 CSS 应用于 HTML 文档既简单又有益！只需几行代码，您就可以将纯文本转换为具有视觉吸引力和专业风格的文档。因此，无论您是为个人用途进行设计、创建报告还是开发 Web 内容，了解如何在 Java 中操作 HTML 和 CSS 都是您工具包中必备的一项强大技能。
## 常见问题解答
### 什么是 Aspose.HTML for Java？
Aspose.HTML for Java 是一个功能强大的库，允许开发人员在 Java 应用程序中处理 HTML 文档，提供从 HTML 操作到渲染的广泛功能。
### 我需要互联网连接才能使用 Aspose.HTML 吗？
不，一旦您下载了必要的库文件，您就可以离线使用 Aspose.HTML。
### 我可以将多个 CSS 文件应用于 HTML 文档吗？
是的，你可以创建多个`<link>`元素并将它们附加到各种 CSS 文件的文档头部。
### 内部 CSS 和外部 CSS 有区别吗？
是的！内部 CSS 在 HTML 文档中定义，而外部 CSS 则放在单独的文件中并链接到文档。
### 如何获得 Aspose.HTML for Java 的支持？
您可以通过以下方式获取社区支持[Aspose 论坛](https://forum.aspose.com/c/html/29)对于您可能遇到的任何问题或疑问。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
