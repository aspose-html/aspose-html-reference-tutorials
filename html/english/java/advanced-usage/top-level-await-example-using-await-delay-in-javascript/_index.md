---
category: general
date: 2026-03-26
description: top level await example showing await delay javascript, increment counter
  class, and public class fields javascript in a live demo.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: en
og_description: top level await example that demonstrates await delay javascript,
  increment counter class, and public class fields javascript in a concise tutorial.
og_title: top level await example – Using await delay in JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: top level await example – Using await delay in JavaScript
url: /java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# top level await example – Using await delay in JavaScript

Ever wondered how to pause module execution without wrapping everything in an async IIFE? That's exactly what a **top level await example** lets you do. In this tutorial we’ll walk through a tiny web page that uses `await delay javascript` to defer work, then creates an `increment counter class` that leverages **public class fields javascript**. By the end you’ll have a complete, copy‑and‑paste snippet that runs in any modern browser.

We’ll cover everything from defining a class with a public field to wiring a simple promise‑based delay helper. No external libraries, no build step—just plain HTML, a `<script type="module">`, and the newest ECMAScript features. If you’re already comfortable with async functions, you’ll see why top‑level await feels like a natural extension. If you’re new to **javascript class public field** syntax, don’t worry—we explain the why behind each line.

## What You’ll Learn

- How a **top level await example** works inside a module script.
- The pattern for an `await delay javascript` helper that mimics `setTimeout` with promises.
- How to write an **increment counter class** that uses a public field (`count`) and a static initialization block.
- Expected console output and how to verify that the static block fires before the rest of the script.
- Tips for troubleshooting common pitfalls, such as older browsers that don’t support top‑level await.

> **Pro tip:** Modern browsers (Chrome 106+, Firefox 102+, Edge 106+) already support top‑level await. If you need to support older environments, consider bundling with a tool like Vite or Babel.

## Step 1 – Define a Class with a Public Field and a Static Block

The first piece of our demo is a class that stores a numeric counter. Notice the `count = 0;` line—this is the **public class fields javascript** syntax introduced in ES2022. It creates an instance property without a constructor.

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

**Why a static block?** It lets us run one‑off initialization logic (like logging) the moment the module is parsed, *before* any top‑level await runs. This guarantees the message appears first in the console, proving that the class was evaluated early.

## Step 2 – Create an `await delay javascript` Helper

Next we need a tiny promise‑based delay function. It’s essentially a wrapper around `setTimeout`, but returning a promise makes it awaitable.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Edge case:** If `ms` is negative or not a number, `setTimeout` treats it as `0`. You could add validation, but for a demo the one‑liner keeps things readable.

## Step 3 – Use Top‑Level Await to Pause Execution

Now comes the star of the show: top‑level await. Because our script is a module (`type="module"`), we can place `await` directly in the top scope. This pauses the module until the promise resolves, letting us control the order of side effects.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Common question:** “Can I use top‑level await in a normal `<script>` tag?” No—only module scripts support it. If you forget `type="module"`, you’ll get a syntax error.

## Step 4 – Instantiate the Class, Increment, and Log the Result

Finally we put everything together: create an instance, call `increment()`, and output the final count. This demonstrates the **increment counter class** in action.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Expected Console Output

```
Counter class initialized
Final count: 1
```

If you open the page in DevTools, you should see the static‑block message appear **before** the delay finishes, confirming that the class was evaluated first.

## Step 5 – Why Use Public Class Fields Instead of a Constructor?

You might wonder why we didn’t write:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Both approaches work, but **public class fields javascript** give you a cleaner, more declarative syntax. The field is defined once, not inside every constructor call, which can be easier to read when the class grows larger. Additionally, static blocks can’t be placed inside a constructor, so separating initialization logic becomes more natural.

## Step 6 – Adapting the Example for Real‑World Apps

In production you’ll often need more than a single counter. Here are a few quick ideas:

- **Multiple counters:** Store them in a `Map` keyed by identifier.
- **Persisted state:** Replace `console.log` with `localStorage` writes.
- **Async initialization:** Use the static block to fetch configuration from a server before any instances are created.

All of these patterns still benefit from top‑level await, because you can fetch data once at module load time and guarantee it’s ready for every consumer.

## Frequently Asked Questions

**Q: Does top‑level await block other modules?**  
A: No. Each module runs independently. Only the module that contains the await is paused; other modules continue loading in parallel.

**Q: What if the delay promise rejects?**  
A: An unhandled rejection will abort the module evaluation and surface as an error in the console. Wrap the await in a `try…catch` if you need graceful fallback.

**Q: Is the `static` keyword required?**  
A: Not for the counter itself, but the static block is a handy way to demonstrate that code runs *once* at load time—great for logging or feature‑detection.

## Conclusion

You’ve just built a **top level await example** that showcases `await delay javascript`, an **increment counter class**, and the power of **public class fields javascript**. The complete, runnable snippet lives above, and the console output proves that the static block fires before the delayed code runs.  

From here you can experiment with more complex async flows, swap the delay for a real API call, or expand the class with additional methods. Remember, modern JavaScript lets you treat modules as first‑class async entities—no extra wrappers needed.

Happy coding, and feel free to drop your variations in the comments. If you found this guide useful, share it with a teammate who’s still wrestling with async patterns!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}