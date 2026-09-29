---
category: general
date: 2026-09-29
description: 學習如何按類別選取元素、從檔案讀取 HTML，並在 Java 中找出外部連結。此逐步指南涵蓋高效遍歷 NodeList。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: zh-hant
lastmod: 2026-09-29
og_description: 在 Java 中按類別選取元素，從檔案讀取 HTML，並使用 querySelectorAll 找出外部連結。請參考完整範例以遍歷
  NodeList。
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: 在 Java 中按類別選取元素 – 使用 querySelectorAll 完整指南
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: 如何在 Java 中使用 querySelectorAll 依類別選取元素
url: /zh-hant/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 querySelectorAll 按類別選取元素

如果您需要在 Java 中處理 HTML 檔案時 **按類別選取元素**，本指南將完整說明操作步驟。您將學會從檔案讀取 HTML、使用 `querySelectorAll` 找出外部連結，並安全地遍歷產生的 `NodeList`。

在 Java 中操作 HTML 往往感覺笨重，但現代函式庫提供簡潔、基於 CSS 選擇器的 API。以下範例使用 **jsoup**（版本 1.17.2），因為它實作了 `querySelectorAll` 風格的選擇器，並回傳可類比 `NodeList` 的 `Elements` 集合。若有需要，也可以將相同邏輯套用到其他 DOM 實作上。

## 前置條件

在開始之前，請確保您已具備：

* JDK 17 或更新版本。
* Maven 或 Gradle 以管理相依性。
* 基本的 Java Stream 與 DOM 模型概念。

將 jsoup 加入您的專案：

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## 步驟 1：從檔案讀取 HTML

第一件事是從磁碟載入 HTML 文件。`Jsoup.parse(Path, Charset)` 會讀取檔案並建立可供查詢的 DOM 樹。

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*為什麼這很重要*：只讀取一次檔案即可避免在之後遍歷元素時重複 I/O。`Document` 物件保存完整的 DOM，讓選擇器查詢速度更快。

## 步驟 2：使用 `querySelectorAll` 按類別選取元素

文件已載入記憶體後，您可以使用 CSS 選擇器 **按類別選取元素**。選擇器 `"a.external"` 會匹配帶有 `external` 類別的 `<a>` 標籤——正是您要 **找出外部連結** 的方式。

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*為什麼這很重要*：類別選擇器既表意又效能佳。函式庫會將選擇器轉譯為最佳化的遍歷程式碼，您不必自行寫迴圈遍歷每個節點。

## 步驟 3：在 Java 中遍歷 NodeList（Elements）

`Elements` 實作了 `Iterable<Element>`，因此您可以使用標準的 **for‑each** 迴圈遍歷 **NodeList Java** 物件。以下程式會印出每個連結的 `href` 屬性。

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*為什麼這很重要*：直接迭代讓程式碼易讀，且在只需要簡單輸出時，避免將集合轉成 Stream 所產生的額外開銷。

## 完整範例

將上述三個步驟整合，即可得到一個可直接從命令列執行的自包含程式。

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### 預期輸出

假設 `input.html` 內容如下：

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

執行程式後會印出：

```
External link: https://example.com
External link: https://openai.com
```

## 專業提示與常見陷阱

* **編碼很重要** – 請務必使用 UTF‑8（或與來源相符的字元集）讀取檔案。編碼錯誤會導致屬性值的字元毀損。
* **多重類別** – 若元素同時擁有多個類別（例如 `class="btn external"`），選擇器 `"a.external"` 仍會匹配，因為 CSS 類別選擇器只檢查 token 是否存在，而非完整字串。
* **效能小技巧** – 若只需要 `href` 屬性，可直接使用 `doc.select("a.external[href]").eachAttr("href")` 取得，這樣可避免為每筆匹配建立完整的 `Element` 物件。
* **空值安全** – `link.attr("href")` 若屬性不存在會回傳空字串，因而在列印前不必額外做 null 檢查。

## 常見問答

**Q: 這個方法能處理沒有 `<html>` 根元素的 HTML 片段嗎？**  
A: 能。`Jsoup.parse` 會將輸入視為片段，並自動補上缺失的根元素，使選擇器能在片段的 body 上正常運作。

**Q: 可以不使用 jsoup 而使用 `querySelectorAll` 嗎？**  
A: 標準的 Java DOM API（`org.w3c.dom`）並未提供 `querySelectorAll`。**HTMLUnit** 或 **jodd-lagarto** 等函式庫提供類似方法。此處示範的「載入 → CSS 選擇 → 迭代」模式在其他函式庫中仍然適用。

**Q: 如果我要修改連結而不是僅列印，該怎麼做？**  
A: 取得每個 `Element` 後，可呼叫 `link.attr("href", "newUrl")` 變更屬性，最後使用 `Files.writeString` 將文件寫回磁碟。

## 結論

您現在已掌握如何 **按類別選取元素**、**從檔案讀取 HTML**、**找出外部連結**，以及 **在 Java 中遍歷 NodeList**，全部透過 `querySelectorAll`‑風格的選擇器完成。完整範例展示了乾淨、可投入生產環境的工作流程，您可以將其嵌入更大型的爬蟲或轉換管線中。

接下來，您可以探索以下相關主題，例如 **使用 HTMLUnit 解析動態內容**、**將修改後的 HTML 寫回檔案**，或 **使用 Java Stream 收集連結 URL 成 List**。這些主題皆建立在本指南所示的類別選擇核心技巧之上。祝您寫程式愉快！

## 接下來您可以學習什麼？

以下教學與本指南所示技巧緊密相關，提供完整的程式碼範例與逐步說明，協助您精通更多 API 功能並在專案中嘗試不同實作方式。

- [如何在 Java 中查詢 HTML – 選取元素、依屬性篩選並取得文字](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [遍歷 NodeList Java – 讀取 HTML 並取得 Image src](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [在 Aspose.HTML for Java 中從檔案載入 HTML 文件](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}