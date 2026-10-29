---
category: general
date: 2026-06-07
description: Create PNG from HTML in Java using Aspose.HTML. Learn to render HTML
  to PNG, set user agent Java, and adjust device pixel ratio in just a few steps.
draft: false
keywords:
- create png from html
- render html to png
- set user agent java
- convert html to png
- set device pixel ratio
language: en
og_description: Create PNG from HTML in Java with Aspose.HTML. This tutorial shows
  how to render HTML to PNG, set user agent Java, and set device pixel ratio.
og_title: Create PNG from HTML in Java – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: Create PNG from HTML in Java using Aspose.HTML. Learn to render HTML
    to PNG, set user agent Java, and adjust device pixel ratio in just a few steps.
  headline: Create PNG from HTML in Java – Full Example
  type: TechArticle
- description: Create PNG from HTML in Java using Aspose.HTML. Learn to render HTML
    to PNG, set user agent Java, and adjust device pixel ratio in just a few steps.
  name: Create PNG from HTML in Java – Full Example
  steps:
  - name: Setting the Viewport Width
    text: '```java renderingSandbox.setDeviceWidth(375); // 375 px width – typical
      iPhone size ```'
  - name: Adjusting the Device Pixel Ratio
    text: '```java renderingSandbox.setDevicePixelRatio(2.0); // 2× pixel density
      for retina displays ```'
  - name: Providing a Custom User‑Agent (set user agent java)
    text: '```java renderingSandbox.setUserAgent( "Mozilla/5.0 (iPhone; CPU iPhone
      OS 14_0 like Mac OS X) " + "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0
      Mobile/15E148 Safari/604.1" ); ```'
  - name: Expected Output
    text: 'Open the PNG in any image viewer and you should see:'
  type: HowTo
tags:
- Java
- Aspose.HTML
- Image Conversion
title: Create PNG from HTML in Java – Full Example
url: /java/conversion-html-to-various-image-formats/create-png-from-html-in-java-full-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PNG from HTML in Java – Full Example

Ever wondered how to **create PNG from HTML** directly inside a Java application? Maybe you need a thumbnail for an email preview, or you want to generate social‑media cards on the fly. Either way, **render HTML to PNG** without opening a browser is a handy trick that saves time and resources.

In this guide we’ll walk through a practical, end‑to‑end solution that uses Aspose.HTML for Java. You’ll see how to **set user agent Java**, tweak the **device pixel ratio**, and finally **convert HTML to PNG** with just a handful of lines. No external services, no headless Chrome—just pure Java code you can drop into any project.

## What You’ll Learn

- How to load an HTML page that contains media queries.
- How to create a rendering sandbox that mimics a mobile device.
- How to **set device pixel ratio** and a custom user‑agent string.
- How to **render HTML to PNG** and save the result to disk.
- Tips for troubleshooting common pitfalls (missing fonts, cross‑origin resources, etc.).

Before we dive in, make sure you have:

- Java 17 or newer (the API works with Java 8+, but newer versions give you better performance).
- Aspose.HTML for Java library (you can grab it from Maven Central).
- An IDE or build tool of your choice (IntelliJ IDEA, Maven, Gradle—whatever you prefer).

Ready? Let’s get our hands dirty.

## Step 1: Set Up the Project and Add Aspose.HTML

First, add the Aspose.HTML dependency to your `pom.xml` if you’re using Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- check for the latest version -->
</dependency>
```

Or, for Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Once the library is on the classpath, you’re ready to **create PNG from HTML**.

## Step 2: Load the HTML Document (the starting point for conversion)

The first thing we need is an `HTMLDocument` instance that points to the source HTML. It could be a local file, a URL, or even a string containing raw markup.

```java
// Step 2: Load the HTML document that contains media queries
HTMLDocument htmlDoc = new HTMLDocument("https://YOUR_DOMAIN/responsive.html");
```

> **Why this matters:** Loading the document through Aspose.HTML gives us full control over the rendering pipeline, letting us later inject a sandbox with custom device settings.

## Step 3: Create a Rendering Sandbox to Simulate a Mobile Device

A sandbox is essentially a virtual browser environment. By configuring it, we can **set device pixel ratio** and other parameters that affect how CSS media queries behave.

```java
// Step 3: Create a rendering sandbox that simulates a mobile device
RenderingSandbox renderingSandbox = new RenderingSandbox();
```

### Setting the Viewport Width

```java
renderingSandbox.setDeviceWidth(375); // 375 px width – typical iPhone size
```

### Adjusting the Device Pixel Ratio

```java
renderingSandbox.setDevicePixelRatio(2.0); // 2× pixel density for retina displays
```

### Providing a Custom User‑Agent (set user agent java)

```java
renderingSandbox.setUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
    "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1"
);
```

> **Pro tip:** Matching a real device’s user‑agent string ensures that any JavaScript or CSS that checks `navigator.userAgent` behaves exactly as on that device.

## Step 4: Attach the Sandbox to the Document

Now we bind the sandbox to our HTML document so that all subsequent rendering respects the mobile settings we just defined.

```java
// Step 4: Apply the sandbox to the document so it renders with the mobile settings
htmlDoc.setSandbox(renderingSandbox);
```

If you skip this step, the default desktop viewport will be used, and your media queries for mobile will never fire—meaning the output PNG won’t look like a phone screen.

## Step 5: Choose Image Save Options (convert html to png)

Aspose.HTML supports many image formats. For a crisp PNG, we create an `ImageSaveOptions` instance with `SaveFormat.PNG`.

```java
// Step 5: Prepare image save options for PNG output
ImageSaveOptions imageOptions = new ImageSaveOptions(SaveFormat.PNG);
```

You can also tweak DPI, background color, or compression level via the `imageOptions` object if you need a higher‑resolution asset.

## Step 6: Render and Save – the final **convert html to png** step

The last line performs the heavy lifting: rendering the page inside the sandbox and writing the bitmap to disk.

```java
// Step 6: Render the page and save it as an image that reflects the mobile viewport
htmlDoc.save("YOUR_DIRECTORY/mobile-view.png", imageOptions);
```

When the program finishes, you’ll find a `mobile‑view.png` file that looks exactly like the page would on a 375 px wide iPhone with a 2× pixel density.

### Expected Output

Open the PNG in any image viewer and you should see:

- Text sized according to the mobile CSS breakpoints.
- Images scaled for a high‑density screen (thanks to the **set device pixel ratio** call).
- Any responsive navigation collapsed into its mobile variant.

If the output looks off, double‑check the URL, ensure all external resources are reachable, and verify that the sandbox settings match the target device.

## Common Pitfalls & How to Fix Them

| Problem | Why it Happens | Fix |
|---------|----------------|-----|
| **Missing fonts** | The sandbox doesn’t have access to system fonts used by the page. | Install the required fonts on the server or embed web‑fonts via `@font-face`. |
| **Cross‑origin images blocked** | Aspose.HTML respects CORS policies. | Host images on the same domain or enable CORS headers on the source server. |
| **JavaScript not executed** | By default, Aspose.HTML disables script execution for security. | Call `renderingSandbox.setEnableJavaScript(true)` if you need script‑driven layout changes (use with caution). |
| **Output blurry on retina screens** | DPI defaults to 96. | Set `imageOptions.setDpiX(300); imageOptions.setDpiY(300);` for higher resolution. |

## Full Working Example (All Steps in One Place)

Below is the complete, ready‑to‑run Java class. Replace `YOUR_DOMAIN` and `YOUR_DIRECTORY` with real values.

```java
import com.aspose.html.*;
import com.aspose.html.saving.*;
import com.aspose.html.rendering.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document that contains media queries
        HTMLDocument htmlDoc = new HTMLDocument("https://YOUR_DOMAIN/responsive.html");

        // Step 2: Create a rendering sandbox that simulates a mobile device
        RenderingSandbox renderingSandbox = new RenderingSandbox();

        // Step 3: Configure the sandbox (viewport width, pixel ratio, and user‑agent)
        renderingSandbox.setDeviceWidth(375);                     // 375 px width
        renderingSandbox.setDevicePixelRatio(2.0);               // 2× pixel density
        renderingSandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

        // Step 4: Apply the sandbox to the document so it renders with the mobile settings
        htmlDoc.setSandbox(renderingSandbox);

        // Step 5: Prepare image save options for PNG output
        ImageSaveOptions imageOptions = new ImageSaveOptions(SaveFormat.PNG);

        // Step 6: Render the page and save it as an image that reflects the mobile viewport
        htmlDoc.save("YOUR_DIRECTORY/mobile-view.png", imageOptions);
    }
}
```

Run the program (`mvn exec:java` or your IDE’s run configuration) and you’ll have a **create PNG from HTML** pipeline that works entirely offline.

## Conclusion

We’ve just covered everything you need to **create PNG from HTML** in Java—loading the document, configuring a sandbox, **setting user agent java**, adjusting the **device pixel ratio**, and finally **render html to png**. The code is compact, the dependencies are minimal, and the result is a perfectly sized PNG that mirrors a real mobile device.

What’s next? Try swapping the PNG format for JPEG if you need smaller files, experiment with different viewport widths to generate thumbnails for tablets, or integrate this snippet into a Spring Boot endpoint that returns the image on demand. The possibilities are endless, and now you have a solid foundation to build on.

Got questions or ran into an odd edge case? Drop a comment below, and let’s troubleshoot together. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to PNG with Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-png/)
- [Convert HTML to PNG with Aspose.HTML Message Handlers in Java](/html/english/java/configuring-environment/use-message-handlers/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}