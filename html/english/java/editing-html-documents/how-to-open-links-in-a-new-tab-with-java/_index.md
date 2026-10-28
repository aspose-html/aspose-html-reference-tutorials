---
category: general
date: 2026-10-28
description: Learn how to open links in a new tab by parsing HTML in Java, finding
  external links and adding target blank.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: en
lastmod: 2026-10-28
og_description: 'Open links in a new tab using Java: parse HTML, find external links,
  add target blank, and save modified HTML.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Open links in a new tab with Java – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: How to open links in a new tab with Java
url: /java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to open links in a new tab with Java

If you need to **open links in a new tab** from a static HTML file, this guide shows you exactly how to do it. You’ll learn to **parse HTML in Java**, **find external links**, **add target blank**, and **save modified HTML** without leaving your IDE.

Opening external links in a new browser tab improves user experience and keeps visitors on the original page. The solution below works with any HTML document, requires only the popular jsoup library, and runs on Java 8 or newer.

## Prerequisites

Before you start, make sure you have:

* JDK 8 + installed  
* A build tool (Maven or Gradle) to pull in the **jsoup** dependency  
* An HTML file that contains anchor tags with the class `external`

You do not need a web server or additional frameworks—jsoup handles everything locally.

## Step 1: Set up jsoup in your project

Add jsoup as a dependency. If you use Maven, place this in `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

For Gradle, add the following line to `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

These coordinates pull the latest stable release (as of October 2026). After syncing, you can import `org.jsoup` classes in your Java source files.

## Step 2: Parse the HTML document

Parsing the file is the first step toward **open links new tab**. The `Jsoup.parse` method reads the file into a mutable DOM‑like structure.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Why this matters*: `Document` gives you CSS‑style selectors, making it trivial to locate the elements you need.

## Step 3: Find external links

Now locate every `<a>` element that carries the class `external`. This matches the **find external links** requirement.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` is a collection of matching nodes. If the selector returns an empty set, your HTML either lacks the class or uses a different naming convention—adjust the selector accordingly.

## Step 4: Add `target="_blank"` to each link

For each node returned by **find external links**, set the `target` attribute to `_blank`. This satisfies the **add target blank** step and ensures browsers open the link in a new tab.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

The `attr` method overwrites any existing `target` value, guaranteeing consistent behavior across all external anchors.

## Step 5: Save the modified HTML

After updating the DOM, write the changes back to a file. This completes the **save modified html** portion of the tutorial.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` serializes the entire document, preserving indentation and formatting as jsoup originally parsed it.

## Full working example

Putting all steps together yields a self‑contained program you can copy, paste, and run.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Expected output

Assume `sample.html` contains:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

After running the program, `updated.html` will contain:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Only the external link received the `target="_blank"` attribute, which means browsers will now open it in a new tab.

## Pro tips and common pitfalls

* **Pro tip:** If you need to treat links that start with `http://` or `https://` as external even without a CSS class, expand the selector: `doc.select("a[href^=http]")`.
* **Edge case:** Some pages already specify `target="_self"`; the `attr` call overwrites it, ensuring consistent behavior.
* **Performance:** For very large HTML files, consider streaming parsing (`Jsoup.parse(File, String, String, Parser.htmlParser())`) to reduce memory usage.
* **Testing:** Verify the result by opening `updated.html` in a browser and inspecting the link with the developer tools—look for the `target` attribute.

## Conclusion

You now have a complete, runnable solution to **open links in a new tab** using Java. The tutorial covered how to **parse html in java**, **find external links**, **add target blank**, and **save modified html**, all with the lightweight jsoup library. 

From here you can:

* Extend the selector to handle other link patterns (e.g., `rel="external"`).  
* Combine this logic with a build step that processes all HTML files in a project.  
* Integrate the code into a larger content‑management pipeline.

Feel free to experiment with different selectors or output formats, and share your results with the community!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}