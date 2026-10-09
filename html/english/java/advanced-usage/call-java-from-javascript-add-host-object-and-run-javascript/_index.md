---
category: general
date: 2026-03-14
description: Learn how to call Java from JavaScript using Aspose.HTML. This guide
  shows how to add host object, run JavaScript in Java, and log from JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: en
og_description: Call Java from JavaScript using Aspose.HTML. Add host object, run
  JavaScript in Java, and log from JavaScript in a single tutorial.
og_title: Call Java from JavaScript – Complete Guide with Host Object
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Call Java from JavaScript – Add Host Object and Run JavaScript in Java
url: /java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Call Java from JavaScript – Add Host Object and Run JavaScript in Java

Ever needed to **call Java from JavaScript** inside a Java application? Maybe you’re building a dynamic HTML report engine or you simply want to expose a Java logger to a script you control. In this tutorial you’ll see exactly how to add a host object, run JavaScript in Java, and even **log from JavaScript** back to the JVM—all with Aspose.HTML.

We’ll walk through a complete, runnable example that creates an empty HTML document, injects a Java `Logger` class as a host object, executes a tiny script, and prints the result to the console. No external web browser required, no mystic “magic”—just plain Java code you can copy‑paste and run today.

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

## Step 1: Create a Minimal Java Project

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

Aspose.HTML’s `HTMLDocument` class spins up a full HTML‑5 compliant scripting environment. Even though we never load any markup, the document’s `window` object gives us access to the JavaScript engine, which is where the **run JavaScript in Java** magic happens.

## Step 2: Add the Host Object – “javaLogger”

The line

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

does the heavy lifting for the **add host object** requirement. By registering the `Logger` instance under the name `"javaLogger"`, any script evaluated in this document can call `javaLogger.log(...)`. This is the core of the **javascript host object** concept: a bridge that lets JavaScript reach into the JVM.

### Common Pitfalls

- **Naming collisions** – If you already have a global variable called `javaLogger` in your script, the host object will be overwritten. Choose a unique name.
- **Thread safety** – The host object is shared across script executions on the same document. If you plan to run scripts concurrently, make the host class thread‑safe (e.g., use `synchronized` or `java.util.concurrent` primitives).

## Step 3: Write and Execute JavaScript

The script we feed into `eval` is deliberately tiny:

```javascript
javaLogger.log('Hello from JavaScript!');
```

When `document.getWindow().eval(script)` runs, the engine looks up `javaLogger` in its global scope, finds the Java object we added, and invokes its `log` method with the supplied string.

### Expected Output

Running the `main` method prints the following line to the console:

```
[JS] Hello from JavaScript!
```

That tiny line proves we have successfully **call java from javascript**, and the **log from javascript** appears exactly where a normal Java `System.out` message would.

## Step 4: Extending the Host – More Than Just Logging

If you need to expose additional functionality (e.g., file access, database queries), simply add more methods to the `Logger` class—or create a brand‑new host class. Here’s a quick example that also returns a value:

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

This demonstrates the flexibility of the **javascript host object** pattern: you can expose any Java API you need, as long as the data types are convertible between Java and JavaScript (primitives, strings, arrays, etc.).

## Step 5: Clean Up Resources

When you’re done with the scripting environment, dispose of the `HTMLDocument` to free native resources:

```java
document.dispose(); // Important for long‑running applications
```

Skipping disposal can lead to memory leaks, especially if you create many documents in a loop.

## Full Working Example

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

That’s the entire **call java from javascript** workflow in a handful of lines.

## Frequently Asked Questions

### Does this work on Android?

Aspose.HTML is a pure‑Java library, so it runs on any JVM, including Android’s Dalvik/ART. Just bundle the JAR and you’ll have the same host‑object capabilities.

### What if I need to pass complex objects?

You can expose POJOs (plain old Java objects) that contain fields, getters, and setters. The engine will map them to JavaScript objects automatically. For collections, use `java.util.List` or arrays—both are convertible.

### How does error handling work?

If the script throws a JavaScript error, `eval` will propagate a `ScriptException`. Wrap the call in a try‑catch block to log or recover:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Can I run multiple scripts sequentially?

Absolutely. The same `HTMLDocument` instance retains its global scope, so you can call `eval` repeatedly. Just be mindful of variable name clashes between scripts.

## Best Practices & Tips

- **Name your host objects clearly**—`javaLogger`, `javaUtils`, etc.—to avoid confusion.
- **Keep host methods small and side‑effect free** when possible; it makes debugging easier.
- **Dispose of the document** as soon as you’re done; it releases native memory that Aspose.HTML allocates.
- **Validate inputs** from JavaScript, especially if scripts come from untrusted sources. Treat them like any external data.

## Conclusion

You now have a solid, end‑to‑end example of how to **call java from javascript** by **adding a host object**, **running JavaScript in Java**, and **logging from JavaScript** using Aspose.HTML. The pattern is powerful: any Java service can be exposed to scripts, turning your Java application into a lightweight scripting platform.

Next, you might explore:

- Injecting a full HTML page and manipulating the DOM from JavaScript.
- Using the host object to stream data back to the Java side (e.g., JSON serialization).
- Integrating with other scripting engines like Nashorn or GraalVM for broader language support.

Give it a try, tweak the `Logger` or `Utils` classes, and see how far you can push the **javascript host object** concept in your own projects

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}