---
category: general
date: 2026-04-23
description: 如何在 Java 中使用 querySelectorAll 按类过滤元素、读取属性值，并遍历 NodeList 以提取产品数据。
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: zh
og_description: 如何在 Java 中使用 querySelectorAll 按类筛选元素、读取属性值，并遍历 NodeList 以提取产品数据。
og_title: 如何在 Java 中使用 querySelectorAll – 按类过滤
tags:
- Java
- HTML parsing
- DOM manipulation
title: 如何在 Java 中使用 querySelectorAll – 按类过滤
url: /zh/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 querySelectorAll – 按类过滤

在需要从 HTML 文档中获取特定元素时，如何在 Java 中使用 querySelectorAll 是关键。在本教程中，我们将按类过滤元素，读取属性值，并遍历 NodeList 从目录页面提取产品价格。  

是否曾经盯着一个庞大的 HTML 文件，想要提取仅“on‑sale”卡片而不编写自定义解析器？这正是我们将在此解决的问题——不需要除 Aspose.HTML 之外的额外库，只需几步简单操作。  

您将获得一个完整、可运行的程序，它：

* **选择元素** 使用 CSS 选择器（`select elements css selector`），
* **按类过滤**（`filter elements by class`），
* **读取自定义属性**（`how to read attribute`），
* **遍历得到的 NodeList**（`iterate nodelist java`）。

不需要事先了解 Aspose.HTML——只需基本的 Java 环境和一个用于测试的 HTML 文件。

![如何在 Java 中使用 querySelectorAll 示例](https://example.com/images/queryselectorall-java.png "如何在 Java 中使用 querySelectorAll")

---

## 您需要的条件

| 需求 | 重要原因 |
|------|----------|
| **Java 17+** | 现代语言特性和更好的模块处理。 |
| **Aspose.HTML for Java** (latest version) | 提供 `Document` 类和 CSS‑selector 引擎。 |
| **catalog.html** (sample HTML) | 我们将查询的源文件。 |
| **IDE or plain `javac`** | 用于编译和运行示例。 |

如果您尚未将 Aspose.HTML 添加到项目中，请将 JAR 放入 `libs` 文件夹并添加到类路径：

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## 第一步 – 加载 HTML 文档

在能够查询之前，您需要一个代表 HTML 文件的 `Document` 对象。可以把它想象成在读取单元格之前先加载电子表格。

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **为什么这很重要：** `Document` 类将标记解析为 DOM 树，使 CSS‑selector 引擎能够工作。跳过此步骤将只得到普通字符串，无法使用 `querySelectorAll`。

---

## 第二步 – 使用 CSS 选择器选择元素

现在进入关键部分：**如何使用 querySelectorAll**。该方法接受任何有效的 CSS 选择器，您可以根据需要精确或宽泛地匹配。对于我们的场景，我们想要的产品卡片满足以下条件：

* 包含类 `product-card`，
* 同时具有类 `sale`，
* 并且带有 `data-price` 属性。

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **解释：**  
> * `.product-card.sale` → 过滤同时包含 **两个** 类的元素。  
> * `[data-price]` → 确保属性存在，实际上在一次调用中 **按类和属性过滤元素**。  
> * 结果是一个 `NodeList`，它是有序集合，可供遍历。  

如果您需要为不同模式 **select elements css selector**，只需更改字符串——无需重写代码。

---

## 第三步 – 在 Java 中遍历 NodeList

`NodeList` 的行为类似数组，但它并未实现 `Iterable`。因此我们使用经典的 `for` 循环——非常适合 **iterate nodelist java** 场景。

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **为什么使用 `for` 循环？**  
> 它让您直接访问索引，便于日志记录或条件分支。如果您更喜欢 `while` 循环，逻辑保持不变——只需更改循环结构。

---

## 第四步 – 读取 `data-price` 属性

现在我们终于回答 **how to read attribute** 如何从元素读取属性值。在 DOM API 中，`getAttribute` 返回原始字符串，完全如标记中所示。

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **提示：** 如果属性可能不存在，`getAttribute` 将返回 `null`。您可以使用简单的检查来防护：

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## 第五步 – 输出结果

最后但同样重要的是，我们将每个价格打印到控制台。这对应于实际场景，您可能会将这些值写入数据库或作为 API 负载发送。

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### 预期的控制台输出

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

如果选择器未找到匹配的节点，循环将根本不执行——不会抛出异常。这为目录可能为空的 **edge cases** 提供了良好的安全保障。

---

## 完整工作示例

将所有内容整合在一起，以下是完整文件，可直接复制粘贴到 `CssSelectorDemo.java` 中：

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

保存文件，编译并运行——观察价格流式输出。 🎉

---

## 常见问题与专业提示

| 问题 | 答案 |
|------|------|
| *如果我还需要按标签名选择怎么办？* | 只需在前面加上标签名：`document.querySelectorAll("div.product-card.sale[data-price]")`。 |
| *我可以链式使用多个属性过滤吗？* | 当然可以。例如：`[data-price][data-stock]` 将只保留同时具有 **两个** 属性的元素。 |
| *`querySelectorAll` 是否区分大小写？* | 是的——在 HTML5 中，CSS 选择器对类名和属性名是区分大小写的。 |
| *如何处理巨大的 HTML 文件？* | Aspose.HTML 会对文档进行流式处理，但您也可以将选择器限制在子树上（`someElement.querySelectorAll(...)`）。 |
| *What

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}