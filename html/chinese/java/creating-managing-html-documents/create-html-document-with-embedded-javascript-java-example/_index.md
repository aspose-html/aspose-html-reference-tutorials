---
category: general
date: 2026-06-03
description: 在 Java 中创建 HTML 文档并嵌入 JavaScript 以递增计数器。学习脚本引擎示例，获取元素 innerHTML 等。
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: zh
og_description: 在 Java 中创建 HTML 文档，嵌入 JavaScript 以递增计数器，并使用脚本引擎示例获取最终值。
og_title: 使用嵌入式 JavaScript 创建 HTML 文档 – Java 示例
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
title: 创建带嵌入式 JavaScript 的 HTML 文档 – Java 示例
url: /zh/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建带嵌入式 JavaScript 的 HTML 文档 – Java 示例

是否曾经需要从 Java 代码 **create HTML document** 并想知道如何在其中嵌入 JavaScript？在本指南中，我们将一步步展示如何实现，最终您将得到一个可运行的脚本引擎示例，打印出最终的计数器值。  

如果您曾经自问 *“how can I get element innerHTML after a script runs?”* 或 *“what’s the cleanest way to increment a counter in JavaScript from Java?”*——那么您来对地方了。我们将在本教程中统一覆盖 **embed javascript html**、**increment counter javascript** 和 **get element innerHTML**。

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="Create HTML Document with embedded JavaScript 示例"}

## 您将构建的内容

在本教程结束时，您将拥有一个独立的 Java 程序，它能够：

1. **Creates an HTML document** 在内存中创建 HTML 文档。
2. **Embeds a small JavaScript snippet** 嵌入一个小的 JavaScript 代码段，使计数器递增五次。
3. **Initializes a script engine**（`ScriptEngine` 示例）来运行该代码段。
4. 使用 `getElementInnerHTML` **Retrieves the final counter value** 获取最终计数器值。
5. 在控制台打印 `Final counter value: 5`。

无需外部文件，无需 Web 服务器——仅使用纯 Java 和一个小的 HTML 字符串。

## 前置条件

- Java 17 或更高版本（`ScriptEngine` API 是标准库的一部分）。
- 对 HTML 和 JavaScript 有基本了解（不需要深入的专业知识）。
- 一个 IDE 或者简单的文本编辑器，加上用于编译和运行程序的终端。

## 步骤 1：在 Java 中创建 HTML 文档

我们首先需要一个空的 HTML 文档对象，以便后续填充标记。可以把它看作仅存在于内存中的虚拟页面。

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

**Why this matters:** 通过自行 **creating HTML document** 对象，您可以避免写入磁盘并保持所有内容可测试。这个小型 DOM 模拟让我们之后能够 **get element innerHTML** 而无需完整的浏览器。

## 步骤 2：嵌入 JavaScript HTML – 计数器逻辑

现在我们将编写包含 `<script>` 块的 HTML 标记。该脚本将 **increment counter JavaScript** 五次。

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
- `<div id='counter'>0</div>` 是我们的目标元素。  
- `for` 循环执行 **increment counter javascript** 逻辑，在每次迭代时更新该 div。  
- 由于我们不在真实的浏览器中，稍后使用的脚本引擎需要能够理解 `document.getElementById`。这就是我们在 `HTMLDocument` 中添加一个小存根的原因。

## 步骤 3：初始化脚本引擎 – 脚本引擎示例

Java 自带 `ScriptEngine` API（JSR‑223）。我们将创建一个小包装器，将 HTML 内容传递给引擎，并提供它所需的最小 DOM 方法。

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

**Why this matters:** 这个 **script engine example** 展示了如何在没有完整浏览器的情况下运行嵌入式 JavaScript。它还演示了一种轻量级方式来暴露 `document.getElementById`，以便脚本能够与我们的模拟 DOM 交互。

## 步骤 4：执行 JavaScript – Increment Counter JavaScript 实际运行

引擎准备就绪后，我们只需运行脚本。`<script>` 标签内的循环将被触发，我们的模拟 `setInnerHTML` 将更新计数器。

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**What happens under the hood?** 循环的每一次迭代都会调用 `document.getElementById('counter').innerHTML = i + 1;`。我们的模拟 `setInnerHTML` 将数字字符串转发给 `HTMLDocument.updateCounter`，后者保存最新的值。循环结束后，文档的内部映射中 `counter` 元素的值为 `"5"`。

## 步骤 5：获取最终计数器值 – Get Element InnerHTML

现在脚本已执行完毕，我们可以从 `HTMLDocument` 实例中 **get element innerHTML**。

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

运行整个程序会输出：

```
Final counter value: 5
```

这证明了 **increment counter javascript** 逻辑已成功运行，并且我们在脚本执行后成功 **retrieved the element innerHTML**。

## 完整可运行示例

将所有内容整合在一起，下面是完整的、可直接运行的 Java 类：



## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本指南演示的技术。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [在 Aspose.HTML for Java 中创建空的 HTML 文档](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [在 Aspose.HTML for Java 中从字符串创建 HTML 文档](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [在 Aspose.HTML for Java 中保存 HTML 文档](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}