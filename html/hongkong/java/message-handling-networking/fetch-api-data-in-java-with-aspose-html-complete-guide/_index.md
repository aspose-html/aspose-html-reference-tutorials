---
category: general
date: 2026-05-28
description: 在 Java 中使用 Aspose.HTML 取得 API 資料 ─ 學習如何執行非同步 JavaScript、執行非同步腳本，以及從取得的
  JSON 設定 DOM 屬性。
draft: false
keywords:
- fetch api data
- execute async javascript
- run async script
- set dom attribute
- how to run async
language: zh-hant
og_description: 在 Java 中使用 Aspose.HTML 獲取 API 數據。本教程展示如何執行非同步 JavaScript、運行非同步腳本，以及從
  API 結果設置 DOM 屬性。
og_title: 在 Java 中抓取 API 資料 – Aspose.HTML 一步一步指南
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  headline: fetch api data in Java with Aspose.HTML - Complete Guide
  type: TechArticle
- description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  name: fetch api data in Java with Aspose.HTML - Complete Guide
  steps:
  - name: Expected Output
    text: '``` GitHub stars: 84327 ```'
  - name: What if the fetch call fails?
    text: 'The script will throw a JavaScript exception, which propagates to `ScriptEngine.evaluate`.
      You can catch it in Java:'
  - name: Can I fetch from a private API that requires authentication?
    text: 'Sure—just add the appropriate headers in the script:'
  - name: Does this work on older Java versions?
    text: Aspose.HTML ships with its own JavaScript engine, so you don’t need Nashorn
      or GraalVM. However, the `try‑with‑resources` syntax requires Java 7+. For Java
      6 you’d have to close the document manually.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Async JavaScript
title: 在 Java 中使用 Aspose.HTML 抓取 API 資料 - 完整指南
url: /zh-hant/java/message-handling-networking/fetch-api-data-in-java-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中使用 Aspose.HTML **fetch api data** – 完整指南

有沒有想過在不離開 IDE 的情況下 **fetch api data**？你並不孤單。許多開發者在需要從 Aspose.HTML 渲染的 HTML 頁面呼叫遠端服務，並將結果帶回 Java 時，常會卡關。

在本教學中，我們將示範一個實作範例，說明如何 **執行 async javascript**、執行 **async script**，最後 **設定 DOM 屬性** 為取得的值。完成後，你將清楚知道 *如何安全執行 async* 操作並取得所需資料。

## 你將會建立什麼

我們會建立一個小型的 Java 主控台應用程式，功能如下：

1. 載入包含 async 函式的 HTML 檔案。  
2. 執行一段使用 **fetch API** 呼叫 GitHub 公開端點的腳本。  
3. 等待 Promise 完成（最長 10 秒）。  
4. 將星星數量存入 `<body>` 元素的自訂 `data-stars` 屬性。  
5. 從 Java 讀取該屬性並印出。

不需要額外的 HTTP 客戶端函式庫，也不需要自行管理執行緒——全部交給 Aspose.HTML 處理。

## 前置條件

- **Java 17** 或更新版本（程式碼在較舊版本亦可編譯，但 17 為目前的 LTS）。  
- **Aspose.HTML for Java** 套件（版本 23.9 以上）。  
- 一個簡易的 HTML 檔案（`async-page.html`），放在磁碟任意位置。  
- 網際網路連線（fetch 會呼叫 `https://api.github.com`）。

如果你已有 Maven 專案，請加入 Aspose.HTML 的相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

現在，讓我們深入程式碼。

## 步驟 1：準備 HTML 頁面

首先，建立一個最小的 HTML 檔案，作為 async 函式的容器。只需要 `<body>` 標籤即可，無需其他複雜標記。

```html
<!-- async-page.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Async Demo</title>
</head>
<body>
    <!-- The script we’ll inject later will populate this attribute -->
</body>
</html>
```

將此檔案儲存於可存取的位置，例如 `C:/temp/async-page.html`。路徑會在 Java 程式中使用。

![fetch api data example](https://example.com/fetch-api-data.png "fetch api data example")

*圖片說明：fetch api data example，顯示 GitHub 星星數的主控台輸出。*

## 步驟 2：在 Java 中載入 HTML 文件

HTML 檔案備妥後，我們使用 Aspose.HTML 的 `HTMLDocument` 來開啟它。`try‑with‑resources` 區塊可確保文件正確釋放。

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {
            // The rest of the steps go here...
        }
    }
}
```

為什麼要使用 `HTMLDocument`？它提供完整的 DOM、內建的 JavaScript 引擎，以及從 Java 與頁面互動的便利方式，且不需啟動瀏覽器。

## 步驟 3：撰寫 Async Script

接下來，我們編寫一段 JavaScript 程式碼，**fetch API 資料**、等待 Promise，最後 **設定 DOM 屬性**。使用 `async/await`，與在瀏覽器中寫法相同。

```java
String script =
    "async function run() {" +
    "  const data = await fetch('https://api.github.com').then(r => r.json());" +
    "  document.body.setAttribute('data-stars', data.stargazers_count);" +
    "}" +
    "run();";
```

重點說明：

- `run` 函式被宣告為 `async`，因此可以 `await` `fetch` 呼叫。  
- 解析 JSON 後，我們把 `data.stargazers_count` 存入自訂屬性 `data-stars`。  
- 最後立即呼叫 `run()`。

這段小腳本即完成 **run async script** 並取得結果的所有工作。

## 步驟 4：執行腳本並等待

Aspose.HTML 的 `ScriptEngine` 能以逾時方式評估 JavaScript。傳入 `10000` 表示引擎最多等待 **10 秒** 讓 async 操作完成。

```java
// Execute the script and wait (up to 10 seconds) for the async operation to finish
ScriptEngine engine = doc.getScriptEngine();
engine.evaluate(script, 10000);   // timeout in milliseconds
```

若請求超過逾時時間，會拋出 `ScriptException`——非常適合處理不穩定的網路情況。實務上，你可能會將其包在 `try‑catch` 中，並視需要重試。

## 步驟 5：從 Java 取得屬性

腳本執行完畢後，`data-stars` 屬性已成為 DOM 的一部份。只要簡單呼叫即可把它拉回 Java：

```java
// Retrieve the value set by the script from the document
String stars = doc.getBody().getAttribute("data-stars");
System.out.println("GitHub stars: " + stars);
```

此行會印出類似 `GitHub stars: 12345` 的訊息。具體數字每日變動，但格式保持不變。

## 完整範例

將上述所有片段組合起來，即得到可直接執行的完整程式：

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {

            // Step 2: Define a script that calls the async function and stores the result in a DOM attribute
            String script =
                "async function run() {" +
                "  const data = await fetch('https://api.github.com').then(r => r.json());" +
                "  document.body.setAttribute('data-stars', data.stargazers_count);" +
                "}" +
                "run();";

            // Step 3: Execute the script and wait (up to 10 seconds) for the async operation to finish
            ScriptEngine engine = doc.getScriptEngine();
            engine.evaluate(script, 10000);

            // Step 4: Retrieve the value set by the script from the document
            String stars = doc.getBody().getAttribute("data-stars");
            System.out.println("GitHub stars: " + stars);
        }
    }
}
```

### 預期輸出

```
GitHub stars: 84327
```

（你的數字會不同；重點是輸出的是一個 **字串**，代表星星數量。）

## 常見問題與邊緣情況

### 若 fetch 呼叫失敗怎麼辦？

腳本會拋出 JavaScript 例外，會傳遞至 `ScriptEngine.evaluate`。你可以在 Java 中捕捉：

```java
try {
    engine.evaluate(script, 10000);
} catch (ScriptException e) {
    System.err.println("Failed to fetch data: " + e.getMessage());
}
```

### 能否從需要驗證的私有 API 取得資料？

可以，只要在腳本中加入相應的標頭：

```javascript
await fetch('https://api.example.com/secure', {
    headers: { 'Authorization': 'Bearer YOUR_TOKEN' }
}).then(r => r.json());
```

記得將機密資訊排除於原始碼管理。

### 這能在較舊的 Java 版本上執行嗎？

Aspose.HTML 內建自己的 JavaScript 引擎，無需 Nashorn 或 GraalVM。但 `try‑with‑resources` 語法需要 Java 7 以上。若使用 Java 6，需手動關閉文件。

## 專業小技巧

- **重複使用 ScriptEngine**：若需要執行多個 async 腳本，保留單一引擎實例可減少開銷。  
- **延長逾時時間** 以因應較慢的 API，但不要設為 `Integer.MAX_VALUE`，仍需安全網。  
- **驗證屬性值** 再使用。若腳本未執行，DOM 屬性可能為 `null`。  
- **開發時列印原始 JSON**；當 API 結構變更時，可協助除錯。

## 往後的方向

既然已掌握 **fetch api data**，你可以延伸此模式：

- **解析更複雜的 JSON**，並注入多個屬性。  
- **在 HTML 頁面內建立表格**，以呈現取得的資料。  
- **結合 Aspose.PDF**，產生包含即時 API 結果的 PDF。

上述皆建立在相同核心概念上：**execute async javascript**、**run async script**，以及 **set dom attribute**。盡情實驗吧——Aspose.HTML 的腳本引擎蘊藏著強大能量。

---

*開心寫程式！若遇到任何問題，歡迎在下方留言，我們一起排除故障。*

## 相關教學

- [How to Run JavaScript in Java – Complete Guide](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Append Element to Body with Aspose.HTML for Java using a DOM Mutation Observer](/html/english/java/advanced-usage/dom-mutation-observer-observing-node-additions/)
- [How to Set Timeout – Manage Network Timeout in Aspose.HTML for Java](/html/english/java/message-handling-networking/network-timeout/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}