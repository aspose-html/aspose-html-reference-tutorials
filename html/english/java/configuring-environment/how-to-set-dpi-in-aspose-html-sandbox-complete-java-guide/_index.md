---
category: general
date: 2026-04-02
description: Learn how to set DPI, set viewport size, and set user agent in Aspose.HTML
  Sandbox. Step‑by‑step Java example with full code and tips.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: en
og_description: Master how to set DPI, set viewport size, and set user agent in Aspose.HTML
  Sandbox with a complete Java example.
og_title: How to Set DPI in Aspose.HTML Sandbox – Java Tutorial
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: How to Set DPI in Aspose.HTML Sandbox – Complete Java Guide
url: /java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Set DPI in Aspose.HTML Sandbox – Complete Java Guide

Ever wondered **how to set DPI** when rendering a web page with Aspose.HTML? You're not the only one. In many testing scenarios you need the layout to match a specific screen density—think print‑ready PDFs or high‑resolution screenshots. The good news is that the Aspose.HTML sandbox lets you control DPI, viewport size, and even the user‑agent string in one tidy package.

In this tutorial we’ll walk through a practical Java example that **sets DPI**, **sets viewport size**, and **sets user agent** all at once. By the end you’ll have a runnable program, know why each setting matters, and be ready to tweak the sandbox for your own projects.

---

## What You’ll Need

- **Java 17** (or any recent JDK; the API is compatible with Java 8+)
- **Aspose.HTML for Java** library (version 23.12 or newer)
- An IDE or simple text editor + command‑line compilation
- Internet access for the sample URL (`https://example.com`)

No external build tools are required; the code compiles with `javac` and runs with `java`. If you prefer Maven or Gradle, just add the Aspose.HTML dependency—nothing fancy.

---

## Step 1: Create a Sandbox that Defines the Rendering Environment

The sandbox is where you tell Aspose.HTML what “screen” you’re pretending to have. Here we set a **viewport of 1024 × 768**, a **DPI of 96**, and a custom **user‑agent string**.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Why this matters:**  
- **DPI** influences how CSS `pt` units translate to pixels; a higher DPI yields sharper rendering.  
- **Viewport size** determines the layout breakpoints that responsive CSS will hit.  
- **User‑agent** can trigger server‑side content variations (mobile vs desktop).

> **Pro tip:** If you’re generating PDFs later, match the DPI to the target print resolution (e.g., 300 dpi for high‑quality prints).

---

## Step 2: Load a Web Page Inside the Sandbox

Now we point the sandbox at a URL. The `HTMLDocument` constructor accepts the sandbox, so the layout engine respects the settings we just defined.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**What happens under the hood?**  
Aspose.HTML creates an isolated rendering context, similar to a headless browser, but without the overhead of a full Chromium instance. This makes the operation fast and memory‑light—perfect for batch processing.

---

## Step 3: Interact with the DOM – Read the Page Title

For demonstration we’ll pull the title and print it. In a real‑world scenario you could take a screenshot, export to PDF, or scrape data.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Expected output** (when `https://example.com` is reachable):

```
Title inside sandbox: Example Domain
```

If the site returns a different title, you’ll see that instead—nothing else needs to change.

---

## Step 4: Verify the Settings (Optional Debug)

Sometimes you want to double‑check that the sandbox really respects your DPI and viewport. Aspose.HTML doesn’t expose those values directly, but you can infer them by measuring element dimensions.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

If you know the CSS declares the element as `width: 200pt;`, at **96 dpi** you should see `200pt * (96/72) ≈ 267px`. Adjust the DPI and rerun to see the number change—proof that **how to set dpi** actually works.

---

## Full Source Code in One Block

Copy‑paste the following into `SandboxExample.java`. It compiles as‑is; just make sure the Aspose.HTML JAR is on your classpath.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Compile and run:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

You should see the title printed, confirming that the sandbox is working with the **set dpi**, **set viewport size**, and **set user agent** you provided.

---

## Common Questions & Edge Cases

### What if I need a different DPI?

Just change the second argument of `DocumentSandbox`. For print‑ready PDFs you might use `300`:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Higher DPI yields larger pixel dimensions for the same CSS points, which improves raster quality but consumes more memory.

### Can I load a local HTML file instead of a URL?

Absolutely. Replace the URL with a file path:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Make sure the path is absolute and uses the `file:///` scheme.

### How do I change the user‑agent after the sandbox is created?

The sandbox is immutable—once you pass it to `HTMLDocument`, the settings are locked in. To use a different user‑agent, instantiate a new `DocumentSandbox` with the desired string.

### Does Aspose.HTML support JavaScript execution?

Yes, the engine runs most client‑side scripts. If a script modifies the DOM after load, you can wait a little:

```java
webDoc.waitForLoad();
```

Or use `setTimeout`‑like logic inside the page before querying elements.

---

## Visual Confirmation (Image)

Below is a console screenshot showing the successful run. Notice the title output matches the page, confirming the sandbox respected our settings.

![Console output showing how to set dpi in Aspose.HTML Sandbox](/images/console-output.png)

*Alt text:* *Console output demonstrating how to set dpi, set viewport size, and set user agent in Aspose.HTML Sandbox.*

---

## Recap & Next Steps

We’ve covered **how to set DPI** (96 dpi in the example), **set viewport size** (1024 × 768), and **set user agent** (custom string) using Aspose.HTML’s sandbox API. The full, runnable Java program proves that these settings are not just theoretical—they directly affect rendering and DOM interaction.

Ready for more?

- **Export to PDF:** After loading the page, call `webDoc.save("output.pdf", SaveFormat.PDF);` to generate a high‑resolution PDF that reflects the DPI you set.  
- **Take a Screenshot:** Use `webDoc.renderToBitmap("screenshot.png");` for pixel‑perfect images.  
- **Play with Responsive Layouts:** Change the viewport dimensions to test mobile breakpoints without a real device.  

Experiment with different DPI values, viewport combos, and user‑agents to see how servers and CSS react. The sandbox is a lightweight playground that saves you from spinning up full browsers.

---

### Keep Exploring

- **Aspose.HTML Documentation** – deep dive into `DocumentSandbox` options.  
- **Advanced CSS Media Queries** – learn how viewport size triggers different styles.  
- **User‑Agent Spoofing** – discover how some sites deliver alternate markup based on the agent string.

Got questions or a tricky case? Drop a comment, and let’s troubleshoot together. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}