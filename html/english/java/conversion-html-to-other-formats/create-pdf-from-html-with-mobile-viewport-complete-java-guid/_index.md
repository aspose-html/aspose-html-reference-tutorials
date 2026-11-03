---
category: general
date: 2026-03-18
description: Create PDF from HTML in Java quickly. Learn how to convert HTML to PDF,
  simulate iPhone screen, and set screen size for responsive PDFs.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- simulate iphone screen
- how to set screen
- how to convert html
language: en
og_description: Create PDF from HTML in Java. This guide shows how to convert HTML
  to PDF, simulate an iPhone screen, and set screen dimensions for perfect responsive
  PDFs.
og_title: Create PDF from HTML with Mobile Viewport – Java Tutorial
tags:
- Java
- Aspose.HTML
- PDF
- Responsive Design
- Mobile Viewport
title: Create PDF from HTML with Mobile Viewport – Complete Java Guide
url: /java/conversion-html-to-other-formats/create-pdf-from-html-with-mobile-viewport-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF from HTML with Mobile Viewport – Complete Java Guide

Ever needed to **create PDF from HTML** but the output looked like a desktop page on a tiny phone screen? You're not the only one. When you convert a responsive website to PDF, the default viewport often ignores the mobile breakpoints, leaving you with a cramped mess.  

The good news? You can **convert HTML to PDF** while **simulating an iPhone screen**, all from plain Java code. In this tutorial we’ll walk through every step—how to set screen size, how to adjust device‑scale factor, and why those settings matter for a pixel‑perfect PDF.

> **Pro tip:** If you’ve already used Aspose.HTML for simple conversions, you’ll find the viewport tweaks just a few extra lines away.

---

## What You’ll Learn

* How to **create PDF from HTML** using Aspose.HTML for Java.  
* The exact code to **simulate iPhone screen** dimensions (375 × 667 px @ 2× density).  
* Where to place **how to set screen** options in the conversion pipeline.  
* Common pitfalls when converting responsive pages and how to avoid them.  
* A complete, ready‑to‑run Java example that you can copy‑paste into your IDE.

### Prerequisites

* Java 17 or newer (the code compiles with older versions, but 17 is recommended).  
* Aspose.HTML for Java library – you can grab the latest JAR from the [Aspose website](https://products.aspose.com/html/java).  
* A simple HTML file (`input.html`) you want to turn into a PDF.  
* Basic familiarity with Maven or Gradle (we’ll show a Maven snippet).

---

## Step 1 – Add Aspose.HTML to Your Project

First things first, you need the library on your classpath. If you use Maven, drop this dependency into your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Why this matters:** Aspose.HTML handles the heavy lifting—parsing HTML, applying CSS, and rasterizing the layout. Without it, you’d have to write a full browser engine yourself, which is a *lot* of work.

If you prefer Gradle, the equivalent is:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

---

## Step 2 – Prepare Load Options and Simulate an iPhone Viewport

Now we’ll configure the **how to set screen** parameters. The `HtmlLoadOptions` class lets you tell Aspose what size and pixel density to pretend the browser has.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class ViewportDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create load options for the HTML document
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // 2️⃣ Simulate a mobile viewport (iPhone 6/7/8) – 375 × 667 pixels with retina density
        loadOptions.setScreenSize(new Size(375, 667));
        loadOptions.setDeviceScaleFactor(2.0);

        // 3️⃣ Convert the HTML file to PDF using the configured viewport
        Converter.convertDocument(
                "YOUR_DIRECTORY/input.html",          // source HTML
                "YOUR_DIRECTORY/output.pdf",          // destination PDF
                new PdfSaveOptions(),
                loadOptions);

        // 4️⃣ Notify that the conversion is complete
        System.out.println("Responsive conversion using mobile viewport.");
    }
}
```

### Why These Numbers?

* **375 × 667** matches the logical CSS pixel dimensions of an iPhone 6/7/8 in portrait mode.  
* **DeviceScaleFactor = 2.0** tells the renderer that each CSS pixel corresponds to two physical pixels, mimicking the Retina display.  

If you need a different device—say an iPhone 12 Pro Max—you’d change the size to `428 × 926` and keep the scale factor at `3.0`.

---

## Step 3 – Run the Conversion and Verify the Output

Compile and run the class:

```bash
mvn compile exec:java -Dexec.mainClass=ViewportDemo
```

After the program finishes, open `output.pdf`. You should see:

* All media queries targeting `max-width: 375px` applied correctly.  
* Images rendered sharply thanks to the 2× scale factor.  
* Text that respects the mobile font‑size hierarchy you defined in CSS.

If the PDF still looks like a desktop page, double‑check that your HTML uses responsive meta tags:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Without that tag, even a perfect viewport setting won’t trigger the mobile stylesheet.

---

## Step 4 – Handling External Resources (Images, Fonts, CSS)

When you **convert HTML to PDF**, Aspose.HTML tries to fetch every linked resource. If you’re converting a page that lives on a local file system, absolute URLs (`file:///…`) work fine. For remote assets you might run into:

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **404 errors for images** | The HTML points to a URL that requires authentication. | Use `HtmlLoadOptions.setBaseUrl("file:///C:/myproject/")` to resolve relative paths, or embed images as Base64. |
| **Missing web fonts** | The PDF engine can’t download the font file. | Download the `.woff`/`.ttf` files locally and reference them with a relative path. |
| **CSS not applied** | The CSS file is blocked by CORS. | Host the CSS on a server that allows cross‑origin requests, or inline the CSS in the HTML. |

A quick way to test resource loading is to wrap the conversion call in a try‑catch block and print the `Exception` message. Aspose.HTML provides detailed logs that point to the exact URL that failed.

```java
try {
    Converter.convertDocument(...);
} catch (Exception ex) {
    System.err.println("Conversion failed: " + ex.getMessage());
}
```

---

## Step 5 – Advanced Tweaks (Optional)

### a) Change PDF Page Size

By default Aspose.HTML creates a PDF page that matches the viewport size. If you prefer A4 or Letter, add a `PdfSaveOptions` configuration:

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PageSize.A4);
Converter.convertDocument("input.html", "output.pdf", pdfOptions, loadOptions);
```

### b) Add a Header/Footer Programmatically

You can inject a simple header/footer after conversion using Aspose.PDF (a separate library). The workflow is:

1. Convert HTML → PDF (as shown).  
2. Open the resulting PDF with Aspose.PDF.  
3. Add `HeaderFooter` objects to each page.

```java
import com.aspose.pdf.*;

Document pdfDoc = new Document("output.pdf");
for (Page page : pdfDoc.getPages()) {
    page.addHeaderFooter(new HeaderFooter("Generated on " + LocalDate.now()));
}
pdfDoc.save("output-with-header.pdf");
```

### c) Batch Conversion

If you have a folder of HTML files, loop over them:

```java
Files.list(Paths.get("html_folder"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(p -> {
         String pdfPath = p.toString().replace(".html", ".pdf");
         Converter.convertDocument(p.toString(), pdfPath, new PdfSaveOptions(), loadOptions);
     });
```

---

## Frequently Asked Questions (FAQs)

**Q: Does this work with JavaScript‑heavy pages?**  
A: Aspose.HTML supports a subset of JavaScript. Simple DOM manipulation and CSS changes usually work, but complex frameworks (React, Angular) may need a pre‑rendered static HTML snapshot.

**Q: What if I need to convert a page that uses `@media print` rules?**  
A: The library respects `@media print` automatically. However, if you also set a mobile viewport, the `print` stylesheet may override some mobile styles. Test both scenarios.

**Q: Can I set a custom DPI for the PDF?**  
A: Yes. Use `PdfSaveOptions.setDpi(300)` before conversion. Higher DPI yields larger files but sharper images.

---

## Expected Result Screenshot

Below is an illustration of the final PDF page (mobile viewport simulated).  
![Screenshot of PDF generated by create pdf from html demo showing iPhone‑sized layout]  

*Image alt text includes the primary keyword for SEO.*

---

## Conclusion

You now have a solid, **create pdf from html** workflow that respects mobile breakpoints, simulates an iPhone screen, and gives you full control over page dimensions. By tweaking `HtmlLoadOptions` you can answer “**how to set screen**” for any device, and by using `Converter.convertDocument` you’ve mastered **how to convert html** in Java.

Ready for the next challenge? Try combining this approach with Aspose.PDF to add watermarks, merge multiple PDFs, or protect the document with a password. And don’t forget to experiment with other devices—just change the `Size` and `DeviceScaleFactor` values to match the pixel density you need.

Happy coding, and may your PDFs always look as crisp on paper as they do on a phone screen! 

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}