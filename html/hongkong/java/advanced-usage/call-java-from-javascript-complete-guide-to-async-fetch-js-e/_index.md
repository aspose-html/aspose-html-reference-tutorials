---
category: general
date: 2026-03-04
description: 使用 Aspose.HTML 從 JavaScript 呼叫 Java，執行非同步 JavaScript，並在 Java 中抓取 JSON，示範簡單範例。學習高效執行
  JavaScript 引擎。
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: zh-hant
og_description: 使用 Aspose.HTML 從 JavaScript 呼叫 Java，執行非同步 JavaScript，並在 Java 中取得 JSON。完整程式碼、說明與技巧皆已提供。
og_title: 從 JavaScript 呼叫 Java – 逐步非同步 Fetch 教學
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: 從 JavaScript 呼叫 Java – 完整指南：非同步 Fetch 與 JS 引擎執行
url: /zh-hant/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 JavaScript 呼叫 Java – 完整教學與非同步 Fetch API

有沒有想過如何 **在不離開 Java 應用程式的情況下呼叫 Java from JavaScript**？也許你正在建構一個伺服器端的 HTML 渲染器，或是需要將某些 Java 邏輯暴露給文件內執行的腳本。好消息是 Aspose.HTML 讓這件事變得非常簡單。在本指南中，我們不僅會示範如何在 Java 支援的文件中 *執行非同步 JavaScript*，還會說明如何使用現代 **非同步 fetch API** 在 Java 中 **取得 JSON**，最後安全地 **執行 JavaScript 引擎** 呼叫。

簡而言之，你將得到一個完整、可執行的範例，從公開端點取得 JSON 資料，將其交給 Java 主機物件，並在主控台印出結果。無需外部 Web 伺服器、無需額外函式庫——只要純 Java 加上 Aspose.HTML。

## 你將學會

- 如何使用 Aspose.HTML 建立空的 HTML 文件。
- 如何從 Java 取得並 **執行 JavaScript 引擎**。
- 如何註冊一個 Java 主機物件讓 JavaScript 能呼叫回來。
- 如何撰寫使用 **非同步 fetch API** 的 **非同步 JavaScript** 函式。
- 如何在 Java 端以乾淨的回呼處理取得的資料。
- 預期輸出與除錯技巧。

### 前置條件

- Java 17 或更新版本（程式碼在 JDK 11 亦可編譯）。
- Aspose.HTML for Java 23.7（或撰寫時的最新版本）。
- 基本的 Java 與 JavaScript Promise 概念。
- 需要網路連線以執行 `jsonplaceholder` 示範請求。

如果上述任一項你不熟悉，也別擔心——每一步都以淺顯的英文說明，並會說明背後的原因。

---

## 步驟 1 – 建立空的 HTML 文件並取得其 JavaScript 引擎

我們首先需要一個空白文件，提供一個受限的 JavaScript 環境。Aspose.HTML 的 `Document` 類別正好能做到這點。

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**為什麼這很重要：** `Document` 物件模擬瀏覽器視窗，而其 `JavaScriptEngine` 讓我們能像瀏覽器一樣執行腳本。這是 **call java from javascript** 的基礎——引擎即是橋樑。

---

## 步驟 2 – 註冊主機物件讓 JavaScript 能回呼 Java

Aspose.HTML 允許你將任意 Java 物件暴露給腳本世界。我們會建立一個匿名類別，內含單一 `onResult` 方法，負責印出收到的 JSON。

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**說明：**  
- `addHostObject` 將名稱 `javaCallback` 綁定到匿名的 Java 物件。  
- 在 JavaScript 中，我們會呼叫 `javaCallback.onResult(...)`。  
- 這正是 **call java from javascript** 的核心——腳本進入 Java 領域，Java 再回應。

> **小技巧：** 保持主機物件的方法 `public` 且簡潔；過於複雜的物件會導致序列化問題。

---

## 步驟 3 – 使用非同步 Fetch API 撰寫非同步 JavaScript 函式

接下來是有趣的部分：一段從遠端端點取得 JSON 的小腳本。我們會使用 `async/await`，這是 **run async JavaScript** 的現代寫法。

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**為什麼選擇 `fetch` 而非舊式 XHR：**  
- `fetch` 會回傳 `Promise`，讓程式碼更簡潔。  
- 它原生支援 `await`，因此流程自上而下閱讀——非常適合 **asynchronous fetch api** 示範。  
- 此 API 前瞻性佳；大多數瀏覽器與引擎（包括 Aspose 的）皆內建支援。

---

## 步驟 4 – 在文件的 JavaScript 引擎中執行腳本

最後，我們把腳本交給引擎。引擎會啟動一個小型事件迴圈，解析 `fetch` 的 Promise，完成後回呼 Java。

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

執行 `AsyncJsTutorial` 類別時，你應該會看到類似以下的輸出：

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

此輸出證實了三件事：

1. **非同步 fetch API** 成功取得資料。  
2. JSON 已序列化並交給 Java。  
3. 我們的 **execute javascript engine** 呼叫在沒有死結的情況下完成。

---

## 步驟 5 – 錯誤處理與邊緣案例（可選加強）

實務程式碼很少每次都能完美執行。以下列出常見的陷阱與防範方式。

### 5.1 網路失敗

若遠端伺服器宕機，`fetch` 會拋出例外。將呼叫包在 `try/catch` 中：

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

如此一來，Java 端會收到錯誤訊息而不會卡住。

### 5.2 超時

Aspose 的引擎未提供原生的 `fetch` 超時機制，但你可以在 JavaScript 中自行實作：

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 多次呼叫

若需要同時取得多筆資源，只要在 URL 陣列上迴圈或使用 `map` 即可。主機物件可擴充接受識別碼，以便對應回應。

---

## 完整可執行範例

以下是 **完整原始檔**，直接複製貼上到 IDE 即可。沒有隱藏的相依性，只要在 classpath 加入 Aspose.HTML JAR。

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**預期的主控台輸出**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

如果看到以 `Error:` 開頭的行，代表發生錯誤——多半是網路暫時中斷。

---

## 視覺概覽

![Diagram illustrating how Java calls JavaScript and receives async fetch results – call java from javascript](/images/java-js-async.png)

*圖示說明流程：Java → JavaScriptEngine → async fetch → JavaCallback。*

---

## 常見問答

**這個方法能套用在其他 JavaScript 引擎嗎？**  
可以，任何提供主機物件機制的引擎（例如 Nashorn、GraalVM）皆可使用，但 Aspose.HTML 為你提供完整的類瀏覽器環境，且內建 `fetch`。

**如果要回傳複雜的 Java 物件而不是字串該怎麼辦？**  
可以先在 Java 端將物件序列化為 JSON，讓 JavaScript 解析；或是在主機物件上暴露多個方法，分別接收不同欄位。

**`fetch` 的實作是否完全符合標準？**  
Aspose.HTML 依照 WHATWG Fetch 標準實作，支援重新導向、CORS 與串流等功能。

**這會阻塞 Java 執行緒嗎？**  
不會。`execute` 呼叫會立即返回，內部引擎會非同步處理 Promise。但主執行緒會持續存活，直到腳本結束或你手動關閉引擎。

---

## 結論

我們已完整示範如何 **call Java from JavaScript**、**run async JavaScript**，以及使用 **asynchronous fetch API** 在 Java 中 **取得 JSON**。透過建立主機物件、編寫整潔的 `async` 函式，並以 Aspose.HTML 的 **JavaScript engine** 執行，你即可在兩個執行環境之間建立乾淨、非阻塞的橋樑。

快試試看，改變 URL，或加入更多回呼——你的想像力就是唯一的限制。接下來可以探索：

- **Executing JavaScript engine** 同時執行多個腳本。  
- 使用 **run async javascript** 平行處理大量資料。  
- 將此模式整合到即時產生動態 HTML 的 Web 服務中。

歡迎實驗，若遇到意外問題，別忘了留下評論。祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}