---
category: general
date: 2026-03-04
description: 使用 Aspose.HTML 从 JavaScript 调用 Java，运行异步 JavaScript，并在 Java 中获取 JSON，示例简洁。学习高效执行
  JavaScript 引擎。
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: zh
og_description: 使用 Aspose.HTML 从 JavaScript 调用 Java，运行异步 JavaScript，并在 Java 中获取 JSON。提供完整代码、解释和技巧。
og_title: 从 JavaScript 调用 Java – 步骤式异步 Fetch 教程
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: 从 JavaScript 调用 Java – 异步获取与 JS 引擎执行完整指南
url: /zh/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 Java 调用 JavaScript – 使用异步 Fetch API 的完整教程

是否曾想过在不离开 Java 应用的情况下 **call Java from JavaScript**？也许你正在构建一个服务器端 HTML 渲染器，或者需要将某些 Java 逻辑暴露给文档内部运行的脚本。好消息是 Aspose.HTML 让这变得轻而易举。在本指南中，我们不仅会展示如何在基于 Java 的文档中 *run async JavaScript*，还会演示如何使用现代 **asynchronous fetch API** 在 **fetch JSON in Java**，以及如何安全地 **execute JavaScript engine** 调用。

简而言之，你将获得一个完整、可运行的示例：从公共端点获取 JSON 负载，将其交给 Java 主机对象，并在控制台打印结果。无需外部 Web 服务器，也不需要额外的库——只需纯 Java 和 Aspose.HTML。

## 你将学到

- 如何使用 Aspose.HTML 创建空的 HTML 文档。  
- 如何从 Java 获取并 **execute JavaScript engine**。  
- 如何注册一个 Java 主机对象，以便 JavaScript 调用。  
- 如何编写使用 **asynchronous fetch API** 的 **asynchronous JavaScript** 函数。  
- 如何在 Java 中通过干净的回调处理获取的数据。  
- 预期输出以及故障排除技巧。

### 前置条件

- Java 17 或更高（代码同样可以在 JDK 11 上编译）。  
- Aspose.HTML for Java 23.7（或撰写时的最新版本）。  
- 对 Java 和 JavaScript Promise 有基本了解。  
- 需要网络访问以进行演示 `jsonplaceholder` 请求。

如果上述任意一点你不熟悉，也不必惊慌——每一步都有通俗的英文解释，你会清楚我们为何如此操作。

---

## 第 1 步 – 创建空的 HTML 文档并获取其 JavaScript 引擎

我们首先需要一个空白文档，为我们提供一个沙箱化的 JavaScript 环境。Aspose.HTML 的 `Document` 类正是如此。

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

**为什么这很重要：** `Document` 对象模拟浏览器窗口，其 `JavaScriptEngine` 让我们能够像浏览器一样运行脚本。这是 **call java from javascript** 的基础——引擎充当桥梁。

---

## 第 2 步 – 注册主机对象，使 JavaScript 能回调 Java

Aspose.HTML 允许你将任意 Java 对象暴露给脚本世界。我们将创建一个仅包含 `onResult` 方法的匿名类，该方法会简单地打印我们收到的 JSON。

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**解释：**  
- `addHostObject` 将名称 `javaCallback` 绑定到匿名 Java 对象。  
- 在 JavaScript 中我们将调用 `javaCallback.onResult(...)`。  
- 这正是 **call java from javascript** 的核心——脚本进入 Java 领域，Java 作出响应。

> **小贴士：** 保持主机对象的方法 `public` 且简洁；复杂对象可能导致序列化问题。

---

## 第 3 步 – 使用异步 Fetch API 编写异步 JavaScript 函数

接下来是有趣的部分：一个从远程端点获取 JSON 的小脚本。我们将使用 `async/await`，这是 **run async JavaScript** 的现代写法。

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

**为何选择 `fetch` 而非旧的 XHR：**  
- `fetch` 返回 `Promise`，代码更简洁。  
- 它原生支持 `await`，因此流程自上而下阅读——非常适合 **asynchronous fetch api** 演示。  
- 该 API 面向未来；大多数浏览器和引擎（包括 Aspose 的）都开箱即用。

---

## 第 4 步 – 在文档的 JavaScript 引擎中执行脚本

最后，我们将脚本交给引擎。引擎会启动一个小型事件循环，解析 `fetch` Promise，并在完成后回调 Java。

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

运行 `AsyncJsTutorial` 类时，你应该会看到类似以下的输出：

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

该输出验证了三点：

1. **asynchronous fetch API** 成功检索到数据。  
2. JSON 已序列化并传递给 Java。  
3. 我们的 **execute javascript engine** 调用在没有死锁的情况下完成。

---

## 第 5 步 – 错误处理与边缘情况（可选增强）

实际项目中的代码很少每次都完美运行。下面列出了一些常见陷阱及其防护措施。

### 5.1 网络故障

如果远程服务器不可用，`fetch` 会抛出异常。请使用 `try/catch` 包裹调用：

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

这样 Java 端将收到错误信息，而不是卡住。

### 5.2 超时

Aspose 的引擎未对 `fetch` 提供原生超时，但你可以在 JavaScript 中实现：

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 多次调用

如果需要获取多个资源，只需对 URL 数组进行循环或映射。主机对象可以扩展为接受标识符，以便关联响应。

---

## 完整工作示例

下面是可以直接复制到 IDE 中的 **full source file**。没有隐藏依赖，只需在类路径上加入 Aspose.HTML JAR。

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

**预期的控制台输出**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

如果看到以 `Error:` 开头的行，则说明出现了错误——通常是网络波动导致。

---

## 可视化概览

![Diagram illustrating how Java calls JavaScript and receives async fetch results – call java from javascript](/images/java-js-async.png)

*该图展示了流程：Java → JavaScriptEngine → async fetch → JavaCallback。*

---

## 常见问题

**我可以将此方法用于其他 JavaScript 引擎吗？**  
可以，任何提供主机对象机制的引擎（如 Nashorn、GraalVM）都能工作，但 Aspose.HTML 为你提供了一个功能完整、类浏览器的环境，并内置 `fetch`。

**如果需要返回复杂的 Java 对象而不是字符串怎么办？**  
可以在 Java 端将对象序列化为 JSON 供 JavaScript 解析，或在主机对象上暴露多个方法以接收不同字段。

**`fetch` 实现是否完全符合标准？**  
Aspose.HTML 实现了 WHATWG Fetch Standard，能够正确处理重定向、CORS 与流式传输。

**这会阻塞 Java 线程吗？**  
不会。`execute` 调用会立即返回，内部引擎会异步处理 Promise。不过，主线程会保持存活，直至脚本结束或你显式关闭引擎。

---

## 结论

我们已经完整演示了如何 **call Java from JavaScript**、**run async JavaScript**，以及使用 **asynchronous fetch API** 在 **fetch JSON in Java**。通过创建主机对象、编写整洁的 `async` 函数，并使用 Aspose.HTML 的 **JavaScript engine** 执行，你可以获得一个干净、非阻塞的双运行时桥梁。

快去试一试，修改 URL，或添加更多回调——想象力就是唯一的限制。接下来你可以探索：

- 使用 **Executing JavaScript engine** 处理多个并发脚本。  
- 用 **run async javascript** 并行处理大数据集。  
- 将此模式集成到能够即时渲染动态 HTML 的 Web 服务中。

欢迎实验，如遇意外问题请留言。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}