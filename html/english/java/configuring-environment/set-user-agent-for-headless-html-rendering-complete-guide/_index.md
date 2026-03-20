---
category: general
date: 2026-03-20
description: Set user agent in a sandbox to extract page title with headless HTML
  rendering – learn how to set device DPI and create sandbox instance.
draft: false
keywords:
- set user agent
- extract page title
- set device dpi
- create sandbox instance
- headless html rendering
language: en
og_description: Set user agent in a sandbox, extract page title, and control device
  DPI for reliable headless HTML rendering.
og_title: Set User Agent for Headless HTML Rendering – Complete Guide
tags:
- Java
- Web Scraping
- Headless Rendering
title: Set User Agent for Headless HTML Rendering – Complete Guide
url: /java/configuring-environment/set-user-agent-for-headless-html-rendering-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set User Agent for Headless HTML Rendering – Complete Guide

Ever needed to **set user agent** while scraping a site but weren’t sure how it affects the rendered page? You’re not alone. In many headless scenarios the server decides what HTML to send based on the UA string, so getting it right can be the difference between a blank page and the content you actually need.  

In this tutorial we’ll walk through configuring a sandbox, **creating a sandbox instance**, tweaking the **device DPI**, and finally **extracting the page title** from a **headless HTML rendering** session. No fluff—just a runnable Java example you can drop into your project today.

> **Pro tip:** If you’re already using Aspose.HTML (or a similar library), the steps below map 1‑to‑1 with its API. If you’re on a different stack, think of the sandbox as any headless browser context (Playwright, Selenium, etc.).

## What You’ll Build

- A sandbox with a custom **user‑agent** string.
- DPI‑aware rendering so CSS units (pt, in, cm) behave like a real screen.
- A clean way to **extract the page title** after the page is fully rendered.
- A self‑contained Java class you can run from the command line.

Prerequisites? Just Java 8+ and the Aspose.HTML for Java JAR on your classpath. Nothing else.

---

## Set User Agent and Configure Sandbox

The very first thing you want to do is tell the rendering engine which browser you’re pretending to be. This is done via the `SandboxConfiguration#setUserAgent` method.

```java
import com.aspose.html.Sandbox;
import com.aspose.html.SandboxConfiguration;
import com.aspose.html.HTMLDocument;

/* Step 1: Configure the sandbox – screen size, DPI, and user‑agent */
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
sandboxConfig.setScreenSize(1280, 800);      // width × height in pixels
sandboxConfig.setDeviceDPI(96);              // DPI for CSS unit conversion
sandboxConfig.setUserAgent("AsposeHTML/1.0"); // <-- set user agent
```

Why does this matter? Many sites serve a simplified layout to unknown agents (think “bot”) and hide the data you actually need. By mimicking a real browser you coax the server into returning the full page.

![set user agent configuration](/images/set-user-agent.png "Illustration of set user agent in sandbox configuration")

*Image alt text: set user agent configuration screenshot.*

## Create Sandbox Instance for Headless HTML Rendering

Once the configuration is ready, spin up the sandbox. Think of it as launching a headless Chrome that lives only in memory.

```java
/* Step 2: Create the sandbox using the configuration */
try (Sandbox sandboxInstance = new Sandbox(sandboxConfig)) {
    // The sandbox is now ready for rendering tasks.
    // Anything you do inside this block runs headlessly.
}
```

Using the try‑with‑resources pattern guarantees the sandbox is disposed properly, freeing native resources. If you forget to close it, you might leak memory or file handles—something I’ve seen trip up newcomers.

## Set Device DPI for Accurate CSS Rendering

The `setDeviceDPI` call isn’t just a nice‑to‑have; it directly influences how CSS units like `pt` or `mm` are calculated. If you’re rendering invoices, PDFs, or any layout‑sensitive page, matching the target DPI ensures your screenshots or extracted data look exactly as they would on a real monitor.

You already saw the call in the configuration snippet, but here’s a quick sanity check:

```java
int dpi = sandboxConfig.getDeviceDPI(); // should return 96
System.out.println("Sandbox DPI set to: " + dpi);
```

If you need a higher resolution (e.g., for retina‑style assets), bump the value to `144` or `192`. Just remember to keep the screen size proportional; otherwise the layout may overflow.

## Extract Page Title from Rendered Document

Now that the sandbox is humming, load a page and pull its title. The `HTMLDocument#getTitle` method reads the `<title>` tag *after* the page’s DOM is fully parsed.

```java
/* Step 3: Load a web page inside the sandboxed environment */
HTMLDocument htmlDoc = new HTMLDocument(sandboxInstance, "https://example.com");

/* Step 4: Work with the rendered document – extract its title */
String pageTitle = htmlDoc.getTitle();
System.out.println("Title: " + pageTitle);
```

Running the above against `https://example.com` prints:

```
Title: Example Domain
```

That’s the **extract page title** step in action. If the site uses JavaScript to set the title dynamically, the sandbox will execute the script (provided you enable scripting, which is on by default). If you ever see an empty string, double‑check that the page actually contains a `<title>` element after scripts run.

## Full Working Example

Putting it all together, here’s a complete, ready‑to‑run class. Feel free to copy‑paste into `Main.java` and execute `javac Main.java && java Main`.

```java
import com.aspose.html.Sandbox;
import com.aspose.html.SandboxConfiguration;
import com.aspose.html.HTMLDocument;

/**
 * Demonstrates how to set user agent, configure DPI,
 * create a sandbox instance, and extract the page title
 * using headless HTML rendering.
 */
public class Main {
    public static void main(String[] args) {
        // 1️⃣ Configure sandbox: screen, DPI, and user‑agent
        SandboxConfiguration config = new SandboxConfiguration();
        config.setScreenSize(1280, 800);
        config.setDeviceDPI(96);
        config.setUserAgent("AsposeHTML/1.0"); // <-- set user agent

        // 2️⃣ Create sandbox (auto‑close with try‑with‑resources)
        try (Sandbox sandbox = new Sandbox(config);
             // 3️⃣ Load the page inside the sandbox
             HTMLDocument doc = new HTMLDocument(sandbox, "https://example.com")) {

            // 4️⃣ Extract and print the title
            String title = doc.getTitle();
            System.out.println("Title: " + title);
        } catch (Exception e) {
            // Simple error handling – in real code you might log this
            System.err.println("Rendering failed: " + e.getMessage());
        }
    }
}
```

### Expected Output

```
Title: Example Domain
```

If you swap `https://example.com` for any other URL, you’ll see that page’s title—provided the site doesn’t block headless agents. That’s the whole **headless HTML rendering** pipeline in under 30 lines of Java.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if the site blocks unknown UAs?* | Use a common browser string, e.g., `"Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/119.0 Safari/537.36"`. The sandbox lets you set any arbitrary UA. |
| *Do I need to enable JavaScript?* | It’s on by default. If you turned it off earlier, call `config.setEnableJavaScript(true)`. |
| *How do I capture a screenshot instead of just the title?* | After loading the document, call `htmlDoc.save("page.png", SaveFormat.PNG)`. The DPI you set earlier will affect the image size. |
| *Can I render multiple pages in one sandbox?* | Yes. Re‑use the same `Sandbox` object; just instantiate new `HTMLDocument` objects for each URL. |
| *What about HTTPS certificates?* | The sandbox trusts the default Java keystore. For self‑signed certs, import them into the JVM trust store or disable verification via `config.setIgnoreCertificateErrors(true)`. |

---

## Tips for Production‑Ready Scraping

1. **Rotate User Agents** – Keep a list of popular UA strings and pick one at random per request. This reduces the chance of being flagged.
2. **Respect Robots.txt** – Even though you’re headless, ethical scraping means honoring the site’s crawling policy.
3. **Throttle Requests** – Insert a `Thread.sleep(500)` between calls to avoid hammering the server.
4. **Cache Rendered HTML** – If you need the same page repeatedly, store the HTML on disk and reuse it; rendering is CPU‑intensive.
5. **Monitor Memory** – The sandbox holds native resources. In long‑running jobs, periodically call `System.gc()` or restart the sandbox after a batch of URLs.

---

## Conclusion

You now know how to **set user agent** for reliable **headless HTML rendering**, configure the **device DPI**, **create a sandbox instance**, and **extract page title** in a clean Java workflow. The complete example above runs out of the box, prints the title, and leaves room for extensions like screenshots or PDF conversion.

Next, try swapping out the URL with a site that serves different content based on the UA string, or experiment with higher DPI values to see how CSS layouts shift. You might also explore the library’s `HTMLDocument.save` overloads to generate PDFs—another handy way to archive rendered pages.

Happy coding, and may your scrapers stay undetected!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}