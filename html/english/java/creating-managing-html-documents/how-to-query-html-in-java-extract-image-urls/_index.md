---
category: general
date: 2026-03-05
description: How to query HTML in Java to read an HTML file and extract images. Learn
  to read HTML file Java, get image URLs Java, and iterate over NodeList Java.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: en
og_description: How to query HTML in Java and retrieve image URLs. This guide shows
  how to read HTML file Java, locate images, and iterate over NodeList Java.
og_title: How to Query HTML in Java – Extract Image URLs
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: How to Query HTML in Java – Extract Image URLs
url: /java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Query HTML in Java – Extract Image URLs

Ever wondered **how to query HTML** in Java to pull out every picture on a page? You're not the only one—developers constantly need to read HTML files, scrape images, and then do something useful with the URLs. In this tutorial we’ll walk through a practical example that shows exactly **how to query HTML**, read an HTML file Java style, and get image URLs Java‑wise.

We'll use Aspose.HTML for Java, but the concepts—XPath, CSS selectors, and iterating over a `NodeList`—apply to any DOM library. By the end of this guide you'll be comfortable with **how to extract images**, know how to **iterate over NodeList Java**, and have a ready‑to‑run code snippet you can drop into your project.

![How to query HTML in Java example](https://example.com/placeholder.png "How to query HTML in Java")

---

## What You'll Learn

- Load an HTML document from disk (read HTML file Java)
- Locate `<img>` tags using both XPath and CSS selectors (how to extract images)
- Loop through the resulting `NodeList` (iterate over NodeList Java)
- Print each image’s `src` attribute (get image URLs Java)

No external services, no complex build tools—just plain Java and a single Maven dependency.

---

## Prerequisites

- Java 8 or newer installed
- Maven or Gradle for dependency management
- Basic familiarity with HTML structure
- Optional but helpful: a simple HTML file (`sample.html`) containing some `<figure><img …></figure>` elements

If you’ve got those, we can jump right in.

---

## Step 1: Read HTML File Java – Load the Document

First thing’s first: we need to bring the HTML into memory. Aspose.HTML’s `HTMLDocument` class does the heavy lifting. Think of it as opening a book so you can flip to any page.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Why this matters:** Loading the file gives you a DOM tree you can query. If the path is wrong, you’ll get a `FileNotFoundException`, so double‑check the location before running.

---

## Step 2: Locate Images with XPath – How to Extract Images

XPath is a powerful query language that lets you pinpoint nodes with laser precision. Here we ask for every `<img>` inside a `<figure>` that also has an `alt` attribute.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Why XPath?** It’s concise and works even when the HTML is messy. The `//figure/img[@alt]` expression translates to: “any `<img>` under a `<figure>` that carries an `alt` attribute.” If you need to filter by other attributes, just tweak the brackets.

---

## Step 3: Locate Images with CSS Selector – Alternative Way to Extract Images

Sometimes you prefer CSS syntax because it mirrors what you write in stylesheets. `querySelectorAll` accepts the same selector you’d use in a browser.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Why both?** Demonstrating both shows you can pick the tool you’re most comfortable with. In practice you’d stick to one, but having both examples makes the tutorial more complete.

---

## Step 4: Iterate Over NodeList Java – Get Image URLs Java

Now that we have a collection, we need to walk through it. This is where **iterate over NodeList Java** comes into play. We’ll pull out the `src` attribute of each image and print it.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Why a classic `for` loop?** The Aspose `NodeList` does not implement `Iterable`, so the enhanced `for‑each` syntax won’t compile. Using an index loop is the reliable way to **iterate over NodeList Java**.

---

## Expected Output

Running the program against a sample HTML like:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Will produce something similar to:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

If your file contains more `<img>` tags that meet the criteria, the numbers will increase accordingly.

---

## Common Pitfalls & Pro Tips

- **File path issues:** Use an absolute path or place `sample.html` relative to your project’s working directory.  
- **Missing `alt` attribute:** Our XPath/CSS queries filter on `[@alt]`. If you need *all* images, drop the attribute filter (`//figure/img` or `figure img`).  
- **Performance:** For huge documents, consider streaming parsers, but for most web‑scraping tasks the DOM approach is fine.  
- **Encoding problems:** Aspose.HTML respects the charset declared in the HTML. If you see garbled characters, ensure the file is saved as UTF‑8.  

---

## Extending the Example

Now that you can **get image URLs Java**, you might want to:

1. **Download the images** using `java.net.URL` and `Files.copy`.  
2. **Store URLs in a database** for later processing.  
3. **Filter by file extension** (`src.endsWith(".png")`).  

All of these are straightforward extensions of the loop shown in Step 4.

---

## Conclusion

In this guide we covered **how to query HTML** in Java from start to finish: loading the file, locating images with both XPath and CSS selectors, and **iterating over NodeList Java** to print each image’s `src`. You now have a solid foundation for **how to extract images**, and you know exactly **how to read HTML file Java** using Aspose.HTML.

Feel free to adapt the code to suit your own scraping needs—whether that means pulling other attributes, handling `<a>` tags, or feeding the URLs into a downloader. The pattern stays the same: load, query, iterate, and act.

Got questions or want to share a cool use‑case? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}