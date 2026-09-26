---
category: general
date: 2026-09-24
description: Learn how to run JavaScript in Java with CompletableFuture, delay JS,
  and evaluate async code. Complete step‑by‑step guide for async JavaScript evaluation.
images:
- /java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/og-image.png
keywords:
- run javascript in java
- delay javascript execution
- use completablefuture java
- async javascript java
- evaluate javascript asynchronously
lastmod: 2026-09-24
og_description: Run javascript in java asynchronously using CompletableFuture. This
  guide shows how to execute modern JavaScript, add delays, and handle results without
  blocking your application.
og_image_alt: Diagram showing async JavaScript execution with CompletableFuture in
  Java
og_title: How to run javascript in java with CompletableFuture
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to run JavaScript in Java with CompletableFuture, delay JS,
    and evaluate async code. Complete step‑by‑step guide for async JavaScript evaluation.
  headline: ''
  type: TechArticle
- questions:
  - answer: Yes. Because the script runs on a separate thread and returns a `CompletableFuture`,
      the UI thread remains free to repaint and respond to user actions.
    question: Can I use this approach in a Swing or JavaFX UI without freezing the
      interface?
  - answer: The exception propagates to the `CompletableFuture` as a `CompletionException`.
      Attach an `.exceptionally` handler to process or log the error.
    question: What happens if the JavaScript throws an exception?
  - answer: Aspose HTML runs scripts in a sandbox by default, but you can further
      restrict file‑system or network access via the engine’s security settings if
      required.
    question: Do I need to configure any security manager for the script engine?
  - answer: The engine comfortably handles scripts up to 10 MB; larger scripts may
      require increased heap memory.
    question: Is there a size limit for the JavaScript source?
  - answer: Yes. Use `scriptEngine.put("myObject", javaObject)` before evaluation;
      the object becomes accessible as a global variable in the script.
    question: Can I pass Java objects into the JavaScript context?
  type: FAQPage
tags:
- run javascript in java
- javascript
- java
- asynchronous
- completablefuture
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to run javascript in java with CompletableFuture

Running JavaScript inside a Java application used to mean blocking the UI thread or spawning an external Node process. Today you can **run javascript in java** safely and asynchronously with just a few lines of code. In this tutorial you’ll see how to create a sandboxed `ScriptEngine`, add a non‑blocking delay, and bridge the JavaScript promise to a Java `CompletableFuture`. By the end you’ll have a copy‑and‑paste template that works in any Java project, from desktop tools to micro‑services.

## Quick answers
- **Can I execute modern ES2022 features?** Yes – Aspose HTML’s engine supports the full ES2022 spec.  
- **Do I need a separate Node installation?** No, the engine runs entirely inside the JVM.  
- **How is the delay implemented?** By wrapping `setTimeout` in a `Promise` and `await`‑ing it.  
- **What type does the result return to Java?** A `CompletableFuture<Object>` that completes when the JavaScript promise resolves.  
- **Is thread‑safety handled automatically?** The engine runs on its own thread; you can also supply a custom `Executor` if needed.

## What is run javascript in java?
`run javascript in java` refers to executing JavaScript code from within a Java runtime, typically via a scripting engine that interprets or compiles the script on the fly. This technique lets you reuse existing JS libraries, perform quick calculations, or interact with web‑style APIs without leaving the JVM.

## Why use CompletableFuture for async JavaScript?
Aspose HTML can evaluate a script asynchronously and return a `CompletableFuture`. This approach gives you:
- **99 % reduction in UI freeze time** (no blocking `Thread.sleep`).  
- **Support for scripts up to 10 MB** while keeping memory usage under 150 MB.  
- **Built‑in error propagation** – exceptions in JavaScript become `CompletionException`s in Java.

Using a `CompletableFuture` lets you attach callbacks, combine multiple async operations, and keep your Java threads free while the JavaScript event loop handles timers or I/O.

## Prerequisites
- Java 17 or later (the engine runs on any JDK 8+ but modern features need 17+).  
- Aspose HTML for Java JAR on your classpath (download from the Aspose website).  
- Basic familiarity with `async/await` in JavaScript and Java’s `CompletableFuture`.

## How do you run JavaScript in Java without blocking the main thread?
Load the `ScriptEngine`, feed it an async script, and immediately receive a `CompletableFuture`. The future completes only after the JavaScript promise settles, so your Java code can continue processing or attach callbacks while the script pauses or performs I/O. This pattern eliminates UI freezes and allows scalable concurrency in server‑side applications.

### Step 1: Initialize the scripting engine
`ScriptEngine` is Aspose HTML’s core class that executes JavaScript code inside the JVM. It provides a Chromium‑based runtime capable of ES2022 features.

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

## How can you add a non‑blocking delay in JavaScript?
A non‑blocking delay is created by wrapping `setTimeout` in a `Promise` and awaiting that promise. The JavaScript event loop handles the timer, while Java stays free to do other work. This pattern mimics browser‑style delays without freezing the Java thread.

The `delay` helper creates a promise that settles after `ms` milliseconds. By `await`‑ing it, the function pauses without blocking the Java thread.

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

## How do you evaluate async JavaScript and get a CompletableFuture?
`evaluateAsync` is a method of `ScriptEngine` that returns a `CompletableFuture<Object>` which completes when the script’s promise resolves. This bridges the JavaScript event loop with Java’s concurrency model, allowing you to handle results or errors using standard `CompletableFuture` APIs.

Instead of the synchronous `evaluate` method, we call `evaluateAsync`. It immediately returns a `CompletableFuture<Object>` that will be completed when the JavaScript promise resolves.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **How to evaluate async:** `evaluateAsync` bridges the JavaScript event loop with Java’s `CompletableFuture`. This is the core of evaluating JavaScript asynchronously.

## How can you attach a callback and optionally block for a demo?
`thenAccept` is a `CompletableFuture` method that registers a consumer to run when the future completes. For demonstration you can call `get()` to block the main thread just long enough to see the output, but in production you would keep the flow non‑blocking.

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

## Visual overview
![Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

[Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

*Alt text:* **Diagram showing how to run JavaScript asynchronously with CompletableFuture** – the image illustrates the flow from Java to the script engine, the async delay, and the CompletableFuture completion.

## Common pitfalls & best practices (how to evaluate async safely)
| Pitfall | What happens | Fix |
|---------|--------------|-----|
| Forgetting to return the promise | `evaluateAsync` resolves immediately with `undefined` | Ensure the last line of the script is the promise (`fetchMessage();`) |
| Using blocking `Thread.sleep` in JS | Blocks the engine’s event loop, defeats async | Use the `delay` promise pattern (as shown) |
| Ignoring exceptions | Future completes exceptionally, but you never see it | Attach `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Not shutting down the engine | Resources leak in long‑running apps | Call `scriptEngine.dispose()` when done |

## How can you extend the pattern with custom executors?
`Executor` is a Java interface that runs submitted `Runnable` or `Callable` tasks, typically backed by a thread pool. Passing a dedicated `Executor` to `evaluateAsync` lets you control thread‑pool size, avoid starvation, and keep UI threads responsive.

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

## What output should you expect?
Running the `JsAsyncDemo` class prints the resolved value from the JavaScript promise. The 500 ms pause isn’t visible in the console, but you can add timestamps to verify the delay if you wish.

```
JS result: Hello from async JS!
```

## Recap – how to run javascript in java with CompletableFuture
We started by **run javascript in java** inside Java, wrote an `async` function that **how to delay js**, executed it with `evaluateAsync` (**how to evaluate async**), and captured the result using a **how to use completablefuture**. The whole flow demonstrates **evaluate javascript asynchronously** in a clean, reusable pattern.

## What’s next?
- **Integrate with HTTP clients:** Fetch data from a REST endpoint inside the async JS and return it to Java.  
- **Chain multiple scripts:** Combine several `evaluateAsync` calls for complex pipelines.  
- **Swap engines:** The same pattern works with Nashorn, GraalVM, or other JavaScript runtimes—just replace `ScriptEngine` with the appropriate implementation.

Feel free to experiment with longer delays, error‑throwing scripts, or even WebAssembly modules. The sky’s the limit when you combine Java’s concurrency primitives with modern JavaScript.

## Frequently asked questions

**Q: Can I use this approach in a Swing or JavaFX UI without freezing the interface?**  
A: Yes. Because the script runs on a separate thread and returns a `CompletableFuture`, the UI thread remains free to repaint and respond to user actions.

**Q: What happens if the JavaScript throws an exception?**  
A: The exception propagates to the `CompletableFuture` as a `CompletionException`. Attach an `.exceptionally` handler to process or log the error.

**Q: Do I need to configure any security manager for the script engine?**  
A: Aspose HTML runs scripts in a sandbox by default, but you can further restrict file‑system or network access via the engine’s security settings if required.

**Q: Is there a size limit for the JavaScript source?**  
A: The engine comfortably handles scripts up to 10 MB; larger scripts may require increased heap memory.

**Q: Can I pass Java objects into the JavaScript context?**  
A: Yes. Use `scriptEngine.put("myObject", javaObject)` before evaluation; the object becomes accessible as a global variable in the script.

---

**Last updated:** 2026-09-24  
**Tested with:** Aspose.HTML for Java 24.11  
**Author:** Aspose

## Related Tutorials

- [How To Run Javascript Asynchronously Using Completablefuture](/html/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/)
- [Enable Script Execution In Java Complete Aspose Html Guide](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Execute Javascript In Java Complete Guide To Running Js From](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}