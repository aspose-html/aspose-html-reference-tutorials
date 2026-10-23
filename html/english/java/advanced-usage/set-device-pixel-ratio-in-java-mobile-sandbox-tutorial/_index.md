---
category: general
date: 2026-10-19
description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how to
  set screen width height and get page title java with a complete, runnable example.
draft: false
images:
- /java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/og-image.png
keywords:
- get page title java
- device pixel ratio java
- create virtual device java
- set screen width height
language: en
lastmod: 2026-10-19
og_description: Get page title java with Aspose.HTML sandbox. This guide shows you
  how to set screen width height and device pixel ratio in Java in a few easy steps.
og_image_alt: 'Developer guide: set device pixel ratio in Java using Aspose.HTML sandbox'
og_title: Get page title java – set device pixel ratio in Java sandbox tutorial
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how
    to set screen width height and get page title java with a complete, runnable example.
  headline: Get page title java – set device pixel ratio in Java sandbox tutorial
  type: TechArticle
- questions:
  - answer: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio`
      value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing
      its options is not supported.
    question: Can I change the pixel ratio at runtime?
  - answer: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run
      the same load‑and‑title logic for each.
    question: What if I need to test multiple devices?
  - answer: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the
      JVM’s keystore or, for testing only, disable verification (not recommended for
      production).
    question: Does this work with HTTPS sites that have self‑signed certificates?
  - answer: The `HTMLDocument` API provides `save` methods that can export the rendered
      page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after
      loading.
    question: How do I capture a screenshot instead of just the title?
  - answer: Each `Sandbox` instance is isolated, but you should avoid sharing a single
      instance across multiple threads without synchronization.
    question: Is the sandbox thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- mobile emulation
title: Get page title java – set device pixel ratio in Java sandbox tutorial
url: /java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get page title java – set device pixel ratio in Java sandbox tutorial

Ever needed to **set device pixel ratio** while testing a responsive site in Java? You're not the only one. Many developers hit a wall when the page looks perfect on desktop but breaks on high‑DPI phones. The good news? With Aspose.HTML’s sandbox you can emulate an iPhone X (or any device) right from your Java code—no browser required.

In this guide we’ll walk through **how to set screen width height**, configure the **device pixel ratio**, and finally **get page title java** to verify everything rendered correctly. By the end you’ll have a self‑contained program you can drop into any project and start testing mobile layouts instantly.

## Quick answers
- **How do I set device pixel ratio in Java?** Use `SandboxOptions.setDevicePixelRatio(double)` before creating the sandbox.  
- **What method returns the page title?** Call `htmlDocument.getTitle()` on the loaded `HTMLDocument`.  
- **Can I emulate other devices?** Yes—create a new `SandboxOptions` with the desired width, height, and pixel ratio.  
- **Do I need a browser driver?** No, Aspose.HTML’s sandbox is head‑less and runs purely in Java.  
- **Which Aspose.HTML version is required?** Version 23.7 or later supports all mobile‑emulation features.

## What is get page title java?
`get page title java` is the operation of retrieving the `<title>` element from an HTML document using Java code. It lets you confirm that a page loaded in a virtual device context rendered the expected title. Retrieving the title is a common step in automated validation to ensure the correct page was loaded after applying device emulation parameters.

## Why use Aspose.HTML sandbox for mobile emulation?
Aspose.HTML supports **30+** input and output formats—including HTML, CSS, SVG, and PDF—and can render pages without launching a full browser. Its sandbox processes multi‑hundred‑page sites while keeping memory usage under 200 MB, making it ideal for CI pipelines.

## Prerequisites

- Java 8 or newer (the code compiles with JDK 11 as well)  
- Aspose.HTML for Java library (version 23.7 or later) – you can pull it from Maven Central  
- An IDE or a simple `javac` command‑line setup  
- Internet access for the demo URL (`https://responsive.example.com`)

No extra frameworks, no Selenium, just pure Java and Aspose.HTML.

## How to set screen width height and device pixel ratio in Java

The `SandboxOptions` class lets you specify the virtual device’s screen dimensions and pixel density. To emulate a specific mobile device you must configure the sandbox with the desired screen width, height, and device pixel ratio. By creating a `SandboxOptions` object and setting these properties, the rendering engine will treat the page as if it were displayed on that device, ensuring CSS media queries and image scaling behave correctly.

Create a `SandboxOptions` instance, set the width to **375**, height to **812**, and device pixel ratio to **3.0**. Then pass those options to a new `Sandbox`. This fully configures the virtual device before any page is loaded.

The `SandboxOptions` class defines the virtual device’s screen size and pixel density. It is the entry point for any mobile‑emulation scenario.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Why this matters:**  
> The `setDevicePixelRatio` call scales everything—from images to font rendering—so the page thinks it’s on a real phone. If you skip it, the layout may fall back to desktop‑style CSS media queries, defeating the purpose of mobile testing.

## How to create the sandbox instance

The `Sandbox` class represents a headless browser environment that renders HTML using the previously defined options. After configuring `SandboxOptions`, instantiate a `Sandbox` with those options to obtain an isolated rendering context. This sandbox acts like a lightweight browser, applying the screen size and pixel density you specified, and can be reused for multiple page loads while keeping the environment clean.

Instantiate a `Sandbox` with the previously configured `SandboxOptions`. The sandbox behaves like a tiny, headless browser that respects the dimensions and pixel ratio you defined.

The `Sandbox` object is Aspose.HTML’s isolated rendering engine that runs without a UI. It guarantees that each test runs in a clean environment.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Pro tip:** You can reuse the same `Sandbox` object for multiple page loads; just change the URL and the sandbox will keep the same device characteristics.

## How to load the page inside the sandbox

The `HTMLDocument` class represents a parsed HTML file in memory, providing DOM access and rendering capabilities. With the sandbox ready, create an `HTMLDocument` by passing the target URL and the sandbox instance. This loads and renders the page using the virtual device settings, allowing you to interact with the DOM or extract information such as the title.

Create an `HTMLDocument` by passing the target URL and the `Sandbox` instance. This forces the document to render using the virtual device you set earlier.

The `HTMLDocument` class represents a parsed HTML file in memory and provides methods for DOM manipulation and metadata extraction.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

If the URL is unreachable or the page contains errors, Aspose.HTML will throw an exception. For production code you’d wrap this in a `try‑catch` and log the failure, but the tutorial keeps it straightforward.

## How to verify with get page title java

The `getTitle()` method returns the content of the HTML document’s `<title>` element as a plain string. Reading the title is the quickest sanity check. After loading the page, call `htmlDocument.getTitle()` to retrieve the title text. This simple check confirms that the page was rendered correctly under the emulated device settings and provides a quick way to validate navigation or content changes in automated tests.

Call `htmlDocument.getTitle()` on the loaded document and print the result. If the sandbox correctly applied the **device pixel ratio**, the title will match what you’d see on a real iPhone X.

The `getTitle()` method returns the content of the `<title>` element as a plain string, allowing you to validate rendering without visual inspection.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Expected output (example):**

```
Title under sandbox: Responsive Demo – Mobile View
```

If you see the title printed, you’ve successfully **set device pixel ratio**, **set screen width height**, and **got the page title** using Java.

## Full, runnable example

Below is the complete program you can copy‑paste into a file named `SandboxDemo.java`. Make sure the Aspose.HTML JARs are on your classpath (`-cp` flag) before you compile.

The `SandboxDemo` class ties together all previous steps into a single, executable example.

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

## Frequently asked questions & edge cases

**Q: Can I change the pixel ratio at runtime?**  
A: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio` value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing its options is not supported.

**Q: What if I need to test multiple devices?**  
A: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run the same load‑and‑title logic for each.

**Q: Does this work with HTTPS sites that have self‑signed certificates?**  
A: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the JVM’s keystore or, for testing only, disable verification (not recommended for production).

**Q: How do I capture a screenshot instead of just the title?**  
A: The `HTMLDocument` API provides `save` methods that can export the rendered page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after loading.

**Q: Is the sandbox thread‑safe?**  
A: Each `Sandbox` instance is isolated, but you should avoid sharing a single instance across multiple threads without synchronization.

## Visual overview

![Diagram showing set device pixel ratio in mobile sandbox](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

[Diagram showing set device pixel ratio in mobile sandbox](https://example.com/images/sandbox-diagram.png "set device pixel ratio diagram")

*The illustration above maps the flow from configuring `SandboxOptions` (including **set screen width height** and **set device pixel ratio**) to loading a URL and extracting the title.*

## Conclusion

You now know **how to set device pixel ratio** in Java, how to **set screen width height** for accurate mobile emulation, and how to **get page title java** to confirm the rendering succeeded. This compact workflow eliminates the need for heavyweight browsers during automated UI testing and fits neatly into CI pipelines.

Ready for the next step? Try exporting the rendered page as an image, or experiment with CSS media‑query debugging by toggling the `devicePixelRatio` between 1.0 and 3.0. You might also explore Aspose.HTML’s PDF conversion features to capture a printable version of the mobile view.

Happy coding, and may your mobile layouts always look crisp—no matter the pixel density!

---

**Last updated:** 2026-10-19  
**Tested with:** Aspose.HTML 23.7 for Java  
**Author:** Aspose

## Related Tutorials

- [Get Html Title Java Render Page In Sandbox With Screen Width](/html/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/)
- [Create Aspose Html Sandbox Complete Java Guide](/html/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/)
- [Set Device Pixel Ratio In Java Complete Guide](/html/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}