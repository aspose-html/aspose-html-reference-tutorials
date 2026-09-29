---
category: general
date: 2026-09-29
description: Set custom user agent in Aspose.HTML for Java and learn how to set virtual
  screen size for accurate HTML rendering.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: en
lastmod: 2026-09-29
og_description: Set custom user agent in Aspose.HTML for Java and learn how to set
  virtual screen size for accurate HTML rendering.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Set custom user agent and screen dimensions in Aspose.HTML for Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Set custom user agent and screen dimensions in Aspose.HTML for Java
url: /java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set custom user agent and screen dimensions in Aspose.HTML for Java

If you need to **set custom user agent** while rendering HTML with Aspose.HTML for Java, this guide shows you exactly how to do it. By configuring a sandbox you also get the ability to **set virtual screen size**, ensuring the layout matches a real browser viewport.

You’ll finish this tutorial with a complete, runnable program that **specifies user agent**, **sets screen width**, and **sets screen height**. No external tools are required—just Aspose.HTML for Java and a Java 8+ runtime.

## What you’ll learn

* How to create a `SandboxConfiguration` to isolate rendering.
* How to **set custom user agent** and why it matters for responsive pages.
* How to **set virtual screen size** (screen width and height) for accurate layout.
* How to load an HTML file in the sandbox and save the processed result.
* Common pitfalls and best‑practice tips for sandboxed rendering.

> **Prerequisites** – You need a valid Aspose.HTML for Java license, Java 8 or newer, and an IDE (IntelliJ IDEA, Eclipse, or VS Code). The example uses a local `input.html` file, but any reachable URL works.

![Sandbox flow diagram](sandbox-flow.png "set custom user agent example in Java")

## Step 1: Create a sandbox configuration (the foundation)

The sandbox isolates the rendering environment from the host JVM, which is essential when you want to **set custom user agent** or change the viewport size.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Why this step?*  
`SandboxConfiguration` holds all rendering options, including **screen dimensions** and **user‑agent** strings. By configuring it before loading the document, you guarantee that the HTML engine respects those settings from the first request.

## Step 2: Set screen dimensions to mimic a real device

Responsive sites often read `window.innerWidth` and `window.innerHeight`. To make the engine think it runs on a 1024 × 768 screen, you **set virtual screen size**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Why this matters* – If you omit **set screen dimensions**, the renderer may default to a tiny viewport, causing CSS media queries to pick the mobile layout. By explicitly **set screen width** and **set screen height**, you control which CSS rules fire.

## Step 3: Specify a custom user‑agent string

Some web pages deliver different content based on the user‑agent header. To **specify user agent** you simply set it on the sandbox configuration:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Why use a custom user agent?*  
A custom string can bypass bot detection, trigger desktop‑only features, or test how a site behaves for a specific browser version. The Aspose engine forwards this value with every HTTP request made while loading external resources (CSS, images, scripts).

## Step 4: Load the HTML document inside the sandbox

Now that the sandbox is fully configured, load the HTML file. The constructor that takes a file path and a `SandboxConfiguration` automatically applies all the settings we defined.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

If you need to load from a remote URL, replace the file path with the URL string—Aspose.HTML will still respect the **set custom user agent** and **screen dimensions**.

## Step 5: Save the processed output

After the document finishes loading, you can save it in any supported format. Here we write a sandboxed HTML file that reflects any DOM changes caused by the custom settings.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

The saved file will contain the same markup, but any scripts that queried `navigator.userAgent` or inspected `window.innerWidth` will now see the values you supplied.

## Full, runnable example

Putting all steps together gives you a self‑contained program you can copy, paste, and run.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Expected output

Running the program creates `sandboxed_output.html`. If you open it in a browser and inspect `navigator.userAgent` via the console, you’ll see **AsposeHTML/1.0**. Likewise, `window.innerWidth` will report **1024**, confirming that **set screen dimensions** worked as intended.

## Common questions & edge‑case handling

| Question | Answer |
|----------|--------|
| **What if the page loads additional resources from a different domain?** | The sandbox forwards the **custom user agent** with every request, but cross‑origin policies still apply. Use `sandboxConfig.setAllowCrossDomain(true)` if you need to relax those restrictions. |
| **Can I change the screen size after the document is loaded?** | No. Screen dimensions are read during the initial layout pass. To render with a different size, create a new `SandboxConfiguration` and reload the document. |
| **Do I need to call `document.close()`?** | The `HTMLDocument` implements `AutoCloseable`. Using a try‑with‑resources block ensures proper cleanup, but explicit `close()` is optional in simple scripts. |
| **How does this differ from setting a user‑agent in an HTTP client?** | Setting the user‑agent on the sandbox affects **all** resource requests made by the HTML engine, not just the initial HTML fetch. This mimics a real browser more closely. |
| **Is the sandbox safe for untrusted HTML?** | Yes. The sandbox isolates file system access and limits network calls according to the configuration, reducing the risk of malicious scripts affecting your host JVM. |

## Pro tips

* **Reuse configurations** – If you render many pages with the same viewport, create a single `SandboxConfiguration` and reuse it to avoid object‑creation overhead.
* **Debug with logging** – Enable Aspose.HTML logging (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) to see which resources were fetched with the custom user‑agent.
* **Combine with CSS media queries** – By adjusting **set screen width** you can test how your responsive design behaves on tablets, phones, or large desktops without opening a real browser.

## Conclusion

You now know how to **set custom user agent** and **set screen dimensions** when rendering HTML with Aspose.HTML for Java. By configuring a sandbox, you isolate the environment, control the viewport, and ensure that external resources see the exact headers you specify. This technique is essential for testing responsive layouts, bypassing bot blocks, or reproducing desktop‑only features in automated pipelines.

Next, you might explore **how to set custom cookies** or **capture rendered screenshots** using Aspose.HTML’s rendering API—both concepts build on the same sandbox configuration pattern you just mastered.

Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [High DPI Rendering in Java – Capture Webpage Screenshots with Custom User Agent](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [How to Load HTML, Set Device DPI & Read Background Color](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Create HTML File Java & Set Up Network Service (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}