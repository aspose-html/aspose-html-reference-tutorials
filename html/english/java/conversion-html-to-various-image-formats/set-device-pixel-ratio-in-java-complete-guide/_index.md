---
category: general
date: 2026-02-22
description: Set device pixel ratio in Java with Aspose.HTML sandbox. Learn how to
  set custom user agent, get page title java, and convert html to png in one tutorial.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: en
og_description: Set device pixel ratio in Java using Aspose.HTML sandbox. This tutorial
  shows how to set custom user agent, retrieve page title java, and convert html to
  png.
og_title: Set Device Pixel Ratio in Java – Complete Guide
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Set Device Pixel Ratio in Java – Complete Guide
url: /java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set Device Pixel Ratio in Java – Complete Guide

Ever wondered how to **set device pixel ratio** when rendering a web page from Java? You’re not the only one. Many developers need to emulate high‑DPI mobile screens so that screenshots look crisp, especially when they later **save html as image** for reports or marketing assets. In this tutorial we’ll walk through a hands‑on example that does exactly that—while also showing you how to **set custom user agent**, **get page title java**, and **convert html to png** using Aspose.HTML.

We’ll start with a brief overview of the sandbox API, then dive into each configuration step, and finally produce a PNG file that mirrors a real iPhone display. By the end, you’ll have a reusable snippet you can drop into any Java project. No external tools required, just plain Java and Aspose.HTML 7.x (or newer).

---

## Prerequisites

- Java 17 or later (the code compiles with earlier versions but 17 is recommended).
- Aspose.HTML for Java library (download from the official Aspose site; Maven coordinates: `com.aspose:aspose-html:23.10`).
- An IDE or text editor of your choice (IntelliJ IDEA, VS Code, Eclipse… all work).
- Internet access for the demo URL (`https://example.com/responsive.html`), or replace it with any public HTML page you own.

> **Pro tip:** If you’re behind a proxy, configure the JVM’s `http.proxyHost` and `http.proxyPort` system properties before running the code.

---

## Step 1: Set Device Pixel Ratio and Other Sandbox Options

The first thing we need is a **SandboxOptions** instance where we define the virtual screen size and the *device pixel ratio* (DPR). Think of DPR as the factor that tells the browser how many physical pixels correspond to one CSS pixel. On a Retina iPhone the DPR is typically **2.0**, which is why we’ll use that value.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Why this matters:** Without setting the correct DPR, the rendered image will appear blurry or oversized because the rasterizer assumes a 1:1 pixel mapping.

---

## Step 2: Set Custom User Agent

Websites often serve different markup based on the **User‑Agent** header. To make sure our page behaves like it would on a real iPhone, we inject a custom string that mimics Safari on iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Edge case:** Some sites inspect the `Accept-Language` header as well. If you notice missing translations, add `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

---

## Step 3: Load the Page Inside the Sandbox and Get the Title

Now we spin up the sandbox with the options we just defined. The **Sandbox** object isolates the rendering process, ensuring our DPR and user‑agent settings are honored.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Once the page loads, retrieving the title is as simple as calling `getTitle()`. This satisfies the **get page title java** requirement.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Expected console output**

```
Title: Responsive Demo – Mobile View
```

If the title is empty, double‑check the URL or make sure the page isn’t blocked by CORS policies.

---

## Step 4: Convert HTML to PNG and Save HTML as Image

Aspose.HTML lets you render the DOM directly to an image file. Because we already set the DPR to 2.0, the resulting PNG will have double the pixel density, yielding a crisp screenshot.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

The `save` method automatically detects the file extension and chooses the appropriate renderer. If you need a different format (JPEG, BMP), just change the file name accordingly.

> **What if you need a specific image size?**  
> Use `ImageSaveOptions` to control width, height, and background color:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

---

## Full Working Example

Below is the complete, ready‑to‑run program that ties all the steps together. Copy‑paste it into a `SandboxDemo.java` file, add the Aspose.HTML dependency, and execute `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

Running the program produces two PNG files:

| File | Description |
|------|-------------|
| `mobile_view.png` | Default rendering using the configured DPR. |
| `mobile_view_custom.png` | Rendering with explicit width/height (useful for fixed‑size assets). |

You can open either file in any image viewer to verify the high‑resolution output.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **What if the page contains JavaScript that modifies the DOM after load?** | Aspose.HTML executes scripts by default. If you need a static snapshot before script execution, set `sandboxOptions.setEnableJavaScript(false)`. |
| **Can I render a page that requires authentication?** | Yes. Use `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` or inject cookies via `sandboxOptions.getCookies().add(...)`. |
| **Is the DPR limited to 2.0?** | No. You can set any positive double (e.g., 3.0 for ultra‑high‑DPI devices). Just remember that larger DPR means larger image files. |
| **How do I handle pages with large assets (images, fonts)?** | Increase the sandbox’s memory limit with `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (bytes). This prevents out‑of‑memory errors on heavy pages. |
| **Do I need to close the sandbox manually?** | The `Sandbox` implements `AutoCloseable`. Wrap it in a try‑with‑resources block for automatic cleanup. |

---

## Conclusion

We’ve shown how to **set device pixel ratio** in a Java sandbox, **set custom user agent**, **get page title java**, and **convert html to png** (effectively **save html as image**) using Aspose.HTML. The complete example demonstrates a practical workflow you can adapt for automated screenshot generation, visual regression testing, or any scenario where a pixel‑perfect representation of a web page is required.

Feel free to experiment—change the DPR to 3.0, swap the user‑agent for an Android string, or point the URL at a local HTML file. The same pattern works for PDFs, SVGs, or even multi‑page rendering.

If you found this guide helpful, consider exploring related topics such as **PDF generation with Aspose.HTML**, **headless Chrome alternatives**, or **batch rendering of multiple URLs**. Happy coding, and may your screenshots always be razor‑sharp! 

![set device pixel ratio in Java sandbox](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}