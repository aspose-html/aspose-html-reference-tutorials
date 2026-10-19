---
category: general
date: 2026-01-14
description: how to set dpi when converting a URL to PNG. Learn to render HTML to
  PNG, set viewport size, and save HTML as PNG using Aspose.HTML in Java.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: en
og_description: how to set dpi when converting a URL to PNG. Step‑by‑step guide to
  render HTML to PNG, control viewport size, and save HTML as PNG using Aspose.HTML.
og_title: how to set dpi – Render HTML to PNG with AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: how to set dpi – Render HTML to PNG with AsposeHTML
url: /java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to set dpi – Render HTML to PNG with AsposeHTML

Ever wondered **how to set dpi** for a screenshot‑like image generated from a web page? Maybe you need a 300 DPI PNG for print, or a low‑res thumbnail for a mobile app. In either case, the trick is to tell the rendering engine what logical DPI you want, then let it do the heavy lifting.  

In this tutorial we’ll take a live URL, render it to a PNG file, **set the viewport size**, adjust the DPI, and finally **save HTML as PNG**—all with Aspose.HTML for Java. No external browsers, no messy command‑line tools—just clean Java code you can drop into any Maven or Gradle project.

> **Pro tip:** If you’re only after a quick thumbnail, you can keep the DPI at 96 DPI (the default for most screens). For print‑ready assets, bump it up to 300 DPI or higher.

![how to set dpi example](https://example.com/images/how-to-set-dpi.png "how to set dpi example")

## What You’ll Need

- **Java 17** (or any recent JDK).  
- **Aspose.HTML for Java** 24.10 or newer. You can grab it from Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- An internet connection to fetch the target page (the example uses `https://example.com/sample.html`).  
- Write permission to the output folder.

That’s it—no Selenium, no headless Chrome. Aspose.HTML does the rendering in‑process, which means you stay inside the JVM and avoid the overhead of launching a browser.

## Step 1 – Load the HTML Document from a URL

First we create an `HTMLDocument` instance pointing at the page we want to capture. The constructor automatically downloads the HTML, parses it, and prepares the DOM.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Why this matters:* By loading the document directly, you skip the need for a separate HTTP client. Aspose.HTML respects redirects, cookies, and even basic authentication if you embed credentials in the URL.

## Step 2 – Build a Sandbox with Desired DPI and Viewport

A **sandbox** is Aspose.HTML’s way of mimicking a browser environment. Here we tell it to pretend it’s a 1280 × 720 screen and, crucially, we set the **device DPI**. Changing the DPI changes the pixel density of the rendered image without altering the logical size.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Why you might tweak these values:*  
- **Viewport size** controls how CSS media queries (`@media (max-width: …)`) behave.  
- **Device DPI** influences the physical size of the image when printed. A 96 DPI image looks fine on screens; a 300 DPI image retains crispness on paper.  

If you need a square thumbnail, simply change `setViewportSize(500, 500)` and keep the DPI low.

## Step 3 – Choose PNG as the Output Format

Aspose.HTML supports several raster formats (PNG, JPEG, BMP, GIF). PNG is loss‑less, which makes it perfect for screenshots where you want every pixel preserved.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

You can also tweak compression level (`pngOptions.setCompressionLevel(9)`) if you’re concerned about file size.

## Step 4 – Render and Save the Image

Now we tell the document to **save** itself as an image. The `save` method takes a file path and the previously configured options.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

When the program finishes, you’ll find a PNG file at `YOUR_DIRECTORY/sandboxed.png`. Open it—if you set the DPI to 300, the image metadata will reflect that, even though the pixel dimensions remain 1280 × 720.

## Step 5 – Verify the DPI (Optional but Handy)

If you want to double‑check that the DPI was really applied, you can read the PNG metadata with a lightweight library like **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

You should see `300` (or whatever you set) printed to the console. This step isn’t required for rendering, but it’s a quick sanity check, especially when you’re generating assets for a print workflow.

## Common Questions & Edge Cases

### “What if the page uses JavaScript to load content?”

Aspose.HTML executes a **limited subset** of JavaScript. For most static sites it works out‑of‑the‑box. If the page heavily relies on client‑side frameworks (React, Angular, Vue), you might need to pre‑render the page or use a headless browser instead. However, setting DPI works the same way once the DOM is ready.

### “Can I render a PDF instead of PNG?”

Absolutely. Swap `ImageSaveOptions` for `PdfSaveOptions` and change the output extension to `.pdf`. The DPI setting still influences the rasterized appearance of any embedded images.

### “What about high‑resolution screenshots for retina displays?”

Just double the viewport dimensions while keeping the DPI at 96 DPI, or keep the viewport and bump the DPI to 192. The resulting PNG will contain twice as many pixels, giving you that crisp retina feel.

### “Do I need to clean up resources?”

`HTMLDocument` implements `AutoCloseable`. In a production app, wrap it in a try‑with‑resources block:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

That ensures native resources are released promptly.

## Full Working Example (Copy‑Paste Ready)

Below is the complete, ready‑to‑run program. Replace `YOUR_DIRECTORY` with an actual folder on your machine.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Run the class, and you’ll get a PNG that respects the **how to set dpi** setting you specified.

## Conclusion

We’ve walked through **how to set dpi** when you **render HTML to PNG**, covered the **set viewport size** step, and showed you how to **save HTML as PNG** using Aspose.HTML for Java. The key takeaways are:

- Use a **sandbox** to control DPI and viewport.  
- Choose the right **ImageSaveOptions** for lossless output.  
- Verify the DPI metadata if you need to guarantee print quality.  

From here you can experiment with different DPI values, larger viewports, or even batch‑process a list of URLs. Want to convert a whole website into PNG thumbnails? Just loop over an array of URLs and reuse the same sandbox configuration.

Happy rendering, and may your screenshots always be pixel‑perfect!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}