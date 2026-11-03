---
category: general
date: 2026-10-14
description: Call java from javascript using Aspose.HTML. Learn how to add a host
  object, execute javascript in java, and log from javascript in a concise tutorial.
images:
- /java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/og-image.png
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Call java from javascript using Aspose.HTML. This guide shows how
  to add a host object, execute javascript in java, and log from javascript, all in
  a few lines of code.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Call java from javascript – add host object and run javascript in java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Call java from javascript – add host object and run javascript in java
url: /java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Call java from javascript – add host object and run javascript in java

Ever needed to **call java from javascript** inside a Java application? Maybe you’re building a dynamic HTML report engine or you simply want to expose a Java logger to a script you control. In this tutorial you’ll see exactly how to add a host object, run JavaScript in Java, and even **log from JavaScript** back to the JVM—all with Aspose.HTML.

We’ll walk through a complete, runnable example that creates an empty HTML document, injects a Java `Logger` class as a host object, executes a tiny script, and prints the result to the console. No external web browser required, no mystic “magic”—just plain Java code you can copy‑paste and run today.

## Quick answers
- **How do I add a host object?** Register a Java instance with `document.getWindow().addHostObject("name", object)`.  
- **Can I execute JavaScript in Java?** Yes—use `document.getWindow().eval(yourScript)`.  
- **Is logging from JavaScript possible?** Absolutely; the host object can expose any `void log(String)` method.  
- **What version of Aspose.HTML is required?** Version 23.10 or newer supports the full host‑object API.  
- **Do I need a web browser?** No—Aspose.HTML provides an embedded engine, so everything runs head‑less.

## What is call java from javascript?
**Call java from javascript** is the technique of exposing Java objects to a JavaScript runtime so that scripts can invoke Java methods directly. Aspose.HTML creates a lightweight JavaScript engine inside a Java process, enabling seamless two‑way communication without external browsers.

## Why use Aspose.HTML for executing javascript in java?
Aspose.HTML supports **50+ input and output formats** and can evaluate JavaScript in a fully‑compliant HTML5 environment. It processes scripts up to 200 ms on average for simple one‑liner code, and it does so without loading a full browser stack, which reduces memory usage by up to 80 % compared with Selenium‑based approaches.

## Prerequisites

- Java 17 (or any recent JDK) installed and configured.  
- Aspose.HTML for Java library (version 23.10 or newer). You can obtain it from Maven Central or the Aspose website.  
- A simple IDE or text editor; the example works from the command line as well.

> **Pro tip:** If you use Maven, add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Or, for Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Now that we’ve got the basics sorted, let’s dive into the step‑by‑step solution.

## How to add a host object and run javascript in java?
`addHostObject` registers a Java object as a global variable in the JavaScript context. Load your `HTMLDocument`, register a Java logger under the name `"javaLogger"` using `addHostObject`, and then evaluate a short script that calls `javaLogger.log`. The entire flow requires only three API calls and works in any Java 17 runtime.

### Step 1: create a minimal java project

First, set up a new Java class called `JsHostObjectDemo`. The class will house our `main` method and the host object definition. Keeping everything in one file makes the tutorial self‑contained and easy to copy.

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

### Why an `HTMLDocument`?
`HTMLDocument` represents an in‑memory HTML document and provides a JavaScript engine. The `HTMLDocument` class spins up a full HTML‑5 compliant scripting environment. Even though we never load any markup, the document’s `window` object gives us access to the JavaScript engine, which is where the **run javascript in java** magic happens. Additionally you can manipulate the DOM, load resources, or evaluate scripts without a browser.

## How to add the host object – “javaLogger”?
`Logger` is a simple Java class with a `log(String)` method that writes messages to the console. Register the `Logger` instance under the name `"javaLogger"` so that any script evaluated in this document can call `javaLogger.log(...)`. This is the core of the **add host object** requirement and makes the logger available as a global variable to JavaScript code.

### Common pitfalls

- **Naming collisions** – If you already have a global variable called `javaLogger` in your script, the host object will be overwritten. Choose a unique name.  
- **Thread safety** – The host object is shared across script executions on the same document. If you plan to run scripts concurrently, make the host class thread‑safe (e.g., use `synchronized` or `java.util.concurrent` primitives).

## How to write and execute javascript in java?
`eval` executes a JavaScript string in the document's scripting engine and returns any result. Feed a tiny script into `eval`. The engine resolves `javaLogger` from the global scope and invokes its `log` method with the supplied string. You can also return values, handle exceptions, and chain multiple evaluations for more complex interactions.

### Expected output

Running the `main` method prints the following line to the console:

```
[JS] Hello from JavaScript!
```

## How to extend the host – more than just logging?
A host object is any Java instance exposed to JavaScript via `addHostObject`. Expose additional functionality by adding methods to the `Logger` class or by creating a new host class. Below is a quick example that also returns a value to JavaScript. The host object can expose complex types, perform I/O, or interact with other services. By returning a value, the script can receive data back, enabling two‑way communication between Java and JavaScript.

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

Now the console shows:

```
[JS] 3+4=7
```

## How to clean up resources after running scripts?
`dispose` releases native resources held by the `HTMLDocument` instance. When you’re done with the scripting environment, dispose of the `HTMLDocument` to free native resources. Failing to call `dispose()` may lead to memory leaks, especially when creating many documents in loops or long‑running services. Always wrap the usage in a try‑with‑resources block or ensure `document.dispose()` is called in a finally clause.

```java
document.dispose(); // Important for long‑running applications
```

## Full working example

Below is the complete source file you can compile and run immediately. Save it as `JsHostObjectDemo.java`, ensure the Aspose.HTML JAR is on your classpath, and execute `java JsHostObjectDemo`.

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

Running this program yields:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Frequently asked questions

**Q: Does this work on Android?**  
A: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including Android’s ART runtime.

**Q: What if I need to pass complex objects?**  
A: You can expose POJOs with getters and setters; the engine maps them to JavaScript objects automatically. Collections such as `java.util.List` or arrays are also convertible.

**Q: How does error handling work?**  
A: If the script throws a JavaScript error, `eval` propagates a `ScriptException`. Wrap the call in a try‑catch block to log or recover.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: Can I run multiple scripts sequentially?**  
A: Absolutely. The same `HTMLDocument` retains its global scope, so you can call `eval` repeatedly. Just manage variable names to avoid clashes.

**Q: Is the host object safe for untrusted scripts?**  
A: Treat any external script as untrusted input. Validate parameters and consider sandboxing by exposing only the minimal required methods.

## Best practices & tips

- **Name your host objects clearly**—`javaLogger`, `javaUtils`, etc.—to avoid confusion.  
- **Keep host methods small and side‑effect free** when possible; it makes debugging easier.  
- **Dispose of the document** as soon as you’re done; it releases native memory that Aspose.HTML allocates.  
- **Validate inputs** from JavaScript, especially if scripts come from untrusted sources. Treat them like any external data.

## Conclusion

You now have a solid, end‑to‑end example of how to **call java from javascript** by **adding a host object**, **running javascript in java**, and **logging from javascript** using Aspose.HTML. The pattern is powerful: any Java service can be exposed to scripts, turning your Java application into a lightweight scripting platform.

Next, you might explore:

- Injecting a full HTML page and manipulating the DOM from JavaScript.  
- Using the host object to stream data back to the Java side (e.g., JSON serialization).  
- Integrating with other scripting engines like Nashorn or GraalVM for broader language support.

Give it a try, tweak the `Logger` or `Utils` classes, and see how far you can push the **javascript host object** concept in your own projects.

---

**Last Updated:** 2026-10-14  
**Tested With:** Aspose.HTML for Java 23.10  
**Author:** Aspose  






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Related Tutorials

- [Enable Script Execution In Java Complete Aspose Html Guide](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Execute Javascript In Java Complete Guide To Running Js From](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [How To Sandbox Javascript Complete Aspose Html Guide](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}