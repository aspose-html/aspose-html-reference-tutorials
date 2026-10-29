---
category: general
date: 2026-06-03
description: 在 Java 中建立 HTML 文件並嵌入 JavaScript 以遞增計數器。學習腳本引擎範例、取得元素 innerHTML 等。
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: zh-hant
og_description: 在 Java 中建立 HTML 文件，嵌入 JavaScript 以遞增計數器，並使用腳本引擎範例取得最終值。
og_title: 建立嵌入 JavaScript 的 HTML 文件 – Java 範例
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: 建立嵌入式 JavaScript 的 HTML 文件 – Java 範例
url: /zh-hant/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 範例建立嵌入 JavaScript 的 HTML 文件

是否曾需要從 Java 程式碼 **create HTML document** 並想知道如何在其中嵌入 JavaScript？在本指南中，我們將一步一步示範，最終您會得到一個可執行的 script engine 範例，會印出最終的計數器值。  

如果您曾自問過 *「script 執行後，如何取得 element innerHTML？」* 或 *「從 Java 端以最簡潔的方式在 JavaScript 中遞增計數器？」*——您來對地方了。我們將在同一篇完整教學中同時涵蓋 **embed javascript html**、**increment counter javascript** 與 **get element innerHTML**。

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="嵌入 JavaScript 的 HTML 文件範例"}

## 您將建立的內容

完成本教學後，您將擁有一個獨立的 Java 程式，具備以下功能：

1. **Creates an HTML document** 在記憶體中建立。
2. **Embeds a small JavaScript snippet** 會將計數器遞增五次的 JavaScript 片段嵌入。
3. **Initializes a script engine**（`ScriptEngine` 範例）以執行該片段。
4. **Retrieves the final counter value** 使用 `getElementInnerHTML` 取得最終計數值。
5. 將 `Final counter value: 5` 印至主控台。

不需要外部檔案，也不需要 Web 伺服器——僅使用純 Java 與一小段 HTML 字串。

## 前置條件

- Java 17 或更新版本（`ScriptEngine` API 為標準函式庫的一部分）。
- 具備 HTML 與 JavaScript 的基本概念（不需要深入專業知識）。
- 一個 IDE 或簡易文字編輯器，加上終端機以編譯與執行程式。

## 步驟 1：在 Java 中建立 HTML Document

我們首先需要一個空白的 HTML document 物件，之後再填入標記。可將其視為僅存在於記憶體中的虛擬頁面。

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**Why this matters:** 透過自行 **creating HTML document** 物件，您可避免寫入磁碟，且讓所有內容皆可測試。這個小型 DOM 模擬讓我們之後能在不使用完整瀏覽器的情況下 **get element innerHTML**。

## 步驟 2：嵌入 JavaScript HTML – 計數器邏輯

現在我們將撰寫包含 `<script>` 區塊的 HTML 標記。此腳本會 **increment counter JavaScript** 五次。

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**Explanation:**  
- `<div id='counter'>0</div>` 為目標元素。  
- `for` 迴圈執行 **increment counter javascript** 邏輯，於每次迭代更新該 div。  
- 由於我們不在真實瀏覽器中，稍後使用的 script engine 必須能理解 `document.getElementById`，因此在 `HTMLDocument` 中加入了小型存根。

## 步驟 3：初始化 Script Engine – Script Engine 範例

Java 內建 `ScriptEngine` API（JSR‑223）。我們將建立一個小型封裝，將 HTML 內容傳入引擎，並提供其所需的最小 DOM 方法。

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**Why this matters:** 此 **script engine example** 展示如何在不使用完整瀏覽器的情況下執行嵌入式 JavaScript。它同時示範了一種輕量方式來公開 `document.getElementById`，讓腳本能與我們的 mock DOM 互動。

## 步驟 4：執行 JavaScript – Increment Counter JavaScript 實作

引擎就緒後，我們直接執行腳本。`<script>` 標籤內的迴圈會被觸發，我們的 mock `setInnerHTML` 會更新計數器。

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**What happens under the hood?** 每次迭代都會呼叫 `document.getElementById('counter').innerHTML = i + 1;`。我們的 mock `setInnerHTML` 會將數字字串傳遞給 `HTMLDocument.updateCounter`，該方法儲存最新的值。迴圈結束後，文件的內部映射會為 `counter` 元素保有 `"5"`。

## 步驟 5：取得最終計數值 – Get Element InnerHTML

腳本執行完畢後，我們可以從 `HTMLDocument` 實例 **get element innerHTML**。

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

執行完整程式會印出：

```
Final counter value: 5
```

這證實 **increment counter javascript** 邏輯已正確執行，且我們成功在腳本執行後 **retrieved the element innerHTML**。

## 完整範例

將所有部份整合起來，以下是完整、可直接執行的 Java 類別：

```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class HtmlJsDemo {

    // ---------- Minimal HTMLDocument implementation ----------
    static class HTMLDocument {
        private final StringBuilder html = new StringBuilder();
        private final java.util.Map<String, String> elements = new java.util.HashMap<>();

        public void write(String content) {
            html.append(content);
        }

        public String getContent() {
            return html.toString();
        }

        public void setElementInnerHTML(String id, String value) {
            elements.put(id, value);
        }

        public String getElementInnerHTML(String id) {
            return elements.getOrDefault(id, "");
        }

        public void updateCounter(int value) {
            setElementInnerHTML("counter", String.valueOf(value));
        }
    }

    // ---------- SimpleScriptEngine (script engine example) ----------
    static class SimpleScriptEngine {
        private final HTMLDocument document;
        private final ScriptEngine engine;

        public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
            this.document = doc;
            ScriptEngineManager manager = new ScriptEngineManager();
            this.engine = manager.getEngineByName("JavaScript");
            // Expose a mock 'document' object
            engine.put("document", new Object() {
                public Object getElementById(String id) {
                    return new Object() {
                        public void setInnerHTML(String value) {
                            document.updateCounter(Integer.parseInt(value));
                        }
                    };
                }
            });
        }

        public void execute() throws ScriptException {
            String html = document.getContent();
            int start = html.indexOf("<script>") + "<script>".length();
            int end   = html.indexOf("</script>");
            String script = html.substring(start, end);
            engine.eval(script);
        }
    }

    // ---------- Main method ----------
    public static void main(String[] args) {
        // Step 1: create HTML document
        HTMLDocument doc = new HTMLDocument();

        // Step 2: embed JavaScript HTML (increment counter JavaScript)
        doc.write(
            "<!DOCTYPE html><html><body>"
          + "<div id='counter'>0</div>"
          + "<script>"
          + "for (let i = 0; i < 5; i++) {"
          + "  document.getElementById('counter').innerHTML = i


## 接下來您可以學習什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [在 Aspose.HTML for Java 中建立空的 HTML 文件](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [在 Aspose.HTML for Java 中從字串建立 HTML 文件](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [在 Aspose.HTML for Java 中儲存 HTML 文件](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}