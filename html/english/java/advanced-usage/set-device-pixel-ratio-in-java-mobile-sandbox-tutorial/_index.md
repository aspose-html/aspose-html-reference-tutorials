---
category: general
date: 2026-02-10
description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how to
  set screen width height and get page title java with a complete, runnable example.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: en
og_description: set device pixel ratio in Java with Aspose.HTML sandbox. This guide
  shows you how to set screen width height and get page title java in a few easy steps.
og_title: set device pixel ratio in Java – Mobile Sandbox Tutorial
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: set device pixel ratio in Java – Mobile Sandbox Tutorial
url: /java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device pixel ratio in Java – Mobile Sandbox Tutorial

Ever needed to **set device pixel ratio** while testing a responsive site in Java? You're not the only one. Many developers hit a wall when the page looks perfect on desktop but breaks on high‑DPI phones. The good news? With Aspose.HTML’s sandbox you can emulate an iPhone X (or any device) right from your Java code—no browser required.

In this guide we’ll walk through **how to set screen width height**, configure the **device pixel ratio**, and finally **get page title java** to verify everything rendered correctly. By the end you’ll have a self‑contained program you can drop into any project and start testing mobile layouts instantly.

## Prerequisites

- Java 8 or newer (the code compiles with JDK 11 as well)  
- Aspose.HTML for Java library (version 23.7 or later) – you can pull it from Maven Central  
- An IDE or a simple `javac` command line setup  
- Internet access for the demo URL (`https://responsive.example.com`)

No extra frameworks, no Selenium, just pure Java and Aspose.HTML.

---

## Step 1: Set screen width height and device pixel ratio

The first thing we need is a `SandboxOptions` object that tells the sandbox what “device” we’re pretending to be. Here we’ll use the iPhone X dimensions (375 × 812 CSS pixels) and a **device pixel ratio** of 3.0, which mirrors the high‑DPI retina display.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Why this matters:**  
> The `setDevicePixelRatio` call scales everything—from images to font rendering—so the page thinks it’s on a real phone. If you skip it, the layout may fall back to desktop‑style CSS media queries, defeating the purpose of mobile testing.

---

## Step 2: Create the sandbox instance

Now we turn those options into a live sandbox. Think of the sandbox as a tiny, headless browser that respects the dimensions and pixel ratio we just defined.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Pro tip:** You can reuse the same `Sandbox` object for multiple page loads; just change the URL and the sandbox will keep the same device characteristics.

---

## Step 3: Load the page inside the sandbox

With the sandbox ready, loading a page is as simple as constructing an `HTMLDocument` and passing the sandbox as a second argument. This forces the document to render using the virtual device we set earlier.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

If the URL is unreachable or the page contains errors, Aspose.HTML will throw an exception. For production code you’d probably wrap this in a `try‑catch` and log the failure, but for the tutorial we keep it straightforward.

---

## Step 4: Verify with get page title java

The quickest sanity check is to read the document’s title. If the sandbox correctly applied the **device pixel ratio**, the title will be identical to what you’d see on a real iPhone X.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Expected output (example):**

```
Title under sandbox: Responsive Demo – Mobile View
```

If you see the title printed, you’ve successfully **set device pixel ratio**, **set screen width height**, and **got the page title** using Java.

---

## Full, Runnable Example

Below is the complete program you can copy‑paste into a file named `SandboxDemo.java`. Make sure the Aspose.HTML JARs are on your classpath (`-cp` flag) before you compile.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Compile and run:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

You should see the title printed to the console, confirming that the page rendered with the desired **device pixel ratio**.

---

## Frequently Asked Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **Can I change the pixel ratio at runtime?** | Yes—just create a new `SandboxOptions` with a different `setDevicePixelRatio` value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing its options is not supported. |
| **What if I need to test multiple devices?** | Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run the same load‑and‑title logic for each. |
| **Does this work with HTTPS sites that have self‑signed certificates?** | Aspose.HTML respects Java’s default SSL trust store. Add the cert to the JVM’s keystore or disable verification for testing only (not recommended for production). |
| **How do I capture a screenshot instead of just the title?** | The `HTMLDocument` API provides `save` methods that can export the rendered page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after loading. |
| **Is the sandbox thread‑safe?** | Each `Sandbox` instance is isolated, but you should avoid sharing a single instance across multiple threads without synchronization. |

---

## Visual Overview

![Diagram showing set device pixel ratio in mobile sandbox](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

*The illustration above maps the flow from configuring `SandboxOptions` (including **set screen width height** and **set device pixel ratio**) to loading a URL and extracting the title.*

---

## Conclusion

You now know **how to set device pixel ratio** in Java, how to **set screen width height** for accurate mobile emulation, and how to **get page title java** to confirm the rendering succeeded. This compact workflow eliminates the need for heavyweight browsers during automated UI testing and fits neatly into CI pipelines.

Ready for the next step? Try exporting the rendered page as an image, or experiment with CSS media‑query debugging by toggling the `devicePixelRatio` between 1.0 and 3.0. You might also explore Aspose.HTML’s PDF conversion features to capture a printable version of the mobile view.

Happy coding, and may your mobile layouts always look crisp—no matter the pixel density!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}