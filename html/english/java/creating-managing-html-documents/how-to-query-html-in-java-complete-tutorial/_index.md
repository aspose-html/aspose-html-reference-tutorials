---
category: general
date: 2026-01-01
description: Learn how to query HTML using Java, how to select CSS, and extract elements
  from HTML with practical examples and node counting.
draft: false
keywords:
- how to query html
- how to select css
- extract elements from html
- select multiple css classes
- how to count nodes
language: en
og_description: Master how to query HTML in Java, learn how to select CSS, extract
  elements from HTML and count nodes with real code examples.
og_title: How to Query HTML in Java – Complete Tutorial
tags:
- Java
- HTML parsing
- Aspose.HTML
title: How to Query HTML in Java – Complete Tutorial
url: /java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Query HTML in Java – Complete Tutorial

Ever wondered **how to query HTML** from a Java program without pulling your hair out? You're not the only one. Many developers hit a wall when they need to pull data from a static catalog or scrape a simple page, and the usual DOM tricks feel clunky.  

The good news? With a few lines of code you can load an HTML file, run XPath or CSS selectors, and even count the nodes you care about—all in one tidy flow. In this guide we’ll walk through **how to query HTML**, **how to select CSS**, and show you how to **extract elements from HTML**, **select multiple CSS classes**, and **how to count nodes** with Aspose.HTML for Java.

## What You’ll Learn

- Load an HTML document from disk or a URL.  
- Use XPath to find elements that match complex conditions.  
- Apply CSS selectors, including multiple class queries.  
- Count the results programmatically.  
- Tips, pitfalls, and variations for real‑world scenarios.

*Prerequisites*: Java 8+, Maven or Gradle, and a copy of the Aspose.HTML for Java library (the free trial works fine for experimentation).

---

![how to query html example](https://example.com/images/query-html.png "Screenshot showing how to query html with Java")

## How to Query HTML – Loading the Document

Before you can ask any questions, you need a document object to interrogate. Aspose.HTML’s `HTMLDocument` class does the heavy lifting.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document you want to query
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");
```

> **Why this matters** – Loading the file creates a DOM tree in memory. From there you can run both XPath and CSS queries without worrying about network latency or malformed markup. If the file isn’t found, Aspose throws a clear `FileNotFoundException`, making debugging painless.

### Pro tip
If you’re pulling HTML from a remote site, simply pass the URL string to `HTMLDocument`—Aspose will fetch and parse it for you.

## How to Select CSS – Using CSS Selectors

Once the DOM is ready, selecting nodes with CSS is as simple as a one‑liner. Let’s grab every element that has either the `featured` or `highlight` class.

```java
        // Step 2: Locate elements marked as featured or highlighted using a CSS selector
        List<Element> featuredElements = document.selectCss(".featured, .highlight");

        // Step 3: Output the number of elements found by the CSS selector
        System.out.println("Featured elements: " + featuredElements.size());
```

> **Explanation** – The selector `.featured, .highlight` tells the engine to return *any* element whose `class` attribute contains `featured` **or** `highlight`. This is the canonical way to **select multiple CSS classes** in a single query.

### Edge case
If an element contains both classes (e.g., `<div class="featured highlight">`), it will appear **once** in the result list, preventing double‑counting.

## Extract Elements from HTML – Combining XPath and CSS

XPath shines when you need relational logic, such as “all `<book>` nodes where the price exceeds 30”. Here’s the exact snippet from the original example:

```java
        // Step 4: Find all <book> elements with a price greater than 30 using XPath
        List<Element> expensiveBooks = document.selectXPath("//book[price>30]");

        // Step 5: Output the number of books that match the XPath query
        System.out.println("Expensive books count: " + expensiveBooks.size());
```

> **Why XPath?** – XPath can evaluate numeric comparisons (`price>30`) directly, something CSS cannot do. It also lets you traverse parent/child relationships without extra code.

### Variation
If you need to fetch the *titles* of those expensive books, you can chain a second query:

```java
        List<Element> titles = expensiveBooks.get(0).selectXPath("./title");
        System.out.println("First expensive book title: " + titles.get(0).getTextContent());
```

## Select Multiple CSS Classes – Advanced Selector Tricks

Sometimes you want to target elements that **simultaneously** have several classes, like `class="product featured"`. The CSS syntax for this is a concatenated selector without commas.

```java
        // Example: select <div> elements that are both .product and .featured
        List<Element> productFeatured = document.selectCss("div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured.size());
```

> **Key point** – No space between the class names; a space would mean “descendant”. This pattern is essential when you’re **selecting multiple CSS classes** that work together to style a component.

## How to Count Nodes – Getting Accurate Totals

Counting nodes is often the final step in a data‑extraction pipeline. You’ve already seen `list.size()` used after each query, but let’s wrap it into a reusable helper.

```java
    /**
     * Returns the count of elements that match the given CSS selector.
     */
    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    /**
     * Returns the count of elements that match the given XPath expression.
     */
    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        System.out.println("Expensive books: " + countByXPath(doc, "//book[price>30]"));
        System.out.println("Featured items: " + countByCss(doc, ".featured, .highlight"));
        System.out.println("Product‑featured divs: " + countByCss(doc, "div.product.featured"));
    }
```

> **Why wrap it?** – Centralising the count logic makes your code easier to test and reduces duplication. It also clarifies **how to count nodes** for future readers.

### Common pitfalls
- **Whitespace in class attributes** – `"featured "` (trailing space) still matches `.featured` because the selector trims whitespace.
- **Case sensitivity** – HTML class names are case‑sensitive in XML mode; ensure your source HTML uses consistent casing.

## Full Working Example

Putting everything together, here’s a self‑contained program you can copy‑paste into your IDE:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {

    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        // Load the HTML file (adjust the path as needed)
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        // XPath: books priced over 30
        int expensiveBooks = countByXPath(document, "//book[price>30]");
        System.out.println("Expensive books count: " + expensiveBooks);

        // CSS: featured or highlighted elements
        int featured = countByCss(document, ".featured, .highlight");
        System.out.println("Featured elements: " + featured);

        // CSS: elements that are both .product and .featured
        int productFeatured = countByCss(document, "div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured);
    }
}
```

**Expected output** (assuming a typical `catalog.html`):

```
Expensive books count: 4
Featured elements: 7
Product‑featured divs: 2
```

If your file contains fewer matching nodes, the numbers will adjust accordingly—no surprises.

---

## Conclusion

We’ve covered **how to query HTML** with Aspose.HTML for Java, demonstrated **how to select CSS**, shown you how to **extract elements from HTML**, tackled **select multiple CSS classes**, and explained **how to count nodes** reliably.  

The key takeaway? Loading the document once and then reusing the same `HTMLDocument` instance lets you mix XPath and CSS queries without performance penalties.  

Ready for the next step? Try chaining selectors to pull attribute values (`@href`, `@src`) or exporting the result set to JSON for downstream processing. You might also explore pagination handling if your source HTML spans multiple pages.

Got a tricky selector or an edge case you can’t crack? Drop a comment below, and let’s troubleshoot together. Happy querying!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}