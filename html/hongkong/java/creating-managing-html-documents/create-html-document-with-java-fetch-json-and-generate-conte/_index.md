---
category: general
date: 2026-02-11
description: 使用 Aspose.HTML 在 Java 中建立 HTML 文件。了解如何取得 JSON JavaScript、加入 script 元素、從
  JSON 產生 HTML 以及將 JSON 轉換為 pre。
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: zh-hant
og_description: 使用 Aspose.HTML 在 Java 中建立 HTML 文件。取得 JSON JavaScript，加入 script 元素，從
  JSON 產生 HTML，並將 JSON 轉換為 pre——一次搞掂的完整教學。
og_title: 在 Java 中建立 HTML 文件 – 完整指南
tags:
- Aspose.HTML
- Java
- Web Automation
title: 使用 Java 建立 HTML 文件 – 擷取 JSON 並產生內容
url: /zh-hant/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 HTML 文件 – 完整 Java 教學

有沒有曾經需要即時 **create HTML document**，但不確定如何將遠端資料拉入其中？你並不孤單。在許多專案中，你會想使用 JavaScript 取得 JSON，將結果注入頁面，然後將最終的標記儲存為靜態檔案。本指南將會示範如何使用 Aspose.HTML for Java 完成此流程。

我們將逐步說明每個步驟：從實例化空白文件、到 **fetch JSON JavaScript**、再到 **add script element**，最後到 **generate HTML from JSON** 與 **convert JSON to pre** 標籤。完成後，你將擁有一個可直接使用的 `fetchResult.html`，其中包含已渲染為美化 JSON 的資料。

## 先決條件

- Java 17 或更新版本（程式碼同樣可在 JDK 11+ 編譯）
- Aspose.HTML for Java 函式庫（可於 Maven Central 取得）
- 具備 HTML 與非同步 JavaScript 的基本知識
- 任一 IDE 或純粹使用 `javac`/`java` 指令列

不需要額外的框架——所有操作皆在本機執行。

## 第一步：設定專案並匯入 Aspose.HTML

首先，將 Aspose.HTML 相依性加入你的 `pom.xml`（或手動下載 JAR）。

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **專業提示：** 請保持版本號為最新；較新的發行版會修正錯誤並提升腳本引擎。

## 第二步：**Create HTML Document** – 空白畫布

我們先建立一個空的 `HTMLDocument`。可以將它視為一張全新的頁面，之後會在上面放入腳本。

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

為什麼需要文件物件？Aspose.HTML 的 `ScriptEngine` 針對 DOM 而非純文字字串執行。透過建立正確的文件，我們為引擎提供真實的執行環境，以執行我們的 **fetch JSON JavaScript**。

## 第三步：撰寫 JavaScript 片段 – **Fetch JSON JavaScript** 與 **Convert JSON to pre**

本教學的核心在於這段多行字串。它會執行非同步的 `fetch`，解析 JSON，然後寫入一個包含美化資料的 `<pre>` 元素。

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

請注意註解 *Convert JSON to <pre>* —— 這正是 `JSON.stringify(..., null, 2)` 所做的事。它會加入縮排，使輸出易於閱讀。

## 第四步：**Add Script Element** 至文件

現在我們建立一個 `<script>` 標籤，將程式碼放入其中，並附加到 body。這就是 **add script element** 的步驟。

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

為什麼要附加到 body？在真實的瀏覽器中，腳本會在解析後立即執行。將它加入 DOM 後，我們模擬相同的行為，確保非同步的 fetch 在稍後呼叫引擎時執行。

## 第五步：執行 Script Engine – 讓非同步 Fetch 完成

Aspose.HTML 提供 `ScriptEngine` 以執行基於 DOM 的 JavaScript。我們呼叫 `run()`，並等待 Promise 鏈完成。

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

引擎會阻塞，直至所有未完成的任務（我們的 fetch）解決，確保產生的 HTML 已包含資料。

## 第六步：**Generate HTML from JSON** – 儲存結果

最後，我們將文件寫入磁碟。檔案現在包含了帶有 JSON 資料的 `<pre>` 區塊。

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

執行程式後會產生 `fetchResult.html`。在任意瀏覽器開啟，即可看到類似以下的內容：

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

這就是你想要的 **generate HTML from JSON** 結果。

## 完整範例程式

以下為完整、可直接執行的來源檔案。複製、貼上、調整輸出路徑，然後執行 `java JsFetchExample`。

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## 預期輸出與驗證

1. **Console:** 你會看到 `HTML with fetched data saved.`  
2. **File (`fetchResult.html`):** 開啟後會在 `<pre>` 區塊中顯示 JSON，且已妥善縮排。  
3. **Validation:** 若檢視頁面原始碼，僅會看到 `<pre>` 元素——不會有額外的 script 標籤，因為引擎已執行它們。

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| *如果 API 回傳錯誤怎麼辦？* | 將 `fetch` 呼叫包在 `try…catch` 區塊中，並將錯誤訊息寫入 body，而非 JSON。 |
| *我可以同時取得多個資源嗎？* | 可以——只要串接額外的 `await fetch(...)` 呼叫或使用 `Promise.all`。最終的 `innerHTML` 可以串接多個 `<pre>` 區塊。 |
| *需要設定 CORS 標頭嗎？* | 由於腳本在 Aspose.HTML 的沙盒中執行，它遵守同源政策。公共的 JSONPlaceholder 端點已允許跨來源請求。 |
| *如何在執行時變更輸出目錄？* | 將路徑作為指令列參數傳入（`args[0]`），並在 `htmlDoc.save` 中取代硬編碼的字串。 |
| *有沒有辦法嵌入 CSS 進行樣式設定？* | 當然可以。建立一個 `<style>` 元素，將 `textContent` 設為你的 CSS，並在執行引擎前將其附加到 `<head>`。 |

## 生產環境使用技巧

- **Cache the JSON** 如果端點回應緩慢；你可以將取得的字串寫入檔案並重複使用。
- **Sanitize the data** 在注入前先清理資料，特別是來源不可信時。安全使用 `JSON.stringify` 或轉義 HTML 實體。
- **Configure the ScriptEngine timeout** (`scriptEngine.setTimeout(5000)`) 以避免在服務無回應時卡住。

## 視覺摘要

![create html document 範例 – 顯示生成的 HTML，內含 JSON 的 <pre> 標籤](fetchResult.png "生成的 HTML 文件截圖")

*Alt text:* *create html document 範例 – 生成的 HTML 檔案顯示在 <pre> 元素內的取得 JSON。*

## 結論

現在你已了解如何在 Java 中以程式方式 **create HTML document**，以及 **fetch JSON JavaScript**、**add script element**、**generate HTML from JSON**，並 **convert JSON to pre** 以產生可讀的輸出。整個工作流程離線執行，只需 Aspose.HTML，即可產生可在任何地方提供的乾淨靜態檔案。

接下來，試著擴充腳本以迭代物件陣列、加入 CSS 樣式，或使用相同技巧產生多頁。你也可以將 `fetch` URL 換成自己的 API，將動態資料轉為靜態快照——非常適合 SEO 友好的預先渲染。

祝程式開發順利，歡迎在留言中分享你的實驗！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}