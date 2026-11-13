---
category: general
date: 2026-10-09
description: Learn how to call Java from JavaScript using Aspose.HTML, run async JavaScript,
  and fetch JSON in Java with a complete example and practical tips.
images:
- /java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/og-image.png
keywords:
- how to call java from javascript
- async fetch api java
- asynchronous javascript fetch example
- call java method from javascript
lastmod: 2026-10-09
og_description: Learn how to call Java from JavaScript using Aspose.HTML, run async
  JavaScript with the fetch API, and handle JSON callbacks in Java. Full example and
  troubleshooting tips.
og_image_alt: Diagram showing Java invoking JavaScript, async fetch returning JSON,
  and Java callback handling
og_title: How to call Java from JavaScript async fetch and JS engine
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn how to call Java from JavaScript using Aspose.HTML, run async
    JavaScript, and fetch JSON in Java with a complete example and practical tips.
  headline: ''
  type: TechArticle
- description: Learn how to call Java from JavaScript using Aspose.HTML, run async
    JavaScript, and fetch JSON in Java with a complete example and practical tips.
  name: ''
  steps:
  - name: The **asynchronous fetch API** successfully retrieved data.
    text: The **asynchronous fetch API** successfully retrieved data.
  - name: The JSON was serialized and handed over to Java.
    text: The JSON was serialized and handed over to Java.
  - name: Our **execute javascript engine** call completed without deadlocks.
    text: Our **execute javascript engine** call completed without deadlocks.
  type: HowTo
- questions:
  - answer: Yes. Any engine that supports host objects (e.g., Nashorn, GraalVM) can
      work, but Aspose.HTML provides a full browser‑like environment with built‑in
      `fetch`.
    question: Can I use this approach with other JavaScript engines?
  - answer: Serialize the object to JSON on the Java side and let JavaScript parse
      it, or expose multiple simple methods on the host object to pass individual
      fields.
    question: What if I need to return a complex Java object instead of a string?
  - answer: Aspose.HTML follows the WHATWG Fetch Standard, handling redirects, CORS,
      and streaming exactly as modern browsers do.
    question: Is the `fetch` implementation fully standards‑compliant?
  - answer: No. The `execute` call returns immediately; the internal engine processes
      the promise asynchronously. The main thread stays alive until the script finishes
      or you shut down the engine.
    question: Does this block the Java thread while waiting for the network?
  - answer: Use the `JavaScriptEngine.setDebugMode(true)` method to output console
      messages to the Java logger.
    question: How can I debug the JavaScript code inside the engine?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- async programming
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to call Java from JavaScript async fetch and JS engine

In this tutorial you’ll discover **how to call Java from JavaScript** using Aspose.HTML, run asynchronous JavaScript with the modern **fetch API**, and retrieve JSON data back into Java. The example runs entirely inside a Java‑backed HTML document—no external web server or extra libraries are required. By the end you’ll have a ready‑to‑run snippet that demonstrates a clean bridge between Java and JavaScript, perfect for server‑side rendering or custom scripting scenarios.

## Quick answers
- **What does this tutorial teach?** Calling Java from JavaScript, using async fetch, and handling JSON callbacks in Java.  
- **Which library is required?** Aspose.HTML for Java (version 23.7 or later).  
- **Do I need a web server?** No, everything runs locally inside the Java process.  
- **Is the fetch API supported?** Yes, Aspose.HTML implements the WHATWG Fetch Standard.  
- **Can I reuse the host object?** Absolutely—expose any public Java method you need.

## How to call Java from JavaScript using Aspose.HTML?

Load your HTML document, expose a Java host object, write an `async` function that uses `fetch`, and execute the script. The engine resolves the promise, calls the Java callback, and returns the JSON result—all without blocking the main thread. This approach lets you keep the Java side responsive while the JavaScript code performs network I/O, and it works the same way as in a browser environment.

## What is the async fetch API in Java?

The asynchronous fetch API is a browser‑compatible method that returns a `Promise`. Using `await` lets you write asynchronous code that reads like synchronous code, improving readability and error handling. In Aspose.HTML the fetch implementation follows the full WHATWG specification, so you get support for redirects, CORS, streaming responses, and proper error propagation, just as you would in modern browsers.

## Why use Aspose.HTML’s JavaScript engine?

Aspose.HTML supports **60+ input and output formats** and can process documents up to **500 MB** without loading the entire file into memory. Its built‑in `JavaScriptEngine` follows the full WHATWG Fetch Standard, giving you reliable network handling, redirects, and CORS support out of the box.

## Prerequisites
- Java 17 (or Java 11) installed and configured on your machine.  
- Aspose.HTML for Java 23.7 (or the latest release) on the classpath.  
- Internet connectivity for the demo JSON endpoint.  
- Basic understanding of Java methods and JavaScript promises.

## Step 1 – Create an empty HTML document and grab its JavaScript engine

The `Document` class represents an in‑memory HTML document and provides a sandboxed JavaScript engine.

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

**Why this matters:** The `Document` object mimics a browser window, and its `JavaScriptEngine` lets you run scripts exactly as a browser would. This is the foundation for **how to call Java from JavaScript**—the engine acts as the bridge.

## Step 2 – Register a host object so JavaScript can call back into Java

The `JavaCallback` host object exposes a single `onResult` method that prints the JSON payload received from JavaScript.

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
- Inside JavaScript you will invoke `javaCallback.onResult(...)`.  
- This is the core mechanism for **call java from javascript**—the script reaches into Java land, and Java reacts.

> **Pro tip:** Keep host‑object methods `public` and return simple types (String, int, boolean) to avoid serialization overhead.

## Step 3 – Write an asynchronous JavaScript function using the async fetch API

The `fetchJson` function demonstrates `async/await` with the standard fetch API.

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
- It works natively with `await`, so the flow reads top‑to‑bottom—perfect for an **asynchronous javascript fetch example**.  
- The API is future‑proof; most browsers and engines (including Aspose’s) support it out of the box.

## Step 4 – Execute the script inside the document’s JavaScript engine

Running the script triggers the event loop, resolves the network request, and calls back into Java.

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

## Step 5 – Handling errors and edge cases (optional enhancements)

Real‑world code rarely runs perfectly every time. Below are a few common pitfalls and how to guard against them.

### 5.1 Network failures

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

Now the Java side receives an error message instead of hanging.

### 5.2 Timeouts

Aspose’s engine doesn’t expose a native timeout for `fetch`, but you can implement one in JavaScript:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 Multiple calls

If you need to fetch several resources, simply loop or map over an array of URLs. The host object can be expanded to accept an identifier, letting you correlate responses.

## Complete working example

Below is the full source file you can copy‑paste into your IDE. No hidden dependencies, just the Aspose.HTML JAR on the classpath.

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

## Visual overview

![Diagram illustrating how Java calls JavaScript and receives async fetch results – call java from javascript](/images/java-js-async.png)

*The image shows the flow: Java → JavaScriptEngine → async fetch → JavaCallback.*

## Frequently asked questions

**Q: Can I use this approach with other JavaScript engines?**  
A: Yes. Any engine that supports host objects (e.g., Nashorn, GraalVM) can work, but Aspose.HTML provides a full browser‑like environment with built‑in `fetch`.

**Q: What if I need to return a complex Java object instead of a string?**  
A: Serialize the object to JSON on the Java side and let JavaScript parse it, or expose multiple simple methods on the host object to pass individual fields.

**Q: Is the `fetch` implementation fully standards‑compliant?**  
A: Aspose.HTML follows the WHATWG Fetch Standard, handling redirects, CORS, and streaming exactly as modern browsers do.

**Q: Does this block the Java thread while waiting for the network?**  
A: No. The `execute` call returns immediately; the internal engine processes the promise asynchronously. The main thread stays alive until the script finishes or you shut down the engine.

**Q: How can I debug the JavaScript code inside the engine?**  
A: Use the `JavaScriptEngine.setDebugMode(true)` method to output console messages to the Java logger.

## Conclusion

We’ve walked through a practical scenario that lets you **call Java from JavaScript**, **run async JavaScript**, and **fetch JSON in Java** using the **asynchronous fetch API**. By creating a host object, writing a tidy `async` function, and executing it with Aspose.HTML’s **JavaScript engine**, you get a clean, non‑blocking bridge between the two runtimes.

Feel free to change the endpoint URL, add more callbacks, or run several scripts in parallel. Next steps you might explore:

- Executing multiple scripts concurrently with separate `JavaScriptEngine` instances.  
- Using the async fetch pattern to process large data sets in parallel.  
- Integrating this bridge into a server‑side HTML renderer that pulls live data before rendering.

Happy coding!

---

**Last Updated:** 2026-10-09  
**Tested With:** Aspose.HTML for Java 23.7  
**Author:** Aspose

## Related Tutorials

- [Call Java From Javascript Add Host Object And Run Javascript](/html/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/)
- [How To Run Javascript In Java Complete Guide](/html/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Enable Script Execution In Java Complete Aspose Html Guide](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}