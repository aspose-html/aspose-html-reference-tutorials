---
category: general
date: 2026-10-14
description: 使用 Aspose.HTML 从 JavaScript 调用 Java。学习如何添加宿主对象、在 Java 中执行 JavaScript，以及从
  JavaScript 进行日志记录的简明教程。
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: 使用 Aspose.HTML 从 JavaScript 调用 Java。本指南展示了如何添加宿主对象、在 Java 中执行 JavaScript，以及从
  JavaScript 进行日志记录，仅需几行代码。
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: 从 JavaScript 调用 Java – 添加宿主对象并在 Java 中运行 JavaScript
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
title: 从 JavaScript 调用 Java – 添加宿主对象并在 Java 中运行 JavaScript
url: /zh/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 JavaScript 调用 Java – 添加宿主对象并在 Java 中运行 JavaScript

是否曾经需要在 Java 应用程序中**从 JavaScript 调用 Java**？也许你正在构建一个动态 HTML 报告引擎，或者只是想将 Java 日志记录器暴露给你控制的脚本。在本教程中，你将看到如何添加宿主对象、在 Java 中运行 JavaScript，甚至**从 JavaScript 记录日志**回到 JVM——全部使用 Aspose.HTML。

我们将演示一个完整、可运行的示例，创建一个空的 HTML 文档，将 Java `Logger` 类注入为宿主对象，执行一个小脚本，并将结果打印到控制台。无需外部网页浏览器，也没有神秘的“魔法”——只是一段可以复制粘贴并立即运行的普通 Java 代码。

## 快速答案
- **如何添加宿主对象？** 使用 `document.getWindow().addHostObject("name", object)` 注册一个 Java 实例。  
- **我可以在 Java 中执行 JavaScript 吗？** 可以——使用 `document.getWindow().eval(yourScript)`。  
- **可以从 JavaScript 记录日志吗？** 当然；宿主对象可以公开任何 `void log(String)` 方法。  
- **需要哪个版本的 Aspose.HTML？** 版本 23.10 或更高版本支持完整的宿主对象 API。  
- **我需要网页浏览器吗？** 不需要——Aspose.HTML 提供嵌入式引擎，所有操作均在无头模式下运行。

## 什么是从 JavaScript 调用 Java？
**Call java from javascript** 是一种将 Java 对象暴露给 JavaScript 运行时的技术，使脚本能够直接调用 Java 方法。Aspose.HTML 在 Java 进程内部创建了轻量级的 JavaScript 引擎，实现了无外部浏览器的无缝双向通信。

## 为什么在 Java 中使用 Aspose.HTML 执行 JavaScript？
Aspose.HTML 支持 **50 多种输入和输出格式**，并且能够在完全符合 HTML5 标准的环境中评估 JavaScript。对于简单的单行代码，它平均在 200 ms 内处理脚本，并且无需加载完整的浏览器堆栈，与基于 Selenium 的方案相比，可将内存使用量降低高达 80 %。

## 先决条件

- Java 17（或任何近期的 JDK）已安装并配置。  
- Aspose.HTML for Java 库（版本 23.10 或更高）。可从 Maven Central 或 Aspose 网站获取。  
- 一个简单的 IDE 或文本编辑器；示例同样可以在命令行运行。

> **专业提示：** 如果使用 Maven，请在 `pom.xml` 中添加以下依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

或者，对于 Gradle：

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

现在我们已经理清了基础，让我们深入逐步解决方案。

## 如何添加宿主对象并在 Java 中运行 JavaScript？

`addHostObject` 将 Java 对象注册为 JavaScript 上下文中的全局变量。加载你的 `HTMLDocument`，使用 `addHostObject` 将 Java 日志记录器注册为名称为 `"javaLogger"` 的对象，然后评估调用 `javaLogger.log` 的短脚本。整个流程仅需三次 API 调用，适用于任何 Java 17 运行时。

### 步骤 1：创建一个最小的 Java 项目

首先，创建一个名为 `JsHostObjectDemo` 的新 Java 类。该类将包含我们的 `main` 方法和宿主对象定义。将所有内容放在一个文件中，使教程自包含且易于复制。

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

### 为什么使用 `HTMLDocument`？

`HTMLDocument` 表示一个内存中的 HTML 文档，并提供 JavaScript 引擎。`HTMLDocument` 类启动了完整的 HTML‑5 兼容脚本环境。即使我们从未加载任何标记，文档的 `window` 对象也让我们访问 JavaScript 引擎，这正是 **在 Java 中运行 JavaScript** 的魔法所在。此外，你还可以操作 DOM、加载资源或在没有浏览器的情况下评估脚本。

## 如何添加宿主对象 – “javaLogger”？

`Logger` 是一个简单的 Java 类，具有 `log(String)` 方法，可将消息写入控制台。将 `Logger` 实例注册为名称为 `"javaLogger"` 的对象，使得在此文档中评估的任何脚本都可以调用 `javaLogger.log(...)`。这就是 **添加宿主对象** 要求的核心，使日志记录器作为全局变量对 JavaScript 代码可用。

### 常见陷阱

- **命名冲突** – 如果你的脚本中已经有名为 `javaLogger` 的全局变量，宿主对象将被覆盖。请选择唯一的名称。  
- **线程安全** – 宿主对象在同一文档的脚本执行之间共享。如果计划并发运行脚本，请使宿主类线程安全（例如，使用 `synchronized` 或 `java.util.concurrent` 原语）。

## 如何在 Java 中编写并执行 JavaScript？

`eval` 在文档的脚本引擎中执行 JavaScript 字符串并返回任何结果。将一个小脚本传入 `eval`。引擎从全局作用域解析 `javaLogger` 并使用提供的字符串调用其 `log` 方法。你还可以返回值、处理异常，并链式执行多个评估以实现更复杂的交互。

### 预期输出

运行 `main` 方法会在控制台打印以下行：

```
[JS] Hello from JavaScript!
```

## 如何扩展宿主对象 – 不仅仅是日志记录？

宿主对象是通过 `addHostObject` 暴露给 JavaScript 的任何 Java 实例。通过向 `Logger` 类添加方法或创建新宿主类来提供额外功能。下面是一个快速示例，它还向 JavaScript 返回一个值。宿主对象可以暴露复杂类型、执行 I/O 或与其他服务交互。通过返回值，脚本可以接收返回数据，实现 Java 与 JavaScript 之间的双向通信。

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

现在控制台显示：

```
[JS] 3+4=7
```

## 运行脚本后如何清理资源？

`dispose` 释放 `HTMLDocument` 实例持有的本机资源。当你完成脚本环境后，需处置 `HTMLDocument` 以释放本机资源。如果未调用 `dispose()`，可能导致内存泄漏，尤其是在循环或长期运行的服务中创建大量文档时。始终将使用包装在 try‑with‑resources 块中，或确保在 finally 子句中调用 `document.dispose()`。

```java
document.dispose(); // Important for long‑running applications
```

## 完整工作示例

下面是完整的源文件，你可以立即编译并运行。将其保存为 `JsHostObjectDemo.java`，确保 Aspose.HTML JAR 在你的类路径上，然后执行 `java JsHostObjectDemo`。

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

运行此程序会得到：

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## 常见问题

**问：这在 Android 上可用吗？**  
答：可以。Aspose.HTML 是纯 Java 库，可在任何 JVM 上运行，包括 Android 的 ART 运行时。

**问：如果需要传递复杂对象怎么办？**  
答：你可以暴露带有 getter 和 setter 的 POJO；引擎会自动将它们映射为 JavaScript 对象。诸如 `java.util.List` 或数组的集合也可以转换。

**问：错误处理如何工作？**  
答：如果脚本抛出 JavaScript 错误，`eval` 会传播 `ScriptException`。将调用包装在 try‑catch 块中以记录或恢复。

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**问：我可以顺序运行多个脚本吗？**  
答：完全可以。相同的 `HTMLDocument` 保持全局作用域，你可以多次调用 `eval`。只需管理变量名以避免冲突。

**问：宿主对象对不受信任的脚本安全么？**  
答：将任何外部脚本视为不受信任的输入。验证参数，并通过仅暴露最小必需方法来考虑沙箱化。

## 最佳实践与技巧

- **清晰命名你的宿主对象**——如 `javaLogger`、`javaUtils` 等——以避免混淆。  
- **尽可能保持宿主方法简短且无副作用**；这使调试更容易。  
- **在完成后立即处置文档**；它会释放 Aspose.HTML 分配的本机内存。  
- **验证来自 JavaScript 的输入**，尤其是脚本来自不受信任的来源时。将其视为任何外部数据来处理。

## 结论

现在，你已经拥有一个完整的示例，展示如何通过 **添加宿主对象**、**在 Java 中运行 JavaScript** 和 **从 JavaScript 记录日志** 来 **从 JavaScript 调用 Java**，使用 Aspose.HTML。该模式功能强大：任何 Java 服务都可以暴露给脚本，使你的 Java 应用程序成为轻量级脚本平台。

接下来，你可以探索：

- 注入完整的 HTML 页面并从 JavaScript 操作 DOM。  
- 使用宿主对象将数据流回 Java 端（例如 JSON 序列化）。  
- 与其他脚本引擎（如 Nashorn 或 GraalVM）集成，以获得更广泛的语言支持。

尝试一下，修改 `Logger` 或 `Utils` 类，看看在自己的项目中能够将 **JavaScript 宿主对象** 概念推向多远。

---

**最后更新：** 2026-10-14  
**测试环境：** Aspose.HTML for Java 23.10  
**作者：** Aspose  

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## 相关教程

- [在 Java 中启用脚本执行完整 Aspose HTML 指南](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [在 Java 中执行 JavaScript 完整指南](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [如何在 Aspose HTML 中对 Javascript 进行沙箱化完整指南](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}