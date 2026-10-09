---
category: general
date: 2026-03-14
description: 学习如何使用 Aspose.HTML 从 JavaScript 调用 Java。本指南展示了如何添加宿主对象、在 Java 中运行 JavaScript，以及从
  JavaScript 进行日志记录。
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: zh
og_description: 使用 Aspose.HTML 从 JavaScript 调用 Java。添加宿主对象，在 Java 中运行 JavaScript，并在同一教程中记录
  JavaScript 日志。
og_title: 从 JavaScript 调用 Java – 带 Host 对象的完整指南
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: 从 JavaScript 调用 Java – 添加宿主对象并在 Java 中运行 JavaScript
url: /zh/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 JavaScript 调用 Java – 添加宿主对象并在 Java 中运行 JavaScript

是否曾经需要在 Java 应用程序内部 **call Java from JavaScript**？也许你正在构建一个动态 HTML 报告引擎，或者只是想将 Java 日志记录器暴露给你控制的脚本。在本教程中，你将看到如何添加宿主对象、在 Java 中运行 JavaScript，甚至 **log from JavaScript** 回到 JVM——全部使用 Aspose.HTML。

我们将通过一个完整、可运行的示例来演示：创建一个空的 HTML 文档，将 Java `Logger` 类注入为宿主对象，执行一段小脚本，并将结果打印到控制台。无需外部浏览器，也不需要神秘的“魔法”——只需复制粘贴下面的 Java 代码即可立即运行。

## 前置条件

- 已安装并配置 Java 17（或任意近期 JDK）。
- Aspose.HTML for Java 库（版本 23.10 或更高）。可从 Maven Central 或 Aspose 官网获取。
- 一个简单的 IDE 或文本编辑器；示例同样可以在命令行下运行。

> **专业提示：** 如果使用 Maven，请在 `pom.xml` 中添加以下依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

或者，使用 Gradle：

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

现在我们已经准备好基础环境，下面进入逐步实现。

## 第一步：创建最小化的 Java 项目

首先，新建一个名为 `JsHostObjectDemo` 的 Java 类。该类将包含我们的 `main` 方法以及宿主对象的定义。将所有内容放在同一个文件中，使教程自包含且易于复制。

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

Aspose.HTML 的 `HTMLDocument` 类会启动一个完整的 HTML‑5 兼容脚本环境。即使我们从不加载任何标记，文档的 `window` 对象仍然让我们能够访问 JavaScript 引擎，这正是 **run JavaScript in Java** 魔法发生的地方。

## 第二步：添加宿主对象 – “javaLogger”

下面这行代码

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

完成了 **add host object** 的核心工作。通过将 `Logger` 实例注册为名称为 `"javaLogger"` 的对象，文档中任何被求值的脚本都可以调用 `javaLogger.log(...)`。这正是 **javascript host object** 概念的核心：为 JavaScript 提供通往 JVM 的桥梁。

### 常见陷阱

- **命名冲突** – 如果你的脚本中已经存在全局变量 `javaLogger`，宿主对象会被覆盖。请使用唯一的名称。
- **线程安全** – 宿主对象在同一文档的多次脚本执行之间是共享的。如果计划并发运行脚本，请确保宿主类是线程安全的（例如使用 `synchronized` 或 `java.util.concurrent` 包中的原语）。

## 第三步：编写并执行 JavaScript

我们传入 `eval` 的脚本故意写得很小：

```javascript
javaLogger.log('Hello from JavaScript!');
```

当 `document.getWindow().eval(script)` 执行时，引擎会在全局作用域中查找 `javaLogger`，找到我们添加的 Java 对象，并使用提供的字符串调用其 `log` 方法。

### 预期输出

运行 `main` 方法后，控制台会打印以下内容：

```
[JS] Hello from JavaScript!
```

这行简短的输出证明我们已经成功 **call java from javascript**，并且 **log from javascript** 正常显示在普通的 Java `System.out` 消息位置。

## 第四步：扩展宿主对象 – 不止日志记录

如果需要暴露更多功能（例如文件访问、数据库查询），只需在 `Logger` 类中添加更多方法，或创建全新的宿主类。下面是一个同时返回值的快速示例：

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

这展示了 **javascript host object** 模式的灵活性：只要数据类型在 Java 与 JavaScript 之间可转换（原始类型、字符串、数组等），你就可以暴露任意 Java API。

## 第五步：清理资源

脚本环境使用完毕后，务必释放 `HTMLDocument` 以回收本地资源：

```java
document.dispose(); // Important for long‑running applications
```

如果不进行释放，尤其是在循环中创建大量文档时，可能会导致内存泄漏。

## 完整可运行示例

下面是完整的源文件，复制后即可编译运行。将其保存为 `JsHostObjectDemo.java`，确保 Aspose.HTML JAR 已加入类路径，然后执行 `java JsHostObjectDemo`。

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

运行该程序会得到：

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

这就是整个 **call java from javascript** 工作流，仅需几行代码即可实现。

## 常见问题

### 这在 Android 上可用吗？

Aspose.HTML 是纯 Java 库，可在任何 JVM 上运行，包括 Android 的 Dalvik/ART。只需将 JAR 打包进项目，即可拥有相同的宿主对象功能。

### 如果需要传递复杂对象怎么办？

你可以暴露 POJO（plain old Java objects），其中包含字段、getter 与 setter。引擎会自动将它们映射为 JavaScript 对象。对于集合，使用 `java.util.List` 或数组——两者都可转换。

### 错误处理如何进行？

如果脚本抛出 JavaScript 错误，`eval` 会传播 `ScriptException`。请使用 try‑catch 包裹调用，以便记录或恢复：

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### 能否顺序运行多个脚本？

完全可以。相同的 `HTMLDocument` 实例会保留全局作用域，你可以多次调用 `eval`。只需注意脚本之间的变量名冲突。

## 最佳实践与技巧

- **明确命名宿主对象**——如 `javaLogger`、`javaUtils`，以免混淆。
- **保持宿主方法简洁且无副作用**，这有助于调试。
- **及时释放文档**，以释放 Aspose.HTML 分配的本地内存。
- **对来自 JavaScript 的输入进行验证**，尤其是脚本来源不可信时。将其视作任何外部数据进行处理。

## 结论

现在，你已经掌握了通过 **add host object**、**run JavaScript in Java**、以及 **log from JavaScript**，使用 Aspose.HTML 实现 **call java from javascript** 的完整端到端示例。该模式功能强大：任何 Java 服务都可以暴露给脚本，使你的 Java 应用程序成为轻量级脚本平台。

接下来，你可以尝试：

- 注入完整的 HTML 页面并通过 JavaScript 操作 DOM。
- 使用宿主对象将数据流回 Java 端（例如 JSON 序列化）。
- 与 Nashorn、GraalVM 等其他脚本引擎集成，以获得更广泛的语言支持。

动手实验，修改 `Logger` 或 `Utils` 类，看看在自己的项目中能把 **javascript host object** 概念推向多远吧。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}