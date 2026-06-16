---
category: general
date: 2026-06-16
description: 如何使用 CSS 載入 HTML 檔案並在 Java 中統計連結。學習在單一、清晰的範例中計算 HTML 元素與評估 XPath（Java）。
draft: false
keywords:
- how to use css
- load html file
- how to count links
- count html elements
- evaluate xpath java
language: zh-hant
og_description: 如何在 Java 中使用 CSS 載入 HTML 檔案、統計連結並評估 XPath 表達式——完整實用指南。
og_title: 在 Java 中使用 CSS – 載入 HTML、計算連結與評估 XPath
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  headline: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  type: TechArticle
- description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  name: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  steps:
  - name: What if the HTML file is malformed?
    text: Both the CSS and XPath engines are tolerant of minor markup errors (missing
      closing tags, unquoted attributes). However, severe malformations may cause
      the parser to abort. In production, wrap the loading step in a try‑catch block
      and log the exception.
  - name: Can I combine CSS and XPath in a single expression?
    text: Not directly; each engine has its own syntax. The typical pattern is to
      use the one that expresses the condition most naturally (CSS for structural
      queries, XPath for attribute functions) and then merge the results in Java if
      needed.
  - name: How do I count elements across multiple files?
    text: 'Just place the loading logic inside a loop:'
  - name: Does this work with Java 8?
    text: Yes—provided you use a library version that targets Java 8 or higher. The
      code shown does not rely on newer language features.
  type: HowTo
tags:
- Java
- HTML parsing
- CSS selectors
- XPath
title: 在 Java 中使用 CSS – 載入 HTML、計算連結與評估 XPath
url: /zh-hant/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 CSS – 載入 HTML、計算連結數量與評估 XPath

有沒有想過 **如何在 Java 處理 HTML 檔案時使用 CSS** 選擇器？也許你正在開發網路爬蟲、資料抓取工具，或只是需要檢查靜態網站。好消息是，你不必從頭寫自訂的解析器——現代函式庫讓你可以在同一個整潔的工作流程中，同時混合 CSS4 選擇器與 XPath 3.1 表達式。

在本教學中，我們將示範 **如何載入 HTML 檔案**、使用 CSS 選擇器計算導覽列中的連結數量，接著 **評估 XPath** 以計算符合條件的圖片元素。完成後，你將擁有一個完整、可執行的程式，會在主控台印出符合條件的節點數量，並了解每個步驟的意義。

## 前置條件

- 已在機器上安裝 Java 17（或任何較新的 JDK）  
- 用於相依管理的 Maven 或 Gradle（範例使用 Maven）  
- 一段儲存於 `input.html` 的小型 HTML 片段，放在你可控制的資料夾中  

除此之外不需要其他工具——只要有文字編輯器與終端機即可。

## 本教學涵蓋內容

- **使用 HTMLDocument 類別** 將 HTML 檔案載入為類 DOM 結構  
- 套用 **CSS4 選擇器** (`nav a[data-role]`) 以定位導覽列連結  
- 執行 **XPath 3.1 表達式**，找出 `src` 以 `.png` 結尾且同時具備 `alt` 屬性的 `<img>` 標籤  
- **計算** 兩個查詢的結果並將其印出至主控台  
- 完整原始碼、背後原因說明，以及常見邊緣案例的快速檢視  

讓我們直接開始吧。

---

## 步驟 1 – 使用 HTMLDocument 載入 HTML 檔案

在能夠查詢之前，必須先將 HTML 文件解析成可遍歷的模型。**jsoup‑plus** 函式庫（或任何類似的 HTML‑aware 解析器）提供的 `HTMLDocument` 類別正是為此而設。

```java
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Load the HTML document from the file system
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/input.html");
        // From here on we can query the DOM using CSS or XPath
```

*為什麼這很重要：*  
一次載入檔案並保留參考 (`doc`) 可以避免重複 I/O，這在處理大量頁面時是效能瓶頸的常見來源。

---

## 步驟 2 – 使用 CSS 計算 `<nav>` 內的連結數量

現在文件已在記憶體中，我們可以使用 CSS4 選擇器抓取每一個位於 `<nav>` 內且帶有 `data‑role` 屬性的 `<a>` 元素。這是導覽選單常見的寫法，會利用 data 屬性作為 JavaScript 鉤子。

```java
        // Use a CSS4 selector to find every <a> inside a <nav> that has a data‑role attribute
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");
```

*說明：*  
- `nav a[data-role]` 代表「任何位於 `<nav>` 元素之下，且具備 `data‑role` 屬性的 `<a>` 元素」。  
- 此選擇器相容 **CSS4**，因此若需求擴充，你也可以使用 `:not()`、`:has()` 等偽類。

> **小技巧：** 若只需要直接子層，將空格改成 `>`（`nav > a[data-role]`）即可。這會縮小搜尋範圍，提升大型文件的效能。

---

## 步驟 3 – 在 Java 中評估 XPath 以計算特定 `<img>` 元素

當需要屬性過濾且在 CSS 中不易表達時，XPath 就顯得非常有用。此處我們會找出所有 `src` 以 `.png` 結尾 **且** 同時具備 `alt` 屬性的 `<img>`，這對於無障礙性檢查相當實用。

```java
        // Use an XPath 3.1 expression to locate all <img> elements whose src ends with .png and have an alt attribute
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");
```

*為什麼選擇 XPath？*  
- `ends-with()` 函式屬於 XPath 3.1，允許直接做字尾比對，無需正規表達式。  
- 結合多個謂詞 (`and @alt`) 可確保只計算同時符合來源正確與描述完整的圖片。

如果你的函式庫僅支援 XPath 1.0，則需要改用 `contains(@src, '.png')`，再於 Java 中自行過濾——精確度較低。

---

## 步驟 4 – 計算 HTML 元素並印出結果

最後，我們取得兩個 `NodeList` 物件的長度並輸出。這正是 **如何計算連結** 的核心，但同樣適用於任何節點集合。

```java
        // Output the number of matches for each query
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**預期的主控台輸出**（假設範例 HTML 中有 3 個符合的連結與 2 個符合的圖片）：

```
Nav links: 3
PNG images with alt: 2
```

若計數為 0，請再次檢查選擇器語法或確認 `input.html` 確實包含預期的元素。

---

## 完整範例程式

以下是可直接貼到 `CssXPathDemo.java` 檔案中的完整、獨立程式碼。內含必要的 import、簡易的 `pom.xml` 片段（供 Maven 使用），以及測試用的最小 HTML 範例。

```java
/* CssXPathDemo.java */
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document
        HTMLDocument doc = new HTMLDocument("input.html");

        // Step 2: CSS selector – count navigation links with data-role
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");

        // Step 3: XPath expression – count PNG images that have alt text
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");

        // Step 4: Print the results
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Maven `pom.xml` 片段**（加入此相依即可取得同時支援 CSS4 與 XPath 3.1 的 HTML‑aware 解析器）：

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>html-parser-plus</artifactId>
        <version>2.3.1</version>
    </dependency>
</dependencies>
```

**範例 `input.html`**（請與 Java 檔案放在同一目錄）：

```html
<!DOCTYPE html>
<html lang="en">
<head><title>Test Page</title></head>
<body>
<nav>
    <a href="/home" data-role="main">Home</a>
    <a href="/about" data-role="secondary">About</a>
    <a href="/contact">Contact</a>
</nav>
<img src="logo.png" alt="Company Logo">
<img src="banner.jpg">
<img src="icon.png" alt="Icon">
</body>
</html>
```

執行 `mvn compile exec:java -Dexec.mainClass=CssXPathDemo` 後，即會得到前述的計數結果。

---

## 邊緣案例與常見問題

### HTML 檔案格式不正確怎麼辦？

CSS 與 XPath 引擎對輕微的標記錯誤（缺少閉合標籤、屬性未加引號）相當寬容。但若錯誤過於嚴重，解析器仍可能中止。正式環境建議將載入步驟包在 try‑catch 中，並記錄例外資訊。

### 能否在單一表達式中同時結合 CSS 與 XPath？

無法直接混用；兩者各自擁有獨立語法。常見做法是根據條件自然度選擇使用 CSS（結構查詢）或 XPath（屬性函式），然後在 Java 中合併結果。

### 如何在多個檔案中計算元素？

只要把載入邏輯放入迴圈即可：

```java
for (Path p : Files.newDirectoryStream(Paths.get("html_folder"), "*.html")) {
    HTMLDocument doc = new HTMLDocument(p.toString());
    // repeat the queries...
}
```

### 這段程式能在 Java 8 上執行嗎？

可以，只要使用相容 Java 8 或以上的函式庫版本。範例程式未使用較新語言特性。

---

## 結論

我們示範了 **如何同時使用 CSS 選擇器與 evaluate xpath java** 來 **載入 HTML 檔案**、**計算連結**，以及 **計算符合特定條件的 HTML 元素**。重點如下：

- 以 `HTMLDocument` 只載入一次文件。  
- 使用 CSS4 處理簡單的結構查詢（`nav a[data-role]`）。  
- 利用 XPath 3.1 完成強大的屬性函式（`ends-with(@src, '.png')`）。  
- 透過 `NodeList` 長度取得精確計數。  

接下來，你可以擴充腳本：加入更多選擇器、將結果寫入 CSV，或整合至更大的爬蟲管線。CSS 與 XPath 的組合為幾乎所有 HTML 抓取需求提供了彈性。

準備好實驗了嗎？試著把 CSS 選擇器換成 `section article[data-id]`，或把 XPath 改為針對帶有特定編碼的 `<video>` 標籤。可能性無限。

如果你覺得本指南對你有幫助，歡迎分享、為倉庫加星，或留下你的使用案例評論。祝開發順利！

![如何使用 CSS 範例圖示](https://example.com/diagram.png "如何使用 CSS 範例")

---


## 接下來該學什麼？

以下教學與本篇內容密切相關，能在此基礎上延伸技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並探索在專案中實作的其他方式。

- [如何在 Aspose.HTML for Java 中加入 CSS – 內嵌 CSS 到 HTML 文件](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [如何編輯 CSS – 使用 Aspose.HTML for Java 進行進階外部 CSS 編輯](/html/english/java/editing-html-documents/advanced-external-css-editing/)
- [如何編輯 HTML 文件樹 – Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}