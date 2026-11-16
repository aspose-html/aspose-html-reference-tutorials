---
category: general
date: 2026-02-11
description: Create HTML document in Java using Aspose.HTML. Learn how to fetch JSON
  JavaScript, add script element, generate HTML from JSON and convert JSON to pre.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: en
og_description: Create HTML document in Java with Aspose.HTML. Fetch JSON JavaScript,
  add script element, generate HTML from JSON and convert JSON to pre—all in one tutorial.
og_title: Create HTML Document in Java – Full Guide
tags:
- Aspose.HTML
- Java
- Web Automation
title: Create HTML Document with Java – Fetch JSON and Generate Content
url: /java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create HTML Document – Full Java Tutorial

Ever needed to **create HTML document** on the fly but weren’t sure how to pull remote data into it? You’re not alone. In many projects you’ll want to fetch JSON with JavaScript, inject the result into a page, and then save the final markup as a static file. This guide shows you exactly how to do that using Aspose.HTML for Java.

We’ll walk through every step: from instantiating an empty document, to **fetch JSON JavaScript**, to **add script element**, and finally to **generate HTML from JSON** and **convert JSON to pre** tags. By the end you’ll have a ready‑to‑use `fetchResult.html` that contains the fetched data rendered as pretty‑printed JSON.

## Prerequisites

- Java 17 or newer (the code compiles with JDK 11+ as well)
- Aspose.HTML for Java library (available via Maven Central)
- Basic familiarity with HTML and async JavaScript
- An IDE or plain `javac`/`java` command line

No additional frameworks are required—everything runs locally.

## Step 1: Set Up the Project and Import Aspose.HTML

First, add the Aspose.HTML dependency to your `pom.xml` (or download the JAR manually).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Pro tip:** Keep the version number up‑to‑date; newer releases fix bugs and improve the script engine.

## Step 2: **Create HTML Document** – the Blank Canvas

We start by creating an empty `HTMLDocument`. Think of it as a fresh page where we’ll later drop our script.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Why do we need a document object? Aspose.HTML’s `ScriptEngine` works against a DOM, not a raw string. By building a proper document we give the engine a real environment to execute our **fetch JSON JavaScript**.

## Step 3: Write the JavaScript Snippet – **Fetch JSON JavaScript** and **Convert JSON to pre**

The heart of the tutorial lives in this multiline string. It performs an asynchronous `fetch`, parses the JSON, then writes a `<pre>` element with pretty‑printed data.

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

Notice the comment *Convert JSON to <pre>* – that’s exactly what the `JSON.stringify(..., null, 2)` call does. It adds indentation, making the output human‑readable.

## Step 4: **Add Script Element** to the Document

Now we create a `<script>` tag, drop our code inside, and attach it to the body. This is the **add script element** part.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Why attach it to the body? In a real browser the script would run as soon as it’s parsed. By appending it to the DOM we mimic that exact behavior, ensuring the asynchronous fetch runs when we later invoke the engine.

## Step 5: Run the Script Engine – Let the Async Fetch Finish

Aspose.HTML provides a `ScriptEngine` that can execute the DOM‑based JavaScript. We call `run()` and wait for the promise chain to settle.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

The engine blocks until all pending tasks (our fetch) are resolved, guaranteeing that the generated HTML already contains the data.

## Step 6: **Generate HTML from JSON** – Save the Result

Finally we persist the document to disk. The file now contains the `<pre>` block with the JSON payload.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

Running the program produces `fetchResult.html`. Open it in any browser and you’ll see something like:

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

That’s the **generate HTML from JSON** result you were after.

## Full Working Example

Below is the complete, ready‑to‑run source file. Copy, paste, adjust the output path, and hit `java JsFetchExample`.

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

## Expected Output & Verification

1. **Console:** You’ll see `HTML with fetched data saved.`  
2. **File (`fetchResult.html`):** Opening it displays the JSON inside a `<pre>` block, nicely indented.  
3. **Validation:** If you view the page source, you’ll find only a `<pre>` element—no extra script tags remain because the engine has already executed them.

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if the API returns an error?* | Wrap the `fetch` call in a `try…catch` block and write an error message to the body instead of the JSON. |
| *Can I fetch multiple resources?* | Yes—just chain additional `await fetch(...)` calls or use `Promise.all`. The final `innerHTML` can concatenate several `<pre>` blocks. |
| *Do I need to set CORS headers?* | Since the script runs inside Aspose.HTML’s sandbox, it respects the same‑origin policy. The public JSONPlaceholder endpoint already allows cross‑origin requests. |
| *How to change the output directory at runtime?* | Pass the path as a command‑line argument (`args[0]`) and replace the hard‑coded string in `htmlDoc.save`. |
| *Is there a way to embed CSS for styling?* | Absolutely. Create a `<style>` element, set its `textContent` to your CSS, and append it to `<head>` before running the engine. |

## Tips for Production Use

- **Cache the JSON** if the endpoint is slow; you can write the fetched string to a file and reuse it.
- **Sanitize the data** before injecting it, especially if the source isn’t trusted. Use `JSON.stringify` safely or escape HTML entities.
- **Configure the ScriptEngine timeout** (`scriptEngine.setTimeout(5000)`) to avoid hanging on unresponsive services.

## Visual Summary

![create html document example showing the generated HTML with JSON inside a pre tag](fetchResult.png "Screenshot of the generated HTML document")

*Alt text:* *create html document example – generated HTML file displaying fetched JSON inside a pre element.*

## Conclusion

You now know how to **create HTML document** programmatically in Java, **fetch JSON JavaScript**, **add script element**, **generate HTML from JSON**, and **convert JSON to pre** for readable output. The whole workflow runs offline, requires only Aspose.HTML, and produces a clean static file you can serve anywhere.

Next, try extending the script to loop over an array of objects, add CSS styling, or write multiple pages using the same technique. You could also replace the `fetch` URL with your own API to turn dynamic data into static snapshots—perfect for SEO‑friendly pre‑rendering.

Happy coding, and feel free to share your experiments in the comments!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}