---
category: general
date: 2026-03-26
description: 顶层 await 示例，展示 await 延迟、递增计数器类和公共类字段的 JavaScript 实时演示。
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: zh
og_description: 顶层 await 示例，演示 await 延迟、递增计数器类和公共类字段的简明 JavaScript 教程。
og_title: 顶层 await 示例 – 在 JavaScript 中使用 await 延迟
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: 顶层 await 示例 – 在 JavaScript 中使用 await 延迟
url: /zh/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# top level await 示例 – 在 JavaScript 中使用 await delay

你是否曾想过如何在不将所有代码包装在 async IIFE 中的情况下暂停模块执行？这正是 **top level await example** 能做到的。在本教程中，我们将演示一个使用 `await delay javascript` 延迟工作的 tiny web page，然后创建一个利用 **public class fields javascript** 的 `increment counter class`。完成后，你将拥有一个完整的、可直接复制粘贴的代码片段，可在任何现代浏览器中运行。

我们将从定义带有公共字段的类到构建一个简单的基于 promise 的 delay 辅助函数全部讲解。无需外部库，无需构建步骤——只需普通的 HTML、一个 `<script type="module">`，以及最新的 ECMAScript 特性。如果你已经熟悉 async 函数，你会明白 top‑level await 为什么像是自然的扩展。如果你对 **javascript class public field** 语法还不熟悉，也别担心——我们会解释每行代码背后的原因。

## 你将学到

- 了解 **top level await example** 在模块脚本中的工作原理。
- `await delay javascript` 辅助函数的模式，它模仿使用 promise 的 `setTimeout`。
- 如何编写使用公共字段 (`count`) 和静态初始化块的 **increment counter class**。
- 预期的控制台输出以及如何验证静态块在脚本其余部分之前触发。
- 排查常见问题的技巧，例如不支持 top‑level await 的旧浏览器。

> **专业提示：** 现代浏览器（Chrome 106+、Firefox 102+、Edge 106+）已经支持 top‑level await。如果需要支持旧环境，考虑使用 Vite 或 Babel 等工具进行打包。

## 步骤 1 – 使用公共字段和静态块定义类

演示的第一部分是一个存储数值计数器的类。请注意 `count = 0;` 这一行——这是 ES2022 引入的 **public class fields javascript** 语法。它在没有构造函数的情况下创建实例属性。

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**为什么使用静态块？** 它让我们在模块被解析的瞬间（*在*任何 top‑level await 运行之前）运行一次性的初始化逻辑（例如日志记录）。这保证了消息首先出现在控制台，证明类已提前求值。

## 步骤 2 – 创建 `await delay javascript` 辅助函数

接下来我们需要一个小型的基于 promise 的 delay 函数。它本质上是 `setTimeout` 的包装，但返回 promise 使其可以被 await。

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**边缘情况：** 如果 `ms` 为负数或不是数字，`setTimeout` 会将其视为 `0`。你可以添加验证，但在演示中单行代码更易读。

## 步骤 3 – 使用 Top‑Level Await 暂停执行

现在登场的是本例的亮点：top‑level await。由于我们的脚本是模块（`type="module"`），我们可以直接在顶层作用域使用 `await`。这会让模块暂停，直到 promise 解析，从而控制副作用的执行顺序。

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**常见问题：** “我可以在普通的 `<script>` 标签中使用 top‑level await 吗？” 不能——只有模块脚本支持它。如果忘记 `type="module"`，会出现语法错误。

## 步骤 4 – 实例化类、递增并记录结果

最后我们将所有内容整合：创建实例，调用 `increment()`，并输出最终计数。这展示了 **increment counter class** 的实际运行。

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### 预期的控制台输出

```
Counter class initialized
Final count: 1
```

如果在 DevTools 中打开页面，你应该会看到 static‑block 消息在延迟完成之前 **出现**，从而确认类先被求值。

## 步骤 5 – 为什么使用公共类字段而不是构造函数？

你可能会想，为什么我们没有这样写：

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

两种方式都可行，但 **public class fields javascript** 提供了更简洁、更声明式的语法。字段只定义一次，而不是在每次构造函数调用中定义，当类变得更大时更易阅读。此外，静态块不能放在构造函数内部，因此将初始化逻辑分离得更自然。

## 步骤 6 – 将示例适配到真实应用

在生产环境中，你通常需要的不止一个计数器。以下是一些快速思路：

- **多个计数器：** 将它们存储在以标识符为键的 `Map` 中。
- **持久化状态：** 用 `localStorage` 写入取代 `console.log`。
- **异步初始化：** 使用静态块在创建任何实例之前从服务器获取配置。

所有这些模式仍然受益于 top‑level await，因为你可以在模块加载时一次性获取数据，并保证它对每个使用者都已准备好。

## 常见问题

**Q: top‑level await 会阻塞其他模块吗？**  
A: 不会。每个模块独立运行。只有包含 await 的模块会暂停；其他模块会并行加载。

**Q: 如果 delay promise 被拒绝会怎样？**  
A: 未处理的拒绝会中止模块求值，并在控制台显示错误。如果需要优雅的回退，请在 `await` 外层使用 `try…catch`。

**Q: `static` 关键字是必需的吗？**  
A: 对计数器本身不是必需的，但静态块是演示代码在加载时 *只运行一次* 的便捷方式——非常适合日志记录或特性检测。

## 结论

你刚刚构建了一个展示 `await delay javascript`、**increment counter class** 和 **public class fields javascript** 强大功能的 **top level await example**。完整、可运行的代码片段位于上方，控制台输出证明静态块在延迟代码运行之前就已触发。  

接下来，你可以尝试更复杂的 async 流程，用真实的 API 调用替代 delay，或为类添加更多方法。记住，现代 JavaScript 允许你将模块视为一等的 async 实体——无需额外的包装器。

祝编码愉快，欢迎在评论中分享你的变体。如果你觉得本指南有帮助，请分享给仍在与 async 模式搏斗的同事！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}