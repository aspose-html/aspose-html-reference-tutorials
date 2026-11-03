---
category: general
date: 2026-10-14
description: 使用 Aspose.HTML 從 javascript 呼叫 java。了解如何新增 host object、在 java 中執行 javascript，以及從
  javascript 紀錄 log 的簡潔教學。
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: 使用 Aspose.HTML 從 javascript 呼叫 java。本指南展示如何新增 host object、在 java 中執行
  javascript，以及從 javascript 紀錄 log，只需幾行程式碼。
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: 從 javascript 呼叫 java – 新增 host object 並在 java 中執行 javascript
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: 從 javascript 呼叫 java – 新增 host object 並在 java 中執行 javascript
url: /zh-hant/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 JavaScript 呼叫 Java – 新增主機物件並在 Java 中執行 JavaScript

是否曾需要在 Java 應用程式中 **從 JavaScript 呼叫 Java**？也許你正在構建動態 HTML 報告引擎，或只是想將 Java logger 暴露給你控制的腳本。在本教學中，你將會看到如何新增主機物件、在 Java 中執行 JavaScript，甚至 **從 JavaScript 記錄** 回 JVM——全部使用 Aspose.HTML。

我們將逐步示範一個完整且可執行的範例，建立空的 HTML 文件，將 Java `Logger` 類別注入為主機物件，執行一段小腳本，並將結果列印到主控台。無需外部瀏覽器，沒有神祕的「魔法」——只要純粹的 Java 程式碼，你可以直接複製貼上並立即執行。

## 快速答案
- **如何新增主機物件？** 使用 `document.getWindow().addHostObject("name", object)` 註冊 Java 實例。  
- **我可以在 Java 中執行 JavaScript 嗎？** 可以——使用 `document.getWindow().eval(yourScript)`。  
- **可以從 JavaScript 記錄嗎？** 當然可以；主機物件可以公開任何 `void log(String)` 方法。  
- **需要哪個版本的 Aspose.HTML？** 版本 23.10 或更新版本支援完整的主機物件 API。  
- **需要瀏覽器嗎？** 不需要——Aspose.HTML 提供嵌入式引擎，所有操作皆在無頭環境下執行。

## 什麼是從 JavaScript 呼叫 Java？
**從 JavaScript 呼叫 Java** 是將 Java 物件暴露給 JavaScript 執行環境的技術，讓腳本能直接呼叫 Java 方法。Aspose.HTML 在 Java 程序內部建立輕量級的 JavaScript 引擎，實現無需外部瀏覽器的雙向溝通。

## 為何使用 Aspose.HTML 在 Java 中執行 JavaScript？
Aspose.HTML 支援 **50+ 輸入與輸出格式**，且能在完整符合 HTML5 標準的環境中評估 JavaScript。對於簡單的單行程式碼，平均執行時間約 200 ms，且不需載入完整的瀏覽器堆疊，與 Selenium 方案相比可減少高達 80 % 的記憶體使用。

## 前置條件

- 已安裝並設定 Java 17（或任何近期的 JDK）。  
- Aspose.HTML for Java 套件（版本 23.10 或更新）。可從 Maven Central 或 Aspose 官方網站取得。  
- 簡易的 IDE 或文字編輯器；範例亦可直接於命令列執行。

> **小技巧：** 如果使用 Maven，請在 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

或是 Gradle：

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

現在基礎已備妥，讓我們深入逐步解決方案。

## 如何新增主機物件並在 Java 中執行 JavaScript？
`addHostObject` 會將 Java 物件註冊為 JavaScript 全域變數。載入 `HTMLDocument`，使用 `addHostObject` 於名稱 `"javaLogger"` 下註冊 Java logger，接著評估呼叫 `javaLogger.log` 的簡短腳本。整個流程僅需三個 API 呼叫，且可在任何 Java 17 執行環境中運作。

### 步驟 1：建立最小的 Java 專案

首先，建立一個名為 `JsHostObjectDemo` 的新 Java 類別。此類別將包含 `main` 方法與主機物件定義。將所有程式碼放在同一檔案內，使教學自包含且易於複製。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### 為何使用 `HTMLDocument`？
`HTMLDocument` 代表記憶體中的 HTML 文件，並提供 JavaScript 引擎。`HTMLDocument` 會啟動完整的 HTML‑5 相容腳本環境。即使我們不載入任何標記，文件的 `window` 物件仍可讓我們存取 JavaScript 引擎，這正是 **在 Java 中執行 JavaScript** 的魔法所在。此外，你還可以操作 DOM、載入資源或評估腳本，而不需瀏覽器。

## 如何新增主機物件 – “javaLogger”？
`Logger` 是一個簡單的 Java 類別，具備 `log(String)` 方法，可將訊息寫入主控台。將 `Logger` 實例以名稱 `"javaLogger"` 註冊，使任何在此文件中評估的腳本都能呼叫 `javaLogger.log(...)`。這正是 **新增主機物件** 的核心需求，讓 logger 成為 JavaScript 的全域變數。

### 常見陷阱

- **命名衝突** – 若腳本中已存在全域變數 `javaLogger`，主機物件會被覆寫。請選擇唯一名稱。  
- **執行緒安全** – 主機物件在同一文件的多次腳本執行間會被共享。若計畫同時執行多個腳本，請確保主機類別具備執行緒安全（例如使用 `synchronized` 或 `java.util.concurrent` 原語）。

## 如何在 Java 中撰寫與執行 JavaScript？
`eval` 會在文件的腳本引擎中執行 JavaScript 字串，並回傳結果。將一段小腳本傳入 `eval`，引擎會從全域範圍解析 `javaLogger`，並以提供的字串呼叫其 `log` 方法。你亦可回傳值、處理例外，或串接多次評估以實作更複雜的互動。

### 預期輸出

執行 `main` 方法後，主控台會印出以下行：

```
[JS] Hello from JavaScript!
```

## 如何擴充主機物件 – 不只記錄？
主機物件是任何透過 `addHostObject` 暴露給 JavaScript 的 Java 實例。可透過在 `Logger` 類別加入其他方法，或建立全新主機類別，來提供額外功能。以下示例同時回傳值給 JavaScript。主機物件可暴露複雜型別、執行 I/O，或與其他服務互動。透過回傳值，腳本即可取得資料，實現 Java 與 JavaScript 之間的雙向通訊。

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

現在控制台顯示：

```
[JS] 3+4=7
```

## 執行腳本後如何清理資源？
`dispose` 會釋放 `HTMLDocument` 實例所持有的原生資源。當腳本環境不再使用時，務必呼叫 `document.dispose()` 以釋放原生記憶體。若未呼叫 `dispose()`，在迴圈或長時間服務中建立大量文件可能導致記憶體洩漏。建議使用 try‑with‑resources 區塊或在 finally 中確保呼叫 `document.dispose()`。

```java
document.dispose(); // Important for long‑running applications
```

## 完整範例

以下為完整的來源檔案，你可以立即編譯並執行。將檔案存為 `JsHostObjectDemo.java`，確保 Aspose.HTML JAR 已加入 classpath，然後執行 `java JsHostObjectDemo`。

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

執行此程式會得到：

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## 常見問題

**Q: 這在 Android 上可用嗎？**  
A: 可以。Aspose.HTML 為純 Java 函式庫，能在任何 JVM 上執行，包括 Android 的 ART 執行環境。

**Q: 若需要傳遞複雜物件該怎麼辦？**  
A: 你可以暴露具備 getter 與 setter 的 POJO，引擎會自動映射為 JavaScript 物件。`java.util.List` 或陣列等集合亦可轉換。

**Q: 錯誤處理機制如何運作？**  
A: 若腳本拋出 JavaScript 錯誤，`eval` 會傳遞 `ScriptException`。請將呼叫包在 try‑catch 區塊中，以記錄或恢復。

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: 可以連續執行多個腳本嗎？**  
A: 完全可以。相同的 `HTMLDocument` 會保留全域範圍，你可以多次呼叫 `eval`。只要妥善管理變數名稱以避免衝突即可。

**Q: 主機物件對不受信任的腳本安全嗎？**  
A: 請將任何外部腳本視為不受信任的輸入。驗證參數，並考慮只暴露最小必要方法以實作沙盒化。

## 最佳實踐與技巧

- **清晰命名主機物件**—`javaLogger`、`javaUtils` 等，以免混淆。  
- **盡可能讓主機方法保持小且無副作用**，這樣除錯較為容易。  
- **使用完畢即釋放文件**，可釋放 Aspose.HTML 所分配的原生記憶體。  
- **驗證來自 JavaScript 的輸入**，尤其當腳本來源不受信任時。將其視同任何外部資料處理。

## 結論

現在你已掌握一個完整的 **從 JavaScript 呼叫 Java** 範例，透過 **新增主機物件**、**在 Java 中執行 JavaScript**，以及 **從 JavaScript 記錄** 的方式，使用 Aspose.HTML 建立強大的腳本平台。此模式相當彈性：任何 Java 服務皆可暴露給腳本，讓你的 Java 應用程式變成輕量級的腳本執行環境。

接下來，你可以探索：

- 注入完整的 HTML 頁面，並從 JavaScript 操控 DOM。  
- 使用主機物件將資料串流回 Java 端（例如 JSON 序列化）。  
- 結合其他腳本引擎如 Nashorn 或 GraalVM，以支援更廣泛的語言。

試著調整 `Logger` 或 `Utils` 類別，看看在自己的專案中能將 **JavaScript 主機物件** 概念推向多遠。

---

**最後更新：** 2026-10-14  
**測試環境：** Aspose.HTML for Java 23.10  
**作者：** Aspose  

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## 相關教學

- [在 Java 中啟用腳本執行完整 Aspose HTML 指南](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [在 Java 中執行 Javascript 完整指南](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [如何在 Aspose HTML 中沙盒化 Javascript 完整指南](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}