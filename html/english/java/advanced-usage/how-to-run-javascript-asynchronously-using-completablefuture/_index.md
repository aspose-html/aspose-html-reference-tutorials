---
category: general
date: 2026-02-16
description: Learn how to run JavaScript in Java with CompletableFuture, delay JS,
  and evaluate async code. Complete step‑by‑step guide for async JavaScript evaluation.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: en
og_description: Master how to run JavaScript from Java, delay JS, and evaluate async
  code with CompletableFuture in this complete tutorial.
og_title: How to Run JavaScript Asynchronously Using CompletableFuture
tags:
- javascript
- java
- asynchronous
- completablefuture
title: How to Run JavaScript Asynchronously Using CompletableFuture
url: /java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Run JavaScript Asynchronously Using CompletableFuture

Ever wondered **how to run JavaScript** inside a Java application without blocking the main thread? Maybe you need to call a tiny script that fetches data, but you don’t want your UI to freeze. The good news is that modern Java libraries let you evaluate JavaScript **asynchronously**, and you can even introduce delays just like you would in a browser. In this guide we’ll show you a complete, runnable example that uses Aspose HTML’s `ScriptEngine` together with `CompletableFuture` to **how to run javascript** and get the result back in Java.

We’ll also cover **how to use CompletableFuture**, **how to delay JS**, and **how to evaluate async** code so you can **evaluate JavaScript asynchronously** in any Java project. By the end you’ll have a solid template you can copy‑paste, tweak, and embed in larger systems.

---

## What You’ll Learn

- Set up a Java `ScriptEngine` that can execute modern ES2022 JavaScript.
- Write an `async` function that includes a delay (`how to delay js`).
- Call `evaluateAsync` and receive a `CompletableFuture` (`how to use completablefuture`).
- Retrieve the result once the JavaScript promise resolves (`how to evaluate async`).
- Tips for error handling, thread management, and extending the pattern.

No external build tools are required beyond the Aspose HTML for Java JAR, which you can drop into your classpath. Let’s dive in.

---

## Step 1: How to Run JavaScript – Initialize the Scripting Engine

First things first. The Aspose HTML library provides a `ScriptEngine` class that can execute JavaScript code. Think of it as a tiny Chromium engine running inside your JVM.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Why this matters:** By instantiating `ScriptEngine` we get a sandboxed environment where modern JavaScript (including `async/await`) works out of the box. No need to spin up an external Node process.

---

## Step 2: How to Delay JS – Write an Async Function with a Promise‑Based Timer

JavaScript’s `setTimeout` is the classic way to pause execution. In modern code we wrap it in a `Promise` so we can `await` it. That’s exactly what we’ll do in the script string.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **How to delay js:** The `delay` helper creates a promise that settles after `ms` milliseconds. By `await`‑ing it, the function pauses without blocking the Java thread.

---

## Step 3: How to Evaluate Async – Run the Script and Get a CompletableFuture

Instead of the synchronous `evaluate` method, we call `evaluateAsync`. It immediately returns a `CompletableFuture<Object>` that will be completed when the JavaScript promise resolves.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **How to evaluate async:** `evaluateAsync` bridges the JavaScript event loop with Java’s `CompletableFuture`. This is the core of **evaluate javascript asynchronously**.

---

## Step 4: How to Use CompletableFuture – Attach a Callback and Block for Demo

Now we attach a callback with `thenAccept` to print the result, and we block the main thread just long enough for the demo to finish.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Why we call `get()`:** In a real application you’d probably continue processing elsewhere. Here we block to keep the example self‑contained.

---

## Visual Overview

![Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

*Alt text:* **Diagram showing how to run JavaScript asynchronously with CompletableFuture** – the image illustrates the flow from Java to the script engine, the async delay, and the CompletableFuture completion.

---

## Common Pitfalls & Best Practices (How to Evaluate Async Safely)

| Pitfall | What Happens | Fix |
|---------|--------------|-----|
| Forgetting to return the promise | `evaluateAsync` resolves immediately with `undefined` | Ensure the last line of the script is the promise (`fetchMessage();`) |
| Using blocking `Thread.sleep` in JS | Blocks the engine’s event loop, defeats async | Use the `delay` promise pattern (as shown) |
| Ignoring exceptions | Future completes exceptionally, but you never see it | Attach `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Not shutting down the engine | Resources leak in long‑running apps | Call `scriptEngine.dispose()` when done |

---

## Extending the Pattern (How to Use CompletableFuture in Real Projects)

You can chain multiple async JavaScript calls, combine them with other futures, or even run them on a custom `Executor`. Here’s a quick sketch:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **How to use CompletableFuture:** By passing an `Executor` you control the thread pool, keeping the UI responsive and avoiding thread‑starvation.

---

## Expected Output

Run the `JsAsyncDemo` class and you should see:

```
JS result: Hello from async JS!
```

The 500 ms pause isn’t visible in the console, but you can add timestamps to verify the delay if you wish.

---

## Recap – How to Run JavaScript with CompletableFuture

We started by **how to run javascript** inside Java, wrote an `async` function that **how to delay js**, executed it with `evaluateAsync` (**how to evaluate async**), and captured the result using a **how to use completablefuture**. The whole flow demonstrates **evaluate javascript asynchronously** in a clean, reusable pattern.

---

## What’s Next?

- **Integrate with HTTP clients:** Fetch data from a REST endpoint inside the async JS and return it to Java.
- **Use multiple scripts:** Chain several `evaluateAsync` calls for complex pipelines.
- **Swap engines:** The same pattern works with Nashorn, GraalVM, or other JavaScript runtimes—just replace `ScriptEngine`.

Feel free to experiment with longer delays, error‑throwing scripts, or even WebAssembly modules. The sky’s the limit when you combine Java’s concurrency primitives with modern JavaScript.

---

### Got Questions?

If something isn’t clear—maybe you’re wondering how to handle a rejected promise or how to pass variables from Java into the script—drop a comment below. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}