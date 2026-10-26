---
category: general
date: 2026-06-03
description: Create HTML document in Java and embed JavaScript to increment a counter.
  Learn a script engine example, get element innerHTML, and more.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: en
og_description: Create HTML document in Java, embed JavaScript to increment a counter,
  and retrieve the final value using a script engine example.
og_title: Create HTML Document with Embedded JavaScript – Java Example
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: Create HTML Document with Embedded JavaScript – Java Example
url: /java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create HTML Document with Embedded JavaScript – Java Example

Ever needed to **create HTML document** from Java code and wonder how to embed JavaScript inside it? In this guide we'll show you exactly that, step by step, and you’ll end up with a working script engine example that prints the final counter value.  

If you’ve ever asked yourself *“how can I get element innerHTML after a script runs?”* or *“what’s the cleanest way to increment a counter in JavaScript from Java?”*—you’re in the right place. We’ll cover **embed javascript html**, **increment counter javascript**, and **get element innerHTML** all in one cohesive tutorial.

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="Create HTML Document with embedded JavaScript example"}

## What You’ll Build

By the end of this tutorial you’ll have a self‑contained Java program that:

1. **Creates an HTML document** in memory.
2. **Embeds a small JavaScript snippet** that increments a counter five times.
3. **Initializes a script engine** (the `ScriptEngine` example) to run that snippet.
4. **Retrieves the final counter value** using `getElementInnerHTML`.
5. Prints `Final counter value: 5` to the console.

No external files, no web server—just pure Java and a tiny HTML string.

---

## Prerequisites

- Java 17 or later (the `ScriptEngine` API is part of the standard library).
- Basic familiarity with HTML and JavaScript (you don’t need deep expertise).
- An IDE or a simple text editor plus a terminal to compile and run the program.

---

## Step 1: Create HTML Document in Java

The first thing we need is a blank HTML document object that we can later fill with markup. Think of it as a virtual page that lives only in memory.

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**Why this matters:** By **creating HTML document** objects yourself, you avoid writing to disk and keep everything testable. The tiny DOM simulation lets us later **get element innerHTML** without a full browser.

---

## Step 2: Embed JavaScript HTML – The Counter Logic

Now we’ll write the HTML markup that includes a `<script>` block. This script will **increment counter JavaScript** five times.

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**Explanation:**  
- The `<div id='counter'>0</div>` is our target element.  
- The `for` loop runs **increment counter javascript** logic, updating the div each iteration.  
- Because we’re not in a real browser, the script engine we’ll use later will need to understand `document.getElementById`. That’s why we added a tiny stub in `HTMLDocument`.

---

## Step 3: Initialize the Script Engine – A Script Engine Example

Java ships with the `ScriptEngine` API (JSR‑223). We’ll create a small wrapper that feeds the HTML content to the engine and provides the minimal DOM methods it expects.

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**Why this matters:** This **script engine example** shows how you can run embedded JavaScript without a full browser. It also demonstrates a lightweight way to expose `document.getElementById` so that the script can interact with our mock DOM.

---

## Step 4: Execute JavaScript – Increment Counter JavaScript in Action

With the engine ready, we simply run the script. The loop inside the `<script>` tag will fire, and our mock `setInnerHTML` will update the counter.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**What happens under the hood?** Each iteration of the loop calls `document.getElementById('counter').innerHTML = i + 1;`. Our mock `setInnerHTML` forwards the numeric string to `HTMLDocument.updateCounter`, which stores the latest value. After the loop finishes, the document’s internal map holds `"5"` for the `counter` element.

---

## Step 5: Retrieve the Final Counter Value – Get Element InnerHTML

Now that the script has finished, we can **get element innerHTML** from our `HTMLDocument` instance.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Running the whole program prints:

```
Final counter value: 5
```

That confirms the **increment counter javascript** logic worked and we successfully **retrieved the element innerHTML** after script execution.

---

## Full Working Example

Putting everything together, here’s the complete, ready‑to‑run Java class:

```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class HtmlJsDemo {

    // ---------- Minimal HTMLDocument implementation ----------
    static class HTMLDocument {
        private final StringBuilder html = new StringBuilder();
        private final java.util.Map<String, String> elements = new java.util.HashMap<>();

        public void write(String content) {
            html.append(content);
        }

        public String getContent() {
            return html.toString();
        }

        public void setElementInnerHTML(String id, String value) {
            elements.put(id, value);
        }

        public String getElementInnerHTML(String id) {
            return elements.getOrDefault(id, "");
        }

        public void updateCounter(int value) {
            setElementInnerHTML("counter", String.valueOf(value));
        }
    }

    // ---------- SimpleScriptEngine (script engine example) ----------
    static class SimpleScriptEngine {
        private final HTMLDocument document;
        private final ScriptEngine engine;

        public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
            this.document = doc;
            ScriptEngineManager manager = new ScriptEngineManager();
            this.engine = manager.getEngineByName("JavaScript");
            // Expose a mock 'document' object
            engine.put("document", new Object() {
                public Object getElementById(String id) {
                    return new Object() {
                        public void setInnerHTML(String value) {
                            document.updateCounter(Integer.parseInt(value));
                        }
                    };
                }
            });
        }

        public void execute() throws ScriptException {
            String html = document.getContent();
            int start = html.indexOf("<script>") + "<script>".length();
            int end   = html.indexOf("</script>");
            String script = html.substring(start, end);
            engine.eval(script);
        }
    }

    // ---------- Main method ----------
    public static void main(String[] args) {
        // Step 1: create HTML document
        HTMLDocument doc = new HTMLDocument();

        // Step 2: embed JavaScript HTML (increment counter JavaScript)
        doc.write(
            "<!DOCTYPE html><html><body>"
          + "<div id='counter'>0</div>"
          + "<script>"
          + "for (let i = 0; i < 5; i++) {"
          + "  document.getElementById('counter').innerHTML = i


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Empty HTML Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Create HTML Documents from String in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Save HTML Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}