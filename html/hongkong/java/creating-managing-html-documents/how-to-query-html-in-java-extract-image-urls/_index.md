---
category: general
date: 2026-03-05
description: 如何在 Java 中查詢 HTML，以讀取 HTML 檔案並提取圖片。學習在 Java 中讀取 HTML 檔案、取得圖片網址，以及遍歷 NodeList。
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: zh-hant
og_description: 如何在 Java 中查詢 HTML 並取得圖片 URL。本指南示範如何讀取 HTML 檔案、定位圖片，以及遍歷 NodeList。
og_title: 如何在 Java 中查詢 HTML – 提取圖片網址
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: 如何在 Java 中查詢 HTML – 提取圖片網址
url: /zh-hant/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中查詢 HTML – 取得圖片 URL

有沒有想過在 Java 中 **如何查詢 HTML** 以取得頁面上的每張圖片？你並非唯一有此需求的人——開發者常常需要讀取 HTML 檔案、抓取圖片，然後對取得的 URL 做有用的處理。在本教學中，我們將示範一個實用範例，完整說明 **如何查詢 HTML**、以 Java 方式讀取 HTML 檔案，並以 Java 方式取得圖片 URL。

我們會使用 Aspose.HTML for Java，但概念——XPath、CSS selectors，以及遍歷 `NodeList`——同樣適用於任何 DOM 函式庫。完成本指南後，你將能熟練 **如何提取圖片**、了解 **如何遍歷 NodeList Java**，並擁有一段可直接放入專案的即用程式碼片段。

![在 Java 中查詢 HTML 示例](https://example.com/placeholder.png "在 Java 中查詢 HTML")

---

## 您將學會

- 從磁碟載入 HTML 文件（read HTML file Java）
- 使用 XPath 與 CSS selectors 同時定位 `<img>` 標籤（how to extract images）
- 迭代產生的 `NodeList`（iterate over NodeList Java）
- 輸出每張圖片的 `src` 屬性（get image URLs Java）

不需要外部服務，也不需要複雜的建置工具——只要純 Java 加上一個 Maven 相依即可。

---

## 前置條件

- 已安裝 Java 8 或更新版本
- Maven 或 Gradle 以管理相依
- 具備基本的 HTML 結構認識
- 可選：一個簡單的 HTML 檔案（`sample.html`），內含若干 `<figure><img …></figure>` 元素

只要具備上述條件，就可以直接開始。

---

## 步驟 1：讀取 HTML 檔案 Java – 載入文件

首先，我們必須把 HTML 載入記憶體。Aspose.HTML 的 `HTMLDocument` 類別負責這項重活。可以把它想成打開一本書，讓你隨時翻到任意頁面。

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

**為什麼這很重要：** 載入檔案後會得到可供查詢的 DOM 樹。若路徑錯誤，程式會拋出 `FileNotFoundException`，因此在執行前務必確認檔案位置正確。

---

## 步驟 2：使用 XPath 定位圖片 – 如何提取圖片

XPath 是一種強大的查詢語言，能以雷射般的精準度定位節點。這裡我們要求取得每個 `<figure>` 內且帶有 `alt` 屬性的 `<img>`。

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**為什麼選擇 XPath？** 它語法簡潔，即使 HTML 結構雜亂也能正常運作。`//figure/img[@alt]` 表示「任何位於 `<figure>` 之下且具有 `alt` 屬性的 `<img>`」。若需依其他屬性過濾，只要調整方括號內的條件即可。

---

## 步驟 3：使用 CSS Selector 定位圖片 – 替代的提取圖片方式

有時候你可能較習慣 CSS 語法，因為它與樣式表的寫法相同。`querySelectorAll` 接受的就是瀏覽器中使用的同樣選擇器。

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**為什麼兩者都示範？** 讓你可以依自己最熟悉的工具選擇使用方式。實務上你會固定使用其中一種，但同時提供兩個範例能讓教學更完整。

---

## 步驟 4：遍歷 NodeList Java – 取得圖片 URL Java

現在我們已取得集合，接下來要逐一處理。這正是 **iterate over NodeList Java** 發揮作用的地方。我們會取出每張圖片的 `src` 屬性並印出。

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

**為什麼使用傳統的 `for` 迴圈？** Aspose 的 `NodeList` 並未實作 `Iterable`，因此增強型的 `for‑each` 語法無法編譯。使用索引迴圈是可靠的 **iterate over NodeList Java** 方法。

---

## 預期輸出

將程式對以下範例 HTML 執行：

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

將會產生類似以下的結果：

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

如果你的檔案中符合條件的 `<img>` 標籤更多，輸出的行數也會相應增加。

---

## 常見陷阱與專業提示

- **檔案路徑問題：** 使用絕對路徑或將 `sample.html` 放在專案的工作目錄相對位置。  
- **缺少 `alt` 屬性：** 我們的 XPath/CSS 查詢使用 `[@alt]` 進行過濾。若想抓取 *所有* 圖片，請移除屬性過濾（`//figure/img` 或 `figure img`）。  
- **效能考量：** 處理極大文件時可考慮串流解析器，但對大多數網頁抓取任務而言，DOM 方式已足夠。  
- **編碼問題：** Aspose.HTML 會遵循 HTML 中宣告的字符集。若出現亂碼，請確保檔案以 UTF‑8 儲存。

---

## 擴充範例

既然已能 **取得圖片 URL Java**，接下來你可能想要：

1. 使用 `java.net.URL` 與 `Files.copy` 下載圖片。  
2. 將 URL 存入資料庫以供日後處理。  
3. 依檔案副檔名過濾（`src.endsWith(".png")`）。  

上述皆可在第 4 步的迴圈中輕鬆加入。

---

## 結論

本指南從頭到尾說明了 **如何在 Java 中查詢 HTML**：載入檔案、以 XPath 與 CSS selectors 定位圖片，並 **遍歷 NodeList Java** 以印出每張圖片的 `src`。現在你已掌握 **如何提取圖片**，也清楚 **如何讀取 HTML 檔案 Java**，只要把程式碼套用到自己的需求上，即可開始進行更進階的爬蟲或資料處理。

有任何問題或想分享有趣的使用案例嗎？歡迎在下方留言，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}