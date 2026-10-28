---
category: general
date: 2026-10-28
description: 學習如何透過 Java 解析 HTML，找出外部連結並加入 target="_blank" 以在新分頁開啟連結。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: zh-hant
lastmod: 2026-10-28
og_description: 使用 Java 在新分頁開啟連結：解析 HTML、尋找外部連結、加入 target="_blank"，並儲存修改後的 HTML。
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: 使用 Java 在新分頁開啟連結 – 逐步教學
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: 如何使用 Java 在新分頁中開啟連結
url: /zh-hant/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中於新分頁開啟連結

如果你需要 **在新分頁開啟連結**（來自靜態 HTML 檔案），本指南會一步步說明如何完成。你將學會 **在 Java 中解析 HTML**、**尋找外部連結**、**加入 target="_blank"**，以及 **儲存修改後的 HTML**，全程不必離開 IDE。

在新瀏覽器分頁開啟外部連結可以提升使用者體驗，並讓訪客仍停留在原始頁面。以下解決方案適用於任何 HTML 文件，只需要流行的 jsoup 函式庫，且可在 Java 8 或更新版本上執行。

## 前置條件

開始之前，請確保你已具備：

* 已安裝 JDK 8 以上  
* 具備建置工具（Maven 或 Gradle）以取得 **jsoup** 相依性  
* 含有 `external` 類別的 `<a>` 標籤的 HTML 檔案

不需要 Web 伺服器或其他框架——jsoup 會在本機完成所有工作。

## 步驟 1：在專案中設定 jsoup

將 jsoup 加入相依性。如果使用 Maven，請在 `pom.xml` 中加入：

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

若使用 Gradle，請在 `build.gradle` 加入以下行：

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

上述座標會取得截至 2026 年 10 月的最新穩定版。同步後，即可在 Java 原始檔中匯入 `org.jsoup` 類別。

## 步驟 2：解析 HTML 文件

解析檔案是 **在新分頁開啟連結** 的第一步。`Jsoup.parse` 方法會將檔案讀入可變的類 DOM 結構。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*為什麼這很重要*：`Document` 提供 CSS 風格的選擇器，讓定位所需元素變得輕而易舉。

## 步驟 3：尋找外部連結

現在找出所有帶有 `external` 類別的 `<a>` 元素。這正符合 **find external links** 的需求。

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` 是符合條件的節點集合。如果選擇器回傳空集合，代表你的 HTML 沒有此類別或使用了不同的命名規則——請相應調整選擇器。

## 步驟 4：為每個連結加入 `target="_blank"`

對於 **find external links** 所回傳的每個節點，將 `target` 屬性設為 `_blank`。這即完成 **add target blank** 步驟，確保瀏覽器會在新分頁開啟連結。

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

`attr` 方法會覆寫任何既有的 `target` 值，保證所有外部錨點的行為一致。

## 步驟 5：儲存修改後的 HTML

更新 DOM 後，將變更寫回檔案。這即完成 **save modified html** 的教學部分。

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` 會序列化整個文件，保留 jsoup 原始解析時的縮排與格式。

## 完整可執行範例

將所有步驟組合起來，即成為一個可直接複製、貼上、執行的自包含程式。

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### 預期輸出

假設 `sample.html` 內容如下：

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

執行程式後，`updated.html` 會變成：

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

只有外部連結被加入了 `target="_blank"` 屬性，瀏覽器因此會在新分頁開啟它。

## 專業提示與常見陷阱

* **專業提示**：若需將所有以 `http://` 或 `https://` 開頭的連結視為外部（即使沒有 CSS 類別），可擴充選擇器：`doc.select("a[href^=http]")`。
* **邊緣情況**：部分頁面已指定 `target="_self"`；`attr` 呼叫會覆寫它，確保行為一致。
* **效能**：對於極大型 HTML 檔案，考慮使用串流解析（`Jsoup.parse(File, String, String, Parser.htmlParser())`）以降低記憶體使用。
* **測試**：在瀏覽器開啟 `updated.html`，使用開發者工具檢查連結是否帶有 `target` 屬性，以驗證結果。

## 結論

現在你已擁有一套完整、可執行的 **在新分頁開啟連結** 解決方案，全部使用 Java 與輕量級的 jsoup 函式庫。教學涵蓋了 **parse html in java**、**find external links**、**add target blank**、以及 **save modified html** 四個關鍵步驟。

接下來你可以：

* 擴充選擇器以處理其他連結模式（例如 `rel="external"`）。  
* 結合此邏輯於建置步驟，批次處理專案中的所有 HTML 檔案。  
* 將程式碼整合至更大的內容管理流程中。

歡迎嘗試不同的選擇器或輸出格式，並將你的成果分享給社群！

## 接下來該學什麼？

以下教學與本指南密切相關，能進一步延伸所學技術。每篇資源皆提供完整可執行的程式碼範例與逐步說明，助你掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}