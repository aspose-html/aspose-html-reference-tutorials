---
category: general
date: 2026-02-16
description: How to load HTML in Java, set device DPI, define a virtual screen size,
  and read the computed background color of any element.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: en
og_description: How to load HTML in Java, set device DPI, define a virtual screen
  size, and read the computed background color of any element.
og_title: How to Load HTML, Set Device DPI & Read Background Color
tags:
- Aspose.HTML
- Java
title: How to Load HTML, Set Device DPI & Read Background Color
url: /java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Load HTML, Set Device DPI & Read Background Color

Ever wondered **how to load html** in a Java app and then inspect the page’s styles? You’re not alone—developers often need to render a web page off‑screen, grab the final CSS values, and use them for PDF conversion, screenshots, or even automated tests.  

In this guide we’ll walk through exactly that: we’ll load an HTML file, **set device DPI**, define a **virtual screen size**, and finally **read background color** from the `<body>` element. By the end you’ll have a fully runnable snippet that prints the **computed background color**—no mystery, just plain Java.

## What You’ll Need

Before we dive, make sure you have:

* Java 17 or newer (the code works with any recent JDK).  
* Aspose.HTML for Java 23.9 or later—download the JAR from the Aspose site or add it via Maven.  
* A simple HTML file (e.g., `responsive.html`) that defines a background color in CSS.

That’s it—no extra frameworks, no browser drivers. Ready? Let’s get started.

![Diagram illustrating how to load html and extract computed styles](/images/load-html-diagram.png){alt="Diagram illustrating how to load html"}

## Step 1: How to Load HTML and Configure Rendering Options

The first thing you do is create a `HtmlLoadOptions` object. This object tells Aspose.HTML **how to load html**—including the virtual screen dimensions and the DPI you want to emulate.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Why this matters:**  
Setting a virtual screen size ensures that media queries like `@media (max-width: 600px)` behave as if the page were rendered on a real monitor. The DPI influences how CSS `px` units are mapped to physical pixels—crucial when you later generate images or PDFs.

## Step 2: Load the HTML File Using the Configured Options

Now we actually load the file. Notice we pass the same `loadOptions` we just configured.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

If the file isn’t found, Aspose throws a clear `FileNotFoundException`. In production you might want to wrap this in a try‑catch and fallback to a default HTML string.

## Step 3: Set Virtual Screen Size and Device DPI (Explicitly)

Even though we already called `setScreenSize` and `setDeviceDpi` above, it’s worth highlighting that **set virtual screen size** and **set device dpi** can be adjusted at any point before rendering. For example, you could increase the DPI for high‑resolution screenshots:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Remember to reload the document if you change these settings after the first load—Aspose treats them as immutable once the `Document` is created.

## Step 4: Read Background Color and Get Computed Background Color

With the document in memory, you can query any element’s computed style. Here we focus on the `<body>` tag, but the same approach works for `<div>`, `<p>`, or even pseudo‑elements.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**What you’ll see:** If `responsive.html` contains `body { background: #ff5722; }`, the console prints something like:

```
Computed background color: rgba(255,87,34,1)
```

That’s the **get computed background color** result—Aspose resolves all CSS cascade rules, media queries, and even `!important` declarations before returning the final value.

## Full Working Example

Putting it all together, here’s the complete, copy‑paste‑ready program:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Expected Output

```
Computed background color: rgba(255,255,255,1)
```

*(The exact RGBA values depend on the CSS in your HTML file.)*

## Common Pitfalls & Pro Tips

* **Missing DPI setting?** Aspose defaults to 96 DPI, which may blur high‑resolution screenshots. Always set it explicitly if you need crisp output.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}