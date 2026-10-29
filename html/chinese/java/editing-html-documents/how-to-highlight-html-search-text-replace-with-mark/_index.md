---
category: general
date: 2026-03-04
description: 如何通过在 HTML 中搜索文本并用 <mark> 标签包裹每个匹配项来实现高亮显示。一步步的 Java 指南，教你将文本替换为 mark
  元素。
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: zh
og_description: 如何通过在 HTML 中搜索文本并用 <mark> 标签包裹匹配项来高亮显示 HTML。完整的 Java 示例用于将文本替换为 mark。
og_title: 如何在HTML中高亮显示——搜索文本并用<mark>替换
tags:
- Aspose.HTML
- Java
- Text Processing
title: 如何在HTML中高亮显示——搜索文本并替换为<mark>
url: /zh/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 HTML 中高亮显示 – 搜索文本并用 `<mark>` 替换

是否曾经想过 **如何在 HTML 中高亮显示** 当某个词出现多次时？也许你正在构建文档站点、博客引擎，或仅仅需要在静态页面中强调品牌名称。好消息是？只要了解如何在 HTML 中搜索文本并用 `<mark>` 元素包裹结果，这其实相当简单。

在本教程中，我们将逐步演示一个完整的 Java 解决方案：加载 HTML 文件，搜索目标词，将每个出现位置替换为 `<mark>` 标签，最后保存高亮后的版本。完成后，你将能够 **highlight word in HTML**、**highlight occurrences of word**，甚至 **replace text with mark**，而不会破坏周围的标记。

> **你需要的**  
> • Java 17 或更高（代码在更早的版本也能工作）  
> • Aspose.HTML for Java 库（免费试用或授权副本）  
> • 你想要处理的简单 HTML 文件  

如果你已经准备好这些基础，让我们开始吧。  

![显示高亮 HTML 输出的截图 – how to highlight html](/images/highlight-html-example.png "how to highlight html 示例")

## 第一步 – 加载 HTML 文档（How to Highlight HTML）

首先我们需要将源文件加载到内存中。Aspose.HTML 的 `Document` 类完成所有繁重的工作，将标记解析为类似 DOM 的结构，供我们查询。

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**为什么这很重要：** 加载文档为我们提供了干净的对象模型，这样我们就可以安全地操作文本节点，而不必担心破坏标签或属性。它还会规范化空白，使后续的 **search text in html** 步骤更可靠。

## 第二步 – 在 HTML 中搜索目标词

现在文档已准备好，我们将查找所有需要强调的词的出现位置。`searchText` 方法返回一个 `TextMatch` 对象列表，每个对象描述匹配在 DOM 中的位置。

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**小贴士：** 默认情况下搜索是区分大小写的。如果需要不区分大小写的搜索，在调用 `searchText` 之前将文档文本和 `searchTerm` 都转换为相同的大小写，或使用库提供的基于正则表达式的方法。

## 第三步 – 用 `<mark>` 替换文本（Highlight Word in HTML）

对于每个匹配，我们将重建包含节点的文本，在确切的词周围插入 `<mark>` 元素。这确保我们只影响目标文本，而不触及其余的 HTML。

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**解释：**  
- `getStartOffset`/`getEndOffset` 为我们提供匹配在其父节点内部的精确字符位置。  
- 通过切分原始文本（`textBefore` 和 `textAfter`），我们保持其他内容不变。  
- 用 `<mark>` 包裹匹配是 **replace text with mark** 的标准做法，可获得原生浏览器高亮而无需额外 CSS。

### 边缘情况与技巧

- **同一节点中的多个匹配：** 循环顺序处理每个 `TextMatch`。由于每次我们都会替换整个节点的内容，后续的偏移会发生变化。Aspose.HTML 按文档顺序返回匹配，因此简单的替换在大多数情况下有效。如果遇到重叠匹配，考虑先收集所有匹配，然后一次性重建节点。  
- **不能包含原始 HTML 的元素：** 如果父节点是 `<script>` 或 `<style>` 块，插入 `<mark>` 会破坏页面。可以在替换前检查 `parentNode.getNodeName()` 来跳过这些节点。

## 第四步 – 保存高亮文档（Highlight Occurrences of Word）

在完成所有替换后，我们将修改后的 DOM 持久化回磁盘。输出文件将包含原始标记以及新的 `<mark>` 标签，从而有效地 **highlighting occurrences of word** “Aspose”。

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

在任意浏览器中打开 `highlighted.html`，你会看到每个 “Aspose” 都被黄色背景（`<mark>` 的默认样式）包裹。如果你想要自定义外观，可以添加一条小的 CSS 规则：

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## 常见问题（Search Text in HTML – FAQs）

**问：如果词出现在属性值内部怎么办？**  
**答：** `searchText` 只检查节点的文本内容，不会搜索属性字符串。要高亮属性值，需要遍历元素并手动检查属性。

**问：我能一次性高亮多个不同的词吗？**  
**答：** 当然可以。构建一个词列表，逐个循环，并运行相同的替换逻辑。只需注意避免匹配重叠。

**问：这能在仅有 HTML5 标签（如 `<section>` 或 `<article>`）的页面上工作吗？**  
**答：** 可以。Aspose.HTML 完全支持现代 HTML5 元素，因此 DOM 遍历不受标签类型限制。

## 完整工作示例（所有步骤合并）

下面是完整的、可直接运行的 Java 程序，演示整个工作流——从加载文件到保存高亮输出。

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**预期输出：** 打开 `highlighted.html`，你会看到每个 “Aspose” 都被高亮。页面的其他部分未被更改，文件仍然是有效的 HTML 文档。

## 结论

我们已经介绍了通过编程方式 **how to highlight HTML**，即 **searching text in HTML**，将每个匹配用 `<mark>` 标签包裹，并最终持久化更改。此方法让你能够 **highlight word in HTML**、**highlight occurrences of word**，以及 **replace text with mark**，而无需编写脆弱的字符串操作代码。

接下来可以尝试扩展脚本：

- 将搜索词作为命令行参数接受。  
- 生成定义自定义高亮颜色的 CSS 文件。  
- 一次性批量处理整个文件夹的 HTML 文件。  

这些变体将加深你对 Aspose.HTML API 以及通用文本处理模式的理解。

如果你遇到任何问题或有进一步改进的想法，请在下方留言。祝你高亮愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}