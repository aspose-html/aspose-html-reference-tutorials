---
category: general
date: 2026-10-28
description: How to read HTML in Java and extract text from HTML files. Learn to convert
  HTML to text with Jsoup, covering read html from file and html to text java techniques.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: en
lastmod: 2026-10-28
og_description: How to read HTML in Java and extract text from HTML files. This tutorial
  shows a complete solution for convert HTML to text using Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: How to read HTML and extract text in Java – quick guide
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: How to read HTML and extract text in Java – a step‑by‑step guide
url: /java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to read HTML and extract text in Java – a step‑by‑step guide

If you need to **how to read html** from a local file, this guide provides a complete solution. You will learn to load an HTML document, extract the plain text, and optionally convert HTML to text with fine‑grained control. By the end of the tutorial you can run the example code and see the extracted text printed on the console.

Reading HTML files is a common task when processing web‑scraped data, generating reports, or cleaning up user‑generated content. The steps below cover everything you need, from adding the required library to handling edge cases such as malformed markup or character‑encoding issues.

## What you’ll need

- Java 17 or newer (the code compiles with earlier versions as well)
- Maven or Gradle for dependency management, or the Jsoup JAR added manually
- An HTML file named `input.html` placed in the project’s `src/main/resources` directory (you can change the path later)

## Set up the Jsoup library

Jsoup is a lightweight, well‑documented library that parses HTML into a DOM‑like structure. It handles broken HTML gracefully, which makes it ideal for **extract text from html** tasks.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

If you prefer a manual download, place the JAR on your classpath and import `org.jsoup.*` in your source file.

## Load HTML from a file

The first programmatic step is to read the file into a `Document` object. Jsoup offers a static `parse` method that accepts a `File` and a charset name.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Why this matters:** `Jsoup.parse(File, String)` reads the raw bytes, decodes them according to the supplied charset, and builds a clean DOM. This approach is safer than reading the file into a string yourself because Jsoup normalizes line endings and fixes common markup errors automatically.

## Extract plain text from the HTML

Once you have a `Document`, retrieving the visible text is a single method call. The `text()` method concatenates the textual content of all elements while discarding tags, scripts, and styles.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

The `body()` call limits the extraction to the `<body>` element, which is the typical target when you **read html from file** for content analysis. The resulting string contains whitespace collapsed to single spaces, mimicking how a browser would render the text.

### Expected output

Assuming `input.html` contains:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

Running the program prints:

```
Extracted text:
Hello World This is a demo page.
```

## Convert HTML to text with additional options

Sometimes you need more control than `text()` provides—e.g., preserving line breaks, keeping list numbering, or ignoring certain tags. Jsoup’s `NodeTraversor` combined with a custom `NodeVisitor` gives you that flexibility.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Replace the simple `doc.body().text()` call with:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Why this works:** The visitor walks the DOM depth‑first, appending a newline before each block‑level element (e.g., `<p>`, `<div>`, `<h1>`). This keeps paragraph separation, which is useful when you **convert html to text** for readability or downstream NLP pipelines.

## Common pitfalls and best practices

| Issue | Why it occurs | Recommended fix |
|-------|---------------|-----------------|
| Wrong charset | Files saved in ISO‑8859‑1 but parsed as UTF‑8 produce garbled characters. | Detect the charset from the file’s meta tag (`<meta charset="...">`) or pass the correct name to `Jsoup.parse`. |
| Large files | Loading a very large HTML file into memory can cause `OutOfMemoryError`. | Stream the file with `Jsoup.parse(File, String, String baseUri)` and process nodes incrementally, or increase the JVM heap size. |
| Unwanted script/style text | `text()` removes script and style content, but custom visitors may unintentionally include it. | Skip nodes whose tag name is `script` or `style` inside the visitor’s `head` method. |
| Preserving whitespace | Collapsing spaces may lose formatting needed for markdown conversion. | Use `Element.wholeText()` for raw text nodes, then post‑process whitespace manually. |

Addressing these concerns ensures your **html to text java** solution works reliably across diverse inputs.

## Full runnable example

Below is a self‑contained program that demonstrates the entire workflow—from dependency setup to output verification. Copy the code into a file named `HtmlToTextDemo.java`, place an `input.html` file alongside it, and run `javac && java` as shown.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Running the program

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

The console displays both the simple extraction and the detailed


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use XPath in Java – Read HTML and Extract Text](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Extract text from HTML with Java – Complete Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}