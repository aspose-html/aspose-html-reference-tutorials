---
category: general
date: 2026-04-03
description: Learn how to use sandbox in Aspose.HTML Java to set user agent, set size,
  and get viewport size instantly. Full code, explanations, and tips included.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: en
og_description: Learn how to use sandbox in Aspose.HTML Java to set user agent, set
  size, and get viewport size instantly. Complete guide with code and best practices.
og_title: How to Use Sandbox – Set User Agent & Get Viewport Size
tags:
- AsposeHTML
- Java
- Sandbox
title: How to Use Sandbox – Set User Agent & Get Viewport Size
url: /java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use Sandbox – Set User Agent & Get Viewport Size

Ever wondered **how to use sandbox** when rendering HTML with Aspose.HTML for Java? Maybe you’ve hit a wall trying to simulate a specific screen size or need to spoof a user‑agent string so the page behaves like it’s being visited from a mobile browser.  

The good news is that the sandbox API lets you do exactly that, and you can also pull the computed viewport size after the page loads. In this tutorial we’ll walk through creating a sandbox, setting the size, setting a custom user agent, loading a remote page, and finally reading the viewport dimensions. By the end you’ll know **how to set size**, **how to get viewport**, and why these steps matter for reliable headless rendering.

> **Quick win:** you’ll have a runnable Java class that prints something like `Viewport: 1280×800` in seconds.

---

## What You’ll Need

- **Aspose.HTML for Java** version 24.6 or newer (the API we use was introduced in 24.5).  
- A Java 17+ development kit (any recent JDK works).  
- An IDE or a simple text editor—no special plugins required.  
- Internet access if you want to load an external URL such as `https://example.com`.

That’s it. No Maven/Gradle wizardry is mandatory; you can drop the JARs on the classpath manually if you prefer.  

---

## How to Use Sandbox – Overview

The sandbox isolates the rendering engine from the host OS, letting you define a virtual screen (width, height, DPI) and a custom **user agent** string. Think of it as a miniature browser window that lives entirely in memory. When you later ask the `HTMLDocument` for its default view, the engine reports the **viewport size** that it calculated based on the sandbox settings.  

Below is a high‑level flow:

1. **Create** a `DocumentSandbox` and configure width, height, DPI, and user‑agent.  
2. **Load** an `HTMLDocument` inside that sandbox.  
3. **Query** the document’s default view for the viewport size.  

Let’s dive into each step.

---

## Step 1: Create a Sandbox and Set Size

First, we spin up a sandbox and tell it how big the virtual screen should be. This is where you answer the question **how to set size** for a headless render.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Pro tip:** If you’re testing a responsive layout, try a narrow width like `360` to emulate a phone, or a wide one like `1920` for a desktop. The sandbox respects the DPI you set, so a high‑density screen (e.g., 144 DPI) will affect media‑queries that use `device-pixel-ratio`.

---

## Step 2: Set User Agent for the Sandbox

Why bother with a custom **user agent**? Some sites deliver different markup or scripts depending on the reported browser. By calling `setUserAgent` you can trick the page into thinking it’s being visited from Chrome, Firefox, or a mobile device.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Now the page will think it’s rendering on an iPhone. If you need to **set user agent** back to the default, just reuse the earlier “AsposeHTML/24.6 …” string.

---

## Step 3: Load an HTML Document Inside the Sandbox

With the sandbox ready, we can load any URL or local HTML file. The `HTMLDocument` constructor takes the sandbox as a second argument, binding the two together.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

The `try‑with‑resources` block ensures the document is disposed properly, freeing native resources that Aspose.HTML allocates under the hood.

---

## Step 4: Get Viewport Size from the Document

Here’s the moment you’ve been waiting for: retrieving the **viewport size** that the rendering engine computed. This answers **how to get viewport** after the page has been laid out.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

When you run the program, you should see something like:

```
Viewport: 1280×800
```

If you changed the sandbox dimensions in Step 1, the printed numbers will reflect those new values—perfect for automated tests that verify responsive breakpoints.

---

## Full Working Example

Below is the complete, ready‑to‑run class that puts all the pieces together. Copy‑paste it into a file named `SandboxExample.java`, add the Aspose.HTML JARs to your classpath, and execute `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Expected output** (assuming the sandbox settings above):

```
Viewport: 1280×800
```

If you set a different width/height in the sandbox, the output will change accordingly—exactly what you need when testing responsive designs.

---

## Edge Cases & Common Questions

### What if the page uses `window.innerWidth` instead of CSS media queries?

The sandbox’s virtual screen size influences both CSS layout and JavaScript’s `window.innerWidth/innerHeight`. So **how to get viewport** via JavaScript will return the same numbers you see in the Java console.

### Can I run multiple sandboxes in parallel?

Yes. Each `DocumentSandbox` instance is independent, so you can spin up a thread pool, give each thread its own sandbox with different dimensions, and render dozens of pages concurrently. Just remember to keep the JARs thread‑safe (they are).

### Does the DPI setting affect image scaling?

Absolutely. A higher DPI makes one CSS pixel map to more device pixels, which can cause high‑resolution images to appear sharper. If you’re testing retina‑style assets, try `sandbox.setDeviceDpi(144)`.

### How do I handle HTTPS certificates that are self

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}