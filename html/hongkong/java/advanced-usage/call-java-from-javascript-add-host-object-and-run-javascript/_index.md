---
category: general
date: 2026-03-14
description: 學習如何使用 Aspose.HTML 從 JavaScript 呼叫 Java。本指南說明如何新增主機物件、在 Java 中執行 JavaScript，以及從
  JavaScript 進行日誌記錄。
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: zh-hant
og_description: 使用 Aspose.HTML 從 JavaScript 呼叫 Java。新增主機物件，在 Java 中執行 JavaScript，並在單一教學中從
  JavaScript 記錄日誌。
og_title: 從 JavaScript 呼叫 Java – 使用主機物件的完整指南
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: 從 JavaScript 呼叫 Java – 新增主機物件並在 Java 中執行 JavaScript
url: /zh-hant/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 JavaScript 呼叫 Java – 新增 Host 物件並在 Java 中執行 JavaScript

是否曾需要在 Java 應用程式中 **從 JavaScript 呼叫 Java**？也許你正在構建動態 HTML 報告引擎，或只是想將 Java logger 暴露給你控制的腳本。在本教學中，你將會看到如何新增 host 物件、在 Java 中執行 JavaScript，甚至 **從 JavaScript 記錄日誌** 回到 JVM——全部使用 Aspose.HTML。

我們將示範一個完整、可執行的範例：建立空的 HTML 文件、將 Java `Logger` 類別注入為 host 物件、執行一段小腳本，並將結果印到主控台。無需外部瀏覽器，沒有神祕的「魔法」——只要純粹的 Java 程式碼，你可以直接複製貼上並立即執行。

## 前置條件

- 安裝並設定 Java 17（或任何近期的 JDK）。
- Aspose.HTML for Java 函式庫（版本 23.10 或更新）。可從 Maven Central 或 Aspose 官方網站取得。
- 簡易的 IDE 或文字編輯器；此範例亦可在命令列下執行。

> **專業提示：** 如果你使用 Maven，請將以下相依性加入你的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

或者，對於 Gradle：

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

現在基礎已備妥，讓我們深入逐步解決方案。

## 步驟 1：建立最小化的 Java 專案

首先，建立一個名為 `JsHostObjectDemo` 的新 Java 類別。此類別將容納我們的 `main` 方法以及 host 物件的定義。將所有內容放在同一檔案中，使教學自成一體且易於複製。

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

### 為什麼使用 `HTMLDocument`？

Aspose.HTML 的 `HTMLDocument` 類別會啟動完整的 HTML‑5 相容腳本環境。即使我們從未載入任何標記，文件的 `window` 物件仍可讓我們存取 JavaScript 引擎，這正是 **在 Java 中執行 JavaScript** 的魔法所在。

## 步驟 2：新增 Host 物件 – “javaLogger”

以下程式碼行

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

完成 **新增 host 物件** 的核心工作。透過將 `Logger` 實例以名稱 `"javaLogger"` 註冊，任何在此文件中評估的腳本都能呼叫 `javaLogger.log(...)`。這正是 **javascript host object** 概念的核心：一座讓 JavaScript 觸及 JVM 的橋樑。

### 常見陷阱

- **命名衝突** – 若你的腳本中已存在全域變數 `javaLogger`，host 物件將被覆寫。請選擇唯一的名稱。
- **執行緒安全** – host 物件在同一文件的多次腳本執行間是共享的。若計畫同時執行多個腳本，請確保 host 類別具備執行緒安全（例如使用 `synchronized` 或 `java.util.concurrent` 原語）。

## 步驟 3：編寫並執行 JavaScript

我們餵入 `eval` 的腳本刻意寫得非常簡短：

```javascript
javaLogger.log('Hello from JavaScript!');
```

當 `document.getWindow().eval(script)` 執行時，引擎會在全域範圍中查找 `javaLogger`，找到先前加入的 Java 物件，並以提供的字串呼叫其 `log` 方法。

### 預期輸出

執行 `main` 方法會在主控台印出以下一行：

```
[JS] Hello from JavaScript!
```

這行簡短的輸出證明我們已成功 **從 JavaScript 呼叫 Java**，且 **從 JavaScript 記錄日誌** 正如普通的 Java `System.out` 訊息般出現在預期位置。

## 步驟 4：擴充 Host – 不僅僅是記錄日誌

如果需要暴露額外功能（例如檔案存取、資料庫查詢），只要在 `Logger` 類別中加入更多方法，或是建立全新的 host 類別。以下是一個同時回傳值的快速範例：

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

現在主控台會顯示：

```
[JS] 3+4=7
```

此範例展示了 **javascript host object** 模式的彈性：只要資料型別在 Java 與 JavaScript 之間可相互轉換（原始類型、字串、陣列等），你就能暴露任何需要的 Java API。

## 步驟 5：清理資源

當你完成腳本環境的使用後，請釋放 `HTMLDocument` 以釋放本機資源：

```java
document.dispose(); // Important for long‑running applications
```

若未釋放可能導致記憶體洩漏，尤其在迴圈中大量建立文件時更需注意。

## 完整範例

以下是完整的原始檔案，你可以立即編譯並執行。將其儲存為 `JsHostObjectDemo.java`，確保 Aspose.HTML JAR 已加入 classpath，然後執行 `java JsHostObjectDemo`。

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

這就是完整的 **從 JavaScript 呼叫 Java** 工作流程，僅需數行程式碼即可完成。

## 常見問題

### 這在 Android 上可用嗎？

Aspose.HTML 是純 Java 函式庫，因而可在任何 JVM 上執行，包括 Android 的 Dalvik/ART。只要將 JAR 包裝進專案，即可擁有相同的 host‑object 功能。

### 如果需要傳遞複雜物件該怎麼辦？

你可以暴露 POJO（plain old Java objects），只要它們包含欄位、getter 與 setter。引擎會自動將它們映射為 JavaScript 物件。對於集合，使用 `java.util.List` 或陣列——兩者皆可轉換。

### 錯誤處理機制如何運作？

若腳本拋出 JavaScript 錯誤，`eval` 會傳遞 `ScriptException`。請將呼叫包在 try‑catch 區塊中，以記錄或恢復：

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### 我可以依序執行多個腳本嗎？

絕對可以。相同的 `HTMLDocument` 實例會保留其全域範圍，因此你可以多次呼叫 `eval`。只需留意腳本之間的變數名稱衝突即可。

## 最佳實踐與技巧

- **清楚命名你的 host 物件**——`javaLogger`、`javaUtils` 等——以免混淆。
- **盡可能讓 host 方法保持小且無副作用**；這樣除錯會更容易。
- **盡早釋放文件**；這會釋放 Aspose.HTML 所分配的本機記憶體。
- **驗證來自 JavaScript 的輸入**，尤其當腳本來自不可信來源時。將其視為任何外部資料來處理。

## 結論

現在你已掌握一個完整、端對端的範例，說明如何透過 **新增 host 物件**、**在 Java 中執行 JavaScript**，以及 **從 JavaScript 記錄日誌** 來 **從 JavaScript 呼叫 Java**，全部使用 Aspose.HTML。此模式功能強大：任何 Java 服務都可以暴露給腳本，讓你的 Java 應用程式變成輕量級的腳本平台。

接下來，你可以探索：

- 注入完整的 HTML 頁面，並從 JavaScript 操控 DOM。
- 使用 host 物件將資料串流回 Java 端（例如 JSON 序列化）。
- 整合其他腳本引擎，如 Nashorn 或 GraalVM，以支援更廣泛的語言。

試著動手改寫 `Logger` 或 `Utils` 類別，看看在自己的專案中能將 **javascript host object** 概念推向多遠。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}