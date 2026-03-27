---
category: general
date: 2026-03-04
description: Call Java from JavaScript using Aspose.HTML, run async JavaScript, and
  fetch JSON in Java with a simple example. Learn to execute JavaScript engine efficiently.
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: en
og_description: Call Java from JavaScript with Aspose.HTML, run async JavaScript,
  and fetch JSON in Java. Full code, explanations, and tips included.
og_title: Call Java from JavaScript – Step‑by‑Step Async Fetch Tutorial
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: Call Java from JavaScript – Complete Guide to Async Fetch & JS Engine Execution
url: /java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Call Java from JavaScript – Full Tutorial with Async Fetch API

Ever wondered how to **call Java from JavaScript** without leaving your Java application? Maybe you’re building a server‑side HTML renderer, or you need to expose some Java logic to a script that runs inside a document. The good news is that Aspose.HTML makes this a piece of cake. In this guide we’ll not only show you how to *run async JavaScript* inside a Java‑backed document, but also how to **fetch JSON in Java** using the modern **asynchronous fetch API** and finally **execute JavaScript engine** calls safely.

In short, you’ll get a complete, runnable example that pulls a JSON payload from a public endpoint, hands it over to a Java host object, and prints the result on the console. No external web servers, no extra libraries—just pure Java and Aspose.HTML.

## What You’ll Learn

- How to create an empty HTML document with Aspose.HTML.
- How to obtain and **execute JavaScript engine** from Java.
- How to register a Java host object that JavaScript can invoke.
- How to write an **asynchronous JavaScript** function that uses the **asynchronous fetch API**.
- How to handle the fetched data back in Java with a clean callback.
- Expected output and troubleshooting tips.

### Prerequisites

- Java 17 or newer (the code compiles with JDK 11 as well).
- Aspose.HTML for Java 23.7 (or the latest version at the time of writing).
- Basic familiarity with Java and JavaScript promises.
- Internet access for the demo `jsonplaceholder` request.

If any of those sound unfamiliar, don’t panic—each step is explained in plain English, and you’ll see exactly why we do what we do.

---

## Step 1 – Create an Empty HTML Document and Grab Its JavaScript Engine

The first thing we need is a blank document that gives us a sandboxed JavaScript environment. Aspose.HTML’s `Document` class does exactly that.

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

**Why this matters:** The `Document` object mimics a browser window, and its `JavaScriptEngine` lets us run scripts exactly as a browser would. This is the foundation for **call java from javascript**—the engine acts as the bridge.

---

## Step 2 – Register a Host Object So JavaScript Can Call Back Into Java

Aspose.HTML allows you to expose any Java object to the script world. We’ll create an anonymous class with a single `onResult` method that simply prints whatever JSON we receive.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**Explanation:**  
- `addHostObject` binds the name `javaCallback` to the anonymous Java object.  
- Inside JavaScript we’ll call `javaCallback.onResult(...)`.  
- This is the core of **call java from javascript**—the script reaches into Java land, and Java reacts.

> **Pro tip:** Keep the host object's methods `public` and simple; complex objects can cause serialization headaches.

---

## Step 3 – Write an Asynchronous JavaScript Function Using the Asynchronous Fetch API

Now comes the fun part: a tiny script that fetches JSON from a remote endpoint. We’ll use `async/await`, which is the modern way to **run async JavaScript**.

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

**Why we choose `fetch` over older XHR:**  
- `fetch` returns a `Promise`, making the code cleaner.  
- It works natively with `await`, so the flow reads top‑to‑bottom—perfect for **asynchronous fetch api** demos.  
- The API is future‑proof; most browsers and engines (including Aspose’s) support it out of the box.

---

## Step 4 – Execute the Script Inside the Document’s JavaScript Engine

Finally, we hand the script to the engine. The engine will spin up a tiny event loop, resolve the `fetch` promise, and call back into Java when it’s done.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

When you run the `AsyncJsTutorial` class, you should see something like:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

That output confirms three things:

1. The **asynchronous fetch API** successfully retrieved data.  
2. The JSON was serialized and handed over to Java.  
3. Our **execute javascript engine** call completed without deadlocks.

---

## Step 5 – Handling Errors and Edge Cases (Optional Enhancements)

Real‑world code rarely runs perfectly every time. Below are a few common pitfalls and how to guard against them.

### 5.1 Network Failures

If the remote server is down, `fetch` throws. Wrap the call in a `try/catch` block:

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

Now the Java side will receive an error message instead of hanging.

### 5.2 Timeouts

Aspose’s engine doesn’t expose a native timeout for `fetch`, but you can implement one in JavaScript:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 Multiple Calls

If you need to fetch several resources, simply loop or map over an array of URLs. The host object can be expanded to accept an identifier, letting you correlate responses.

---

## Complete Working Example

Below is the **full source file** you can copy‑paste into your IDE. No hidden dependencies, just the Aspose.HTML JAR on the classpath.

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

**Expected console output**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

If you see an error line starting with `Error:` then something went wrong—most likely a network hiccup.

---

## Visual Overview

![Diagram illustrating how Java calls JavaScript and receives async fetch results – call java from javascript](/images/java-js-async.png)

*The image shows the flow: Java → JavaScriptEngine → async fetch → JavaCallback.*

---

## Frequently Asked Questions

**Can I use this approach with other JavaScript engines?**  
Yes, any engine exposing a host object mechanism (e.g., Nashorn, GraalVM) can work, but Aspose.HTML gives you a fully‑featured browser‑like environment with built‑in `fetch`.

**What if I need to return a complex Java object instead of a string?**  
You can serialize the object to JSON on the Java side and let JavaScript parse it, or you can expose multiple methods on the host object to receive separate fields.

**Is the `fetch` implementation fully standards‑compliant?**  
Aspose.HTML implements the WHATWG Fetch Standard, so you get proper handling of redirects, CORS, and streaming.

**Does this block the Java thread while waiting for the network?**  
No. The `execute` call returns immediately, and the internal engine processes the promise asynchronously. However, the main thread will stay alive until the script finishes or you explicitly shut down the engine.

---

## Conclusion

We’ve just walked through a practical scenario that lets you **call Java from JavaScript**, **run async JavaScript**, and **fetch JSON in Java** using the **asynchronous fetch API**. By creating a host object, writing a tidy `async` function, and executing it with Aspose.HTML’s **JavaScript engine**, you get a clean, non‑blocking bridge between the two runtimes.

Give it a spin, tweak the URL, or add more callbacks—your imagination is the limit. Next up you might explore:

- **Executing JavaScript engine** with multiple concurrent scripts.  
- Using **run async javascript** to process large data sets in parallel.  
- Integrating this pattern into a web‑service that renders dynamic HTML on the fly.

Feel free to experiment, and don’t hesitate to drop a comment if you hit an unexpected snag. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}