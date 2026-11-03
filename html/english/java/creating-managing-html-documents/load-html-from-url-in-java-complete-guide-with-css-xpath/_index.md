---
category: general
date: 2026-07-02
description: Load HTML from URL using Aspose.HTML for Java, then select elements with
  attribute, extract download links, and count XPath nodes in a few easy steps.
draft: false
keywords:
- load html from url
- select elements with attribute
- extract download links
- search html with css
- count xpath nodes
language: en
og_description: Load HTML from URL in Java, then use CSS selectors and XPath to select
  elements with attribute, extract download links, and count XPath nodes.
og_title: Load HTML from URL in Java – Full CSS & XPath Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Load HTML from URL using Aspose.HTML for Java, then select elements
    with attribute, extract download links, and count XPath nodes in a few easy steps.
  headline: Load HTML from URL in Java – Complete Guide with CSS & XPath
  type: TechArticle
- description: Load HTML from URL using Aspose.HTML for Java, then select elements
    with attribute, extract download links, and count XPath nodes in a few easy steps.
  name: Load HTML from URL in Java – Complete Guide with CSS & XPath
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-html</artifactId>
      <version>23.10</version> <!-- Check for the latest version --> </dependency>
      ```'
  - name: Gradle
    text: '```gradle implementation ''com.aspose:aspose-html:23.10'' ```'
  - name: What the selector means
    text: '| Part | Meaning | |------|---------| | `a` | any `<a>` element | | `[href*=''download'']`
      | attribute `href` that **contains** the substring `download` (`*=` is the “contains”
      operator) |'
  - name: Expected console output (may vary by site)
    text: '``` Document loaded from https://example.com'
  type: HowTo
tags:
- Java
- Aspose.HTML
- Web Scraping
title: Load HTML from URL in Java – Complete Guide with CSS & XPath
url: /java/creating-managing-html-documents/load-html-from-url-in-java-complete-guide-with-css-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Load HTML from URL in Java – Complete Guide with CSS & XPath

Ever needed to **load HTML from URL** in a Java app and pull out specific links without writing a full‑blown web‑crawler? You're not alone. Whether you're building a download manager, a content aggregator, or just curious about the pages you visit, being able to fetch a page, **search HTML with CSS**, and then **count XPath nodes** is a handy skill to have.  

In this tutorial we’ll walk through the whole process: from pulling a remote page into memory, to using a CSS selector to **select elements with attribute**, extracting those **download links**, and finally verifying the same result with an XPath query. No external services, just pure Java and the Aspose.HTML for Java library.

> **Prerequisites** – You’ll need Java 8+ installed, Maven or Gradle for dependency management, and a basic understanding of HTML and Java syntax. If you’re new to Aspose.HTML, don’t worry; we’ll cover the setup step‑by‑step.

---

## What You’ll Build

By the end of this guide you’ll have a runnable Java class that:

1. **Loads HTML from a URL** (e.g., `https://example.com`).
2. **Searches the DOM with a CSS selector** to find every `<a>` tag whose `href` contains “download”.
3. **Extracts and prints each download link**.
4. **Runs an equivalent XPath query** and prints how many nodes were found.

You’ll also see a small diagram that visualizes the flow—just in case you’re a visual learner.

![Diagram showing the flow of loading HTML from URL, selecting elements, extracting links, and counting XPath nodes](load-html-from-url-diagram.png)

---

## Step 1: Add Aspose.HTML for Java to Your Project

First things first. Aspose.HTML is a commercial library, but it offers a free trial that works perfectly for learning purposes.

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

> **Pro tip:** If you hit a `NoClassDefFoundError` later, double‑check that the `aspose-html` jar is on your runtime classpath.

---

## Step 2: Load HTML from URL and Initialize the Document

Now that the library is on board, we can actually **load HTML from URL**. The `HTMLDocument` class accepts a string URL and takes care of the HTTP request, redirects, and character‑set detection for you.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class HtmlDownloader {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Define the target page
        String pageUrl = "https://example.com";

        // Step 2.2: Load the page into an HTMLDocument object
        HTMLDocument document = new HTMLDocument(pageUrl);

        System.out.println("Document loaded successfully.");
        // From here on we can query the DOM.
    }
}
```

**Why this works:** `HTMLDocument` internally creates an `HttpWebRequest`, follows redirects, and builds a DOM tree that behaves just like a browser’s `document`. That means we can use both CSS selectors and XPath straight away.

---

## Step 3: Search HTML with CSS – Select Elements with Attribute

The most readable way to locate elements is with a CSS selector. In our case we want every `<a>` whose `href` attribute contains the word “download”. The selector syntax `a[href*='download']` does exactly that.

```java
// Step 3: Find all anchor elements whose href contains "download"
NodeList downloadLinks = document.selectElements("a[href*='download']");

// Quick sanity check – how many did we find?
System.out.println("CSS found " + downloadLinks.getLength() + " nodes.");
```

### What the selector means

| Part | Meaning |
|------|---------|
| `a` | any `<a>` element |
| `[href*='download']` | attribute `href` that **contains** the substring `download` (`*=` is the “contains” operator) |

> **Edge case:** If the page uses relative URLs (e.g., `href="/files/download.zip"`), Aspose.HTML will keep them as‑is. You may need to resolve them against the base URL later.

---

## Step 4: Extract Download Links

Now that we have a `NodeList`, pulling out the actual URLs is trivial. We’ll cast each node to an `Element` and read its `href` attribute.

```java
System.out.println("\n--- Extracted Download Links ---");
for (int i = 0; i < downloadLinks.getLength(); i++) {
    Element anchor = (Element) downloadLinks.item(i);
    String href = anchor.getAttribute("href");
    // Resolve relative URLs to absolute ones (optional but handy)
    String absoluteHref = document.getBaseUrl().resolve(href).toString();
    System.out.println(absoluteHref);
}
```

**Result you’ll see** (sample output):

```
CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx
```

If you only need the raw attribute value, skip the `resolve` call. The resolution step is useful when you later feed those URLs into a downloader.

---

## Step 5: Search HTML with XPath – Count XPath Nodes

Sometimes you prefer XPath—especially when you need more complex hierarchical queries. The equivalent XPath expression for our CSS selector is:

```xpath
//a[contains(@href,'download')]
```

Let’s run it and see how many nodes we get.

```java
// Step 5: Perform the same search using XPath
NodeList xpathNodes = document.selectNodes("//a[contains(@href,'download')]");

// Output the count
System.out.println("\nXPath found " + xpathNodes.getLength() + " nodes.");
```

The output should match the CSS count, confirming that both approaches are equivalent:

```
XPath found 3 nodes.
```

> **Why both?** Using both selectors in the same codebase gives you flexibility. CSS is concise for simple attribute checks, while XPath shines when you need to navigate up/down the tree or combine multiple conditions.

---

## Step 6: Full Working Example

Putting everything together, here’s the complete class you can copy‑paste into your IDE and run immediately.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class QueryExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the HTML document from a web page
        String url = "https://example.com";
        HTMLDocument document = new HTMLDocument(url);
        System.out.println("Document loaded from " + url);

        // 2️⃣ Search HTML with CSS – select elements with attribute
        NodeList cssMatches = document.selectElements("a[href*='download']");
        System.out.println("\nCSS found " + cssMatches.getLength() + " nodes.");

        // 3️⃣ Extract download links
        System.out.println("\n--- Extracted Download Links ---");
        for (int i = 0; i < cssMatches.getLength(); i++) {
            Element anchor = (Element) cssMatches.item(i);
            String href = anchor.getAttribute("href");
            // Resolve relative URLs (optional)
            String absolute = document.getBaseUrl().resolve(href).toString();
            System.out.println(absolute);
        }

        // 4️⃣ Search HTML with XPath – count xpath nodes
        NodeList xpathMatches = document.selectNodes("//a[contains(@href,'download')]");
        System.out.println("\nXPath found " + xpathMatches.getLength() + " nodes.");
    }
}
```

### Expected console output (may vary by site)

```
Document loaded from https://example.com

CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx

XPath found 3 nodes.
```

Run the program, and you’ll instantly see all the links that contain “download”. Change the selector or XPath string to fit your own criteria—maybe `a[href$='.pdf']` for PDFs only, or `//div[@class='product']//a` for product pages.

---

## Common Pitfalls & How to Avoid Them

| Issue | Symptom | Fix |
|-------|----------|-----|
| **HTTPS certificate errors** | `javax.net.ssl.SSLHandshakeException` | Add a trust manager or use a URL with a valid cert. For quick testing, you can disable certificate validation, but never in production. |
| **Redirect loops** | Program hangs or throws `Too many redirects` | Set a reasonable redirect limit (`document.setRedirectLimit(5)`) or inspect the target URL manually. |
| **Relative URLs** | Extracted links start with `/` instead of full domain | Use `document.getBaseUrl().resolve(relative)` as shown in the example. |
| **Large pages** | High memory usage | Stream the response or use `HTMLDocument` overloads that limit DOM size. |
| **Missing Aspose license** | Runtime throws `LicenseException` after trial expires | Purchase a license or continue using the trial for non‑commercial experiments. |

---

## Next Steps & Related Topics

- **Download the files** – combine the extracted URLs with Java’s `HttpURLConnection` or Apache HttpClient to actually fetch the resources.
- **Parallel processing** – use `CompletableFuture` to download multiple files concurrently.
- **Advanced CSS selectors** – try `a[href$='.zip']` for file extensions, or `div[data-id]` to select elements with custom attributes.
- **XPath functions** – explore `starts-with()`, `ends-with()`, and logical operators (`and`, `or`) for more granular queries.
- **HTML sanitization** – if you plan to display the fetched HTML, consider using a library like Jsoup to clean it.

---

## Conclusion

We’ve just demonstrated how to **load HTML from URL** in Java, then **search HTML with CSS** to **select elements with attribute**, **extract download links**, and finally **count XPath nodes** to verify the result. The approach is compact, relies on a single library, and works for both simple scraping tasks and more sophisticated DOM analysis.  

Feel free to tweak the selectors


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Load HTML Documents from Stream with Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Handle Document Load Events in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}