---
category: general
date: 2026-09-29
description: Learn how to select elements by class, read HTML from file, and find
  external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: en
lastmod: 2026-09-29
og_description: Select elements by class in Java, read HTML from file, and find external
  links using querySelectorAll. Follow the full example to iterate a NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Select elements by class in Java – complete guide with querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: How to select elements by class in Java using querySelectorAll
url: /java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to select elements by class in Java using querySelectorAll

If you need to **select elements by class** while processing an HTML file in Java, this guide shows you exactly how to do it. You’ll learn to read HTML from file, use `querySelectorAll` to find external links, and iterate the resulting `NodeList` safely.

Working with HTML in Java often feels heavyweight, but modern libraries give you a concise, CSS‑selector‑based API. The example below uses **jsoup** (version 1.17.2) because it implements `querySelectorAll`‑style selectors and returns a `Elements` collection that behaves like a `NodeList`. You can adapt the same logic to other DOM implementations if needed.

## Prerequisites

Before you start, make sure you have:

* JDK 17 or newer installed.
* Maven or Gradle for dependency management.
* Basic familiarity with Java streams and the DOM model.

Add jsoup to your project:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Step 1: Read HTML from file

The first task is to load the HTML document from disk. `Jsoup.parse(Path, Charset)` reads the file and builds a DOM tree you can query.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Why this matters*: Loading the file once avoids repeated I/O while you iterate over elements later. The `Document` object holds the full DOM, enabling fast selector queries.

## Step 2: Use `querySelectorAll` to select elements by class

Now that the document is in memory, you can **select elements by class** using a CSS selector. The selector `"a.external"` matches `<a>` tags that carry the `external` class—exactly what you need to **find external links**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Why this matters*: Using a class selector is both expressive and performant. The library translates the selector into an optimized traversal, so you don’t need to write manual loops over every node.

## Step 3: Iterate the NodeList (Elements) in Java

`Elements` implements `Iterable<Element>`, which means you can use a standard `for‑each` loop to **iterate NodeList Java** objects. The loop below prints each link’s `href` attribute.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Why this matters*: Direct iteration keeps the code readable and avoids the overhead of converting the collection to a stream when you only need simple output.

## Full working example

Putting the three steps together yields a self‑contained program you can run from the command line.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Expected output

Assuming `input.html` contains:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Running the program prints:

```
External link: https://example.com
External link: https://openai.com
```

## Pro tips and common pitfalls

* **Encoding matters** – Always read the file with UTF‑8 (or the charset that matches your source). Incorrect encoding can corrupt characters in attribute values.
* **Multiple classes** – If an element has several classes (e.g., `class="btn external"`), the selector `"a.external"` still matches because CSS class selectors check for the presence of the token, not the exact string.
* **Performance tip** – If you only need the `href` attribute, you can request it directly with `doc.select("a.external[href]").eachAttr("href")`. This avoids creating full `Element` objects for each match.
* **Null safety** – `link.attr("href")` returns an empty string if the attribute is missing, so you don’t need a null check before printing.

## Frequently asked questions

**Q: Does this work with HTML fragments that lack a `<html>` root?**  
A: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds missing root elements, allowing selectors to work on the fragment’s body.

**Q: Can I use `querySelectorAll` without jsoup?**  
A: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`. Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods. The pattern shown here—load, select with CSS, iterate—remains the same.

**Q: What if I need to modify the links instead of just printing them?**  
A: After obtaining each `Element`, you can call `link.attr("href", "newUrl")` and then write the document back to disk with `Files.writeString`.

## Conclusion

You now know how to **select elements by class**, **read HTML from file**, **find external links**, and **iterate a NodeList in Java** using `querySelectorAll`‑style selectors. The complete example demonstrates a clean, production‑ready workflow that you can embed in larger scraping or transformation pipelines.

Next, explore related topics such as **parsing dynamic content with HTMLUnit**, **writing modified HTML back to disk**, or **using Java streams to collect link URLs into a list**. Each of these builds on the core technique of class‑based selection demonstrated here. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to query HTML in Java – Select elements, filter by attribute, and get text](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Iterate NodeList Java – Read HTML & Get Image src](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}