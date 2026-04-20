---
category: general
date: 2026-02-11
description: 使用 Aspose.HTML 在 Java 中创建 HTML 文档。了解如何获取 JSON JavaScript、添加 script 元素、从
  JSON 生成 HTML 并将 JSON 转换为 pre。
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: zh
og_description: 使用 Aspose.HTML 在 Java 中创建 HTML 文档。获取 JSON JavaScript，添加 script 元素，从
  JSON 生成 HTML 并将 JSON 转换为 pre——一站式教程。
og_title: 在 Java 中创建 HTML 文档 – 完整指南
tags:
- Aspose.HTML
- Java
- Web Automation
title: 使用 Java 创建 HTML 文档——获取 JSON 并生成内容
url: /zh/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 HTML 文档 – 完整的 Java 教程

是否曾需要**动态创建 HTML 文档**却不知如何将远程数据拉入其中？你并不孤单。在许多项目中，你会想要使用 JavaScript 获取 JSON，将结果注入页面，然后将最终的标记保存为静态文件。本指南将展示如何使用 Aspose.HTML for Java 完成此操作。

我们将逐步演示每一步：从实例化空文档、**获取 JSON JavaScript**、**添加 script 元素**，直到**从 JSON 生成 HTML**以及**将 JSON 转换为 pre**标签。完成后，你将拥有一个可直接使用的 `fetchResult.html`，其中包含以美化格式呈现的 JSON 数据。

## 前置条件

- Java 17 或更高版本（代码同样可以在 JDK 11+ 上编译）
- Aspose.HTML for Java 库（可通过 Maven Central 获取）
- 基本的 HTML 与异步 JavaScript 知识
- IDE 或普通的 `javac`/`java` 命令行

无需额外框架——所有内容均在本地运行。

## 第一步：设置项目并导入 Aspose.HTML

首先，将 Aspose.HTML 依赖添加到你的 `pom.xml`（或手动下载 JAR）。

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **专业提示：** 保持版本号为最新；新版会修复 bug 并改进脚本引擎。

## 第二步：**创建 HTML 文档** – 空白画布

我们先创建一个空的 `HTMLDocument`。把它想象成一张空白页，稍后我们会把脚本放进去。

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

为什么需要文档对象？Aspose.HTML 的 `ScriptEngine` 是基于 DOM 工作的，而不是对原始字符串操作。通过构建合适的文档，我们为引擎提供了真实的执行环境，以运行我们的**获取 JSON JavaScript**。

## 第三步：编写 JavaScript 代码片段 – **Fetch JSON JavaScript** 与 **Convert JSON to pre**

教程的核心在于这个多行字符串。它执行异步 `fetch`，解析 JSON，然后写入一个带有美化数据的 `<pre>` 元素。

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

注意注释 *Convert JSON to <pre>* ——这正是 `JSON.stringify(..., null, 2)` 所做的工作。它添加缩进，使输出易于阅读。

## 第四步：**添加 Script 元素** 到文档

现在我们创建一个 `<script>` 标签，把代码放进去，并将其附加到 body。这就是**添加 script 元素**的步骤。

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

为什么要附加到 body？在真实浏览器中，脚本会在解析时立即执行。将其追加到 DOM 中可以模拟相同的行为，确保异步 fetch 在我们随后调用引擎时运行。

## 第五步：运行脚本引擎 – 等待异步 Fetch 完成

Aspose.HTML 提供了 `ScriptEngine`，可以执行基于 DOM 的 JavaScript。我们调用 `run()` 并等待 promise 链完成。

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

引擎会阻塞，直到所有挂起任务（我们的 fetch）解析完毕，保证生成的 HTML 已经包含数据。

## 第六步：**从 JSON 生成 HTML** – 保存结果

最后我们将文档持久化到磁盘。文件中现在包含了带有 JSON 负载的 `<pre>` 块。

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

运行程序会生成 `fetchResult.html`。在任意浏览器打开，你会看到类似下面的内容：

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

这就是你想要的**从 JSON 生成 HTML**的结果。

## 完整可运行示例

下面是完整的、可直接运行的源文件。复制、粘贴，调整输出路径，然后执行 `java JsFetchExample`。

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

## 预期输出与验证

1. **控制台：** 会显示 `HTML with fetched data saved.`  
2. **文件（`fetchResult.html`）：** 打开后会在 `<pre>` 块中显示缩进好的 JSON。  
3. **验证：** 查看页面源代码，你会发现只有一个 `<pre>` 元素——脚本标签已被引擎执行，不会残留。

## 常见问题与边缘情况

| 问题 | 答案 |
|----------|--------|
| *如果 API 返回错误怎么办？* | 在 `fetch` 调用外层使用 `try…catch`，在出现异常时将错误信息写入 body，而不是 JSON。 |
| *可以一次获取多个资源吗？* | 可以——只需链式追加 `await fetch(...)` 调用或使用 `Promise.all`。最终的 `innerHTML` 可以拼接多个 `<pre>` 块。 |
| *需要设置 CORS 头吗？* | 由于脚本在 Aspose.HTML 的沙箱中运行，它遵循同源策略。公共的 JSONPlaceholder 接口已经允许跨域请求。 |
| *如何在运行时更改输出目录？* | 将路径作为命令行参数传入（`args[0]`），并在 `htmlDoc.save` 中替换硬编码的字符串。 |
| *能否嵌入 CSS 进行样式化？* | 完全可以。创建 `<style>` 元素，将 `textContent` 设置为你的 CSS，然后在运行引擎前追加到 `<head>`。 |

## 生产使用技巧

- **缓存 JSON**：如果接口响应慢，可以将获取的字符串写入文件并重复使用。  
- **对数据进行消毒**：在注入之前对数据进行清理，尤其是来源不可信时。安全使用 `JSON.stringify` 或转义 HTML 实体。  
- **配置 ScriptEngine 超时**：使用 `scriptEngine.setTimeout(5000)` 防止对无响应服务的长时间挂起。

## 可视化概览

![create html document example showing the generated HTML with JSON inside a pre tag](fetchResult.png "Screenshot of the generated HTML document")

*替代文字：* *create html document example – 生成的 HTML 文件在 pre 元素中显示获取的 JSON。*

## 结论

现在你已经掌握了如何在 Java 中**创建 HTML 文档**、**获取 JSON JavaScript**、**添加 script 元素**、**从 JSON 生成 HTML**以及**将 JSON 转换为 pre**以获得可读输出。整个工作流离线运行，仅需 Aspose.HTML，即可生成可随处部署的干净静态文件。

接下来，尝试让脚本循环遍历对象数组、添加 CSS 样式，或使用相同技术生成多页。你也可以将 `fetch` URL 替换为自己的 API，将动态数据转为静态快照——这对 SEO 友好的预渲染非常有用。

祝编码愉快，欢迎在评论区分享你的实验成果！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}