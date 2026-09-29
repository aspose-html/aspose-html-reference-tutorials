---
category: general
date: 2026-09-29
description: 使用 Java 在 HTML 檔案中以 JavaScript 更改背景顏色。學習如何在 Java 中載入 HTML、在 HTML 中執行
  JS，並透過 Java 修改 HTML 以設定新頁面的背景。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: zh-hant
lastmod: 2026-09-29
og_description: 使用 Java 在 HTML 頁面中變更背景顏色（JavaScript）。本教學示範如何在 Java 中載入 HTML、在 HTML
  中執行 JavaScript，並以程式方式設定頁面背景。
og_image_alt: Screenshot of Java code that changes the page background color
og_title: 使用 Java 透過 JavaScript 更改背景顏色 – 一步一步教學
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
title: 如何使用 Java 透過 JavaScript 更改背景顏色
url: /zh-hant/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Java 更改背景顏色（javascript）

如果您需要在現有的 HTML 檔案中 **更改背景顏色（javascript）**，可以完全在 Java 中完成，無需開啟瀏覽器。本教學將示範如何 **在 Java 中載入 html**、執行一小段 JavaScript 程式碼，然後 **使用 java 修改 html**，使頁面的背景顏色得以更新。

此解決方案使用開源的 **HTMLUnit** 函式庫，提供一個無頭瀏覽器，能夠像真實瀏覽器一樣評估 JavaScript。完成本指南後，您將擁有一個可重複使用的方法，**設定頁面背景** 為任意您想要的顏色。

## 前置條件

| 您需要的項目 | 為什麼重要 |
|---------------|------------|
| Java 8 或更新版本 | HTMLUnit 至少需要 Java 8。 |
| Maven 或 Gradle 建置工具 | 讓您自動下載 HTMLUnit 相依套件。 |
| 您想要編輯的 HTML 檔案（例如 `input.html`） | 需要載入並修改的來源文件。 |

將 HTMLUnit 加入您的專案：

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

> **小技巧：** 使用最新的穩定版 HTMLUnit，以取得最精確的 JavaScript 引擎。

## 更改背景顏色（javascript） – 在 Java 中載入 HTML

第一步是將 HTML 文件載入到 `HTMLPage` 物件中。這樣您就能取得類似 DOM 的 API 以及 JavaScript 執行環境。

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

*為什麼重要*：`WebClient` 會建立一個沙盒環境，讓 JavaScript 能夠執行，您可以 **在 html 中執行 js**，效果與使用者的瀏覽器相同。

## 在 html 中執行 js 以設定頁面背景

頁面載入後，您可以評估任意 JavaScript 表達式。以下程式碼會變更 `<body>` 元素的 `backgroundColor` 樣式。

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

*說明*：  
- `document.body.style.backgroundColor` 是頁面背景的標準 DOM 屬性。  
- 透過呼叫 `eval`，我們 **在 html 中執行 js**，不需要真實的瀏覽器視窗。  
- 此方法可重複使用於任何顏色，滿足 **設定頁面背景** 的需求。

## 使用 java 修改 html 並儲存結果

腳本執行完畢後，DOM 已反映新的樣式。現在可以將更新後的 HTML 寫回磁碟。

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

把所有步驟整合起來，即可得到一個可直接執行的程式：

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

### 預期輸出

執行程式後會印出：

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

在任何瀏覽器開啟 `js_modified.html`，即可看到頁面呈現淡藍色背景，證明 **更改背景顏色（javascript）** 的操作已成功。

## 常見變化與例外情況

| 情況 | 處理方式 |
|------|----------|
| **不同的顏色格式** | 傳入任何 CSS 相容的值（`"red"`、`"#ff0000"`、`"rgb(255,0,0)"`）。 |
| **缺少 `<body>` 標籤** | 程式會靜默失敗；您可以先使用 `page.getFirstByXPath("//body")` 確認 `<body>` 是否存在。 |
| **大型 HTML 檔案** | 關閉 CSS（`setCssEnabled(false)`）並僅啟用所需的 JavaScript 功能，以降低記憶體使用量。 |
| **執行多段腳本** | 重複呼叫 `changeBackground`，或建立接受 JavaScript 命令清單的工具方法。 |

## 結論

現在您已了解如何透過在 Java 中載入 HTML、**在 html 中執行 js**，以及 **使用 java 修改 html**，來 **設定頁面背景** 為任意顏色。上述完整範例使用最新的 HTMLUnit 函式庫，且可整合至更大的自動化流程，例如批次處理 HTML 報告或製作電子郵件範本。

**後續步驟**  
- 探索其他 DOM 操作（例如插入元素、移除腳本）。  
- 結合此方法與 PDF 產生器，將已樣式化的頁面匯出為 PDF。  
- 若需要完整的瀏覽器相容性，可改用 Selenium WebDriver 等其他無頭引擎。

祝開發順利！


## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化您所學的技巧。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [Get Computed Style Java – Extract Background Color from HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Generate HTML from JavaScript in Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}