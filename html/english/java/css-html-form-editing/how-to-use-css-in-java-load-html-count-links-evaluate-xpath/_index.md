---
category: general
date: 2026-06-16
description: How to use CSS to load HTML file and count links in Java. Learn to count
  html elements and evaluate xpath java in a single, clear example.
draft: false
keywords:
- how to use css
- load html file
- how to count links
- count html elements
- evaluate xpath java
language: en
og_description: How to use CSS in Java to load an HTML file, count links, and evaluate
  XPath expressions—all in one practical guide.
og_title: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  headline: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  type: TechArticle
- description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  name: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  steps:
  - name: What if the HTML file is malformed?
    text: Both the CSS and XPath engines are tolerant of minor markup errors (missing
      closing tags, unquoted attributes). However, severe malformations may cause
      the parser to abort. In production, wrap the loading step in a try‑catch block
      and log the exception.
  - name: Can I combine CSS and XPath in a single expression?
    text: Not directly; each engine has its own syntax. The typical pattern is to
      use the one that expresses the condition most naturally (CSS for structural
      queries, XPath for attribute functions) and then merge the results in Java if
      needed.
  - name: How do I count elements across multiple files?
    text: 'Just place the loading logic inside a loop:'
  - name: Does this work with Java 8?
    text: Yes—provided you use a library version that targets Java 8 or higher. The
      code shown does not rely on newer language features.
  type: HowTo
tags:
- Java
- HTML parsing
- CSS selectors
- XPath
title: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
url: /java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath

Ever wondered **how to use CSS** selectors while processing an HTML file in Java? Maybe you're building a web‑crawler, a scraper, or just need to audit a static site. The good news? You don’t have to write a custom parser from scratch—modern libraries let you blend CSS4 selectors with XPath 3.1 expressions in a single, tidy workflow.

In this tutorial we’ll walk through **how to load an HTML file**, apply a CSS selector to count links inside a navigation bar, and then **evaluate XPath** to count specific image elements. By the end you’ll have a complete, runnable program that prints the number of matching nodes, and you’ll understand why each piece matters.

## Prerequisites

- Java 17 (or any recent JDK) installed on your machine  
- Maven or Gradle for dependency management (we’ll use Maven in the example)  
- A tiny HTML snippet saved as `input.html` in a folder you control  

No other tools are required—just a text editor and a terminal.

## What the Tutorial Covers

- **Loading an HTML file** into a DOM‑like structure using the *HTMLDocument* class  
- Applying a **CSS4 selector** (`nav a[data-role]`) to locate navigation links  
- Running an **XPath 3.1 expression** to find `<img>` tags whose `src` ends with `.png` and that also have an `alt` attribute  
- **Counting** the results of both queries and printing them to the console  
- Full source code, explanations of the “why”, and a quick look at possible edge cases  

Let's jump right in.

---

## Step 1 – How to Load an HTML File with HTMLDocument

Before you can query anything, the HTML document must be parsed into a traversable model. The `HTMLDocument` class from the **jsoup‑plus** library (or any similar HTML‑aware parser) does exactly that.

```java
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Load the HTML document from the file system
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/input.html");
        // From here on we can query the DOM using CSS or XPath
```

*Why this matters:*  
Loading the file once and keeping a reference (`doc`) avoids repeated I/O, which can be a performance bottleneck when processing large batches of pages.

---

## Step 2 – How to Use CSS to Count Links Inside `<nav>`

Now that the document is in memory, we can use a CSS4 selector to grab every `<a>` element that lives inside a `<nav>` and also carries a `data‑role` attribute. This is a common pattern for navigation menus that use data attributes for JavaScript hooks.

```java
        // Use a CSS4 selector to find every <a> inside a <nav> that has a data‑role attribute
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");
```

*Explanation:*  
- `nav a[data-role]` reads as “any `<a>` element with a `data‑role` attribute that is a descendant of a `<nav>` element.”  
- The selector is **CSS4**‑compatible, meaning you can also use pseudo‑classes like `:not()` or `:has()` if your use case grows.

> **Pro tip:** If you only need direct children, replace the space with `>` (`nav > a[data-role]`). This reduces the search space and can speed up large documents.

---

## Step 3 – Evaluate XPath Java to Count Specific `<img>` Elements

XPath shines when you need attribute‑based filtering that isn’t as straightforward in CSS. Here we’ll locate every `<img>` whose `src` ends with `.png` **and** that also defines an `alt` attribute—useful for accessibility audits.

```java
        // Use an XPath 3.1 expression to locate all <img> elements whose src ends with .png and have an alt attribute
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");
```

*Why XPath?*  
- The `ends-with()` function is part of XPath 3.1, allowing suffix matching without resorting to regex.  
- Combining multiple predicates (`and @alt`) ensures you only count images that are both correctly sourced and described.

If your library only supports XPath 1.0, you’d need to use `contains(@src, '.png')` and then filter in Java—a less precise approach.

---

## Step 4 – How to Count HTML Elements and Print Results

Finally, we retrieve the lengths of both `NodeList` objects and output them. This is the **how to count links** part of the puzzle, but it works for any node collection.

```java
        // Output the number of matches for each query
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Expected console output** (assuming the sample HTML contains 3 matching links and 2 matching images):

```
Nav links: 3
PNG images with alt: 2
```

If the counts are zero, double‑check your selector syntax or verify that `input.html` actually contains the expected elements.

---

## Full Working Example

Below is the complete, self‑contained program you can copy‑paste into a file named `CssXPathDemo.java`. It includes the necessary imports, a simple `pom.xml` snippet for Maven, and a minimal HTML sample for testing.

```java
/* CssXPathDemo.java */
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document
        HTMLDocument doc = new HTMLDocument("input.html");

        // Step 2: CSS selector – count navigation links with data-role
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");

        // Step 3: XPath expression – count PNG images that have alt text
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");

        // Step 4: Print the results
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Maven `pom.xml` excerpt** (add this dependency to pull in the HTML‑aware parser that supports both CSS4 and XPath 3.1):

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>html-parser-plus</artifactId>
        <version>2.3.1</version>
    </dependency>
</dependencies>
```

**Sample `input.html`** (place it in the same directory as the Java file):

```html
<!DOCTYPE html>
<html lang="en">
<head><title>Test Page</title></head>
<body>
<nav>
    <a href="/home" data-role="main">Home</a>
    <a href="/about" data-role="secondary">About</a>
    <a href="/contact">Contact</a>
</nav>
<img src="logo.png" alt="Company Logo">
<img src="banner.jpg">
<img src="icon.png" alt="Icon">
</body>
</html>
```

Running `mvn compile exec:java -Dexec.mainClass=CssXPathDemo` yields the expected counts shown earlier.

---

## Edge Cases & Common Questions

### What if the HTML file is malformed?

Both the CSS and XPath engines are tolerant of minor markup errors (missing closing tags, unquoted attributes). However, severe malformations may cause the parser to abort. In production, wrap the loading step in a try‑catch block and log the exception.

### Can I combine CSS and XPath in a single expression?

Not directly; each engine has its own syntax. The typical pattern is to use the one that expresses the condition most naturally (CSS for structural queries, XPath for attribute functions) and then merge the results in Java if needed.

### How do I count elements across multiple files?

Just place the loading logic inside a loop:

```java
for (Path p : Files.newDirectoryStream(Paths.get("html_folder"), "*.html")) {
    HTMLDocument doc = new HTMLDocument(p.toString());
    // repeat the queries...
}
```

### Does this work with Java 8?

Yes—provided you use a library version that targets Java 8 or higher. The code shown does not rely on newer language features.

---

## Conclusion

We’ve demonstrated **how to use CSS** selectors alongside **evaluate xpath java** expressions to **load an HTML file**, **count links**, and **count html elements** that meet specific criteria. The key takeaways are:

- Load the document once with `HTMLDocument`.  
- Leverage CSS4 for straightforward structural queries (`nav a[data-role]`).  
- Harness XPath 3.1 for powerful attribute functions (`ends-with(@src, '.png')`).  
- Retrieve the `NodeList` length to get exact counts.  

From here you can expand the script: add more selectors, write results to a CSV, or integrate it into a larger crawling pipeline. The combination of CSS and XPath gives you the flexibility to tackle virtually any HTML‑scraping challenge.

Ready to experiment? Try swapping the CSS selector for `section article[data-id]` or change the XPath to target `<video>` tags with a specific codec. The sky’s the limit.

If you found this guide helpful, feel free to share it, star the repository, or drop a comment with your own use‑cases. Happy coding!

![how to use css example diagram](https://example.com/diagram.png "how to use css example")

---


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}