---
category: general
date: 2026-05-31
description: Disable external images when you render webpage to PNG in Java using
  Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: en
og_description: Disable external images when rendering a webpage to PNG in Java. This
  step‑by‑step guide shows how to load a webpage in sandbox and save HTML document
  as PNG.
og_title: Disable External Images While Rendering Webpage to PNG in Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Disable External Images While Rendering Webpage to PNG in Java
url: /java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Disable External Images While Rendering Webpage to PNG in Java

Ever needed to **disable external images** when you render a webpage to PNG in Java? Maybe you’re building a thumbnail service that must stay isolated from the public internet, or you simply want to guarantee that no third‑party image leaks during conversion. Either way, you’ve landed in the right spot.

In this tutorial we’ll walk through loading a web page in a sandbox, turning off external image fetching, and finally saving the HTML document as a PNG file—all with Aspose.HTML for Java. By the end you’ll have a ready‑to‑run example, plus a handful of practical tips to avoid the usual pitfalls.

## What You’ll Learn

- **How to render HTML to image Java** using Aspose.HTML’s `Converter`.
- The exact steps to **load webpage in sandbox** with a custom viewport and DPI.
- The configuration needed to **disable external images** while still rendering the page.
- How to **save HTML document as PNG** (or any other supported format) on disk.
- Edge‑case handling, performance hints, and troubleshooting advice.

### Prerequisites

- Java 8 or newer installed (the code works with JDK 11+ as well).
- Maven or Gradle to pull the Aspose.HTML for Java library.
- Basic familiarity with Java syntax and exception handling.
- An internet connection for the initial page load (unless you serve the HTML locally).

> **Pro tip:** If you’re working behind a corporate proxy, set the JVM `http.proxyHost` and `http.proxyPort` properties before running the example.

---

## Step 1: Set Up Your Project and Add Aspose.HTML

First things first—add the Aspose.HTML dependency. If you’re using Maven, drop this into your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

For Gradle, the equivalent is:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Once the library is on the classpath, you’re ready to start coding.

---

## Step 2: **Disable External Images** with a Sandbox Environment

The heart of the solution lies in `DocumentSandbox`. By passing `false` for the *allowExternalImages* flag, we instruct Aspose.HTML to ignore any `<img>` tags that point to URLs outside the sandbox. This is the exact mechanism that **disables external images**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Why this matters:** Without the sandbox, the renderer would attempt to download every image referenced by the page, which can be slow, unreliable, or even a security risk. Setting the flag to `false` guarantees a clean, self‑contained rendering pass.

---

## Step 3: **Load Webpage in Sandbox**  

Now we point Aspose.HTML at the URL we want to capture. The `HTMLDocument` constructor accepts the sandbox instance, automatically applying the restrictions we just defined.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

If the page relies heavily on external scripts for layout, you might notice missing content because we also disabled scripts. In that case, toggle the `allowExternalScripts` flag to `true` while keeping `allowExternalImages` set to `false`.

---

## Step 4: **Render Webpage to PNG**  

With the document loaded, converting it to an image is a one‑liner using `Converter.convert`. The `ImageSaveOptions` object lets you pick the output format; here we choose PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

The resulting file, `sandboxed.png`, contains a snapshot of the page **without any external images**—only the inline SVGs or base64‑encoded graphics remain, if any.

---

## Step 5: Verify the Output and Debug Common Issues

After running the program, open `sandboxed.png` in any image viewer. You should see the page layout, text, and CSS styling, but all `<img src="http://…">` elements will be blank (often rendered as a white rectangle or omitted entirely).

### Typical hiccups and how to fix them

| Symptom | Likely cause | Fix |
|---|---|---|
| Blank page | The target URL blocked the request (e.g., Cloudflare) | Add proper headers to the sandbox’s user‑agent or use a proxy. |
| Missing fonts | Font files are hosted externally | Install the fonts locally or embed them as `@font-face` with data URIs. |
| Layout shift | CSS references external stylesheets that were blocked | Set `allowExternalScripts` to `true` *only* for CSS loading, then re‑run. |
| `java.lang.OutOfMemoryError` | Rendering a very large page at high DPI | Reduce viewport size or DPI, or increase JVM heap (`-Xmx2g`). |

---

## Step 6: Extending the Example – Save as Other Formats

The same code works for JPEG, BMP, or even PDF. Just change the `SaveFormat` enum:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

If you need a PDF instead, replace `ImageSaveOptions` with `PdfSaveOptions` and adjust the file extension accordingly.

---

## Full Working Example (Copy‑Paste Ready)

Below is the **complete, runnable program**. Create a new Java class, paste the code, ensure the `output` directory exists, and run it.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Expected output** (console):

```
PNG image saved to: output/sandboxed.png
```

Open `sandboxed.png` – you’ll see the page rendered **without any external images**.

---

## Frequently Asked Questions

**Q: Can I still display images that are bundled inside the HTML?**  
A: Yes. Inline `data:` URIs or base64‑encoded images are treated as part of the document and will appear in the PNG.

**Q: What if I need to keep some external images but block others?**  
A: The sandbox works as an all‑or‑nothing switch. For fine‑grained control, download the allowed images yourself, embed them as data URIs, and then render.

**Q: Does this approach work on headless servers?**  
A: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a display server or browser engine.

**Q: How does this differ from using Selenium or Puppeteer?**  
A: Selenium drives a real browser, which is heavyweight and harder to sandbox. Aspose.HTML renders HTML directly in memory, giving you deterministic performance and easier security controls like **disable external images**.

---

## Conclusion

You now have a solid, end‑to‑end recipe for **disabling external images while rendering a webpage to PNG in Java**. By leveraging `DocumentSandbox`, you gain tight control over what external resources are permitted, ensuring both security and reproducibility. From here you can experiment with different viewport sizes, DPI settings, or output formats—each tweak opens a new avenue for generating thumbnails, previews, or archival snapshots.

Ready for the next challenge? Try rendering a batch of URLs in parallel, or integrate this logic into a Spring Boot microservice that returns PNGs on demand. The sky’s the limit when you combine Aspose.HTML’s flexibility with Java’s concurrency tools.

Happy coding, and don’t forget to share your success stories in the comments!


## What Should You Learn Next?

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}