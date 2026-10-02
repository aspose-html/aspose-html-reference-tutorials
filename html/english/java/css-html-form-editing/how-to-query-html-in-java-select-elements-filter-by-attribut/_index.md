---
category: general
date: 2026-02-16
description: How to query HTML using Aspose.HTML for Java. Learn to select HTML elements,
  filter elements by attribute, iterate over NodeList, and get text content in a few
  steps.
draft: false
keywords:
- how to query html
- select html elements
- get text content
- iterate over nodelist
- filter elements by attribute
language: en
og_description: How to query HTML with Aspose.HTML for Java. This tutorial shows how
  to select HTML elements, filter by attribute, iterate over NodeList, and get text
  content.
og_title: How to query HTML in Java – Complete Guide
tags:
- Java
- Aspose.HTML
- DOM manipulation
title: How to query HTML in Java – Select elements, filter by attribute, and get text
  content
url: /java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to query HTML in Java – Complete Guide

Ever wondered **how to query HTML** when you need to pull data from a static page? Maybe you’re building a price‑monitoring tool or scraping product listings for a catalog. In either case, you’ll soon discover that selecting the right nodes and extracting their text is the core of the job.  

In this tutorial we’ll walk through a real‑world example that **selects HTML elements**, **filters elements by attribute**, **iterates over a NodeList**, and finally **gets text content** from each match. By the end you’ll have a ready‑to‑run Java program that prints every product title whose price is over 100 USD.

> **Pro tip:** Aspose.HTML for Java makes CSS‑style selectors feel native, so you don’t need a separate parsing library.

---

## What You’ll Need

- **Java 17** (or any recent JDK) – the API works with Java 8+ but newer versions give you better performance.
- **Aspose.HTML for Java** JARs – you can download the free trial from the Aspose website or add the Maven dependency.
- A simple **catalog.html** file containing product cards with a `data-price` attribute (we’ll show a snippet below).

No other frameworks are required; the code runs as a plain Java application.

---

## Step 1: Load the HTML document from disk  

The first thing you have to do is tell Aspose.HTML where your source file lives. The `Document` class represents the whole DOM tree, just like a browser would build it.

```java
import com.aspose.html.dom.*;
import com.aspose.html.load.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document from a local file
        Document htmlDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Why this matters:** Loading the document creates a live DOM, which lets you run CSS selectors later. If the file isn’t found, Aspose throws a clear `FileNotFoundException`, so you’ll know exactly what to fix.

---

## Step 2: Filter elements by attribute – select high‑priced product cards  

Now we want only those `.product‑card` elements whose `data-price` attribute exceeds 100. The selector `.product-card[data-price>100]` does exactly that.

```java
        // Select product cards where data-price > 100
        NodeList highPricedCards = htmlDoc.querySelectorAll(".product-card[data-price>100]");
```

> **How it works:**  
> - `.product-card` matches any element with that class.  
> - `[data-price>100]` is an attribute filter that keeps only nodes whose `data-price` numeric value is greater than 100.  
> This is the same syntax you’d use in a browser’s DevTools console, making it intuitive for front‑end developers.

---

## Step 3: Iterate over NodeList and get text content  

A `NodeList` behaves like an array‑like collection, but you still need a loop to walk through each element. Inside the loop we’ll **select a child element** (`.title`) and read its text, then pull the price from the attribute.

```java
        // Loop through each matching card
        for (Node node : highPricedCards) {
            Element cardElement = (Element) node; // cast to Element for convenience

            // Get the product title text
            String productTitle = cardElement.querySelector(".title").getTextContent();

            // Retrieve the raw price from the attribute
            String productPrice = cardElement.getAttribute("data-price");

            // Output the result
            System.out.println(productTitle + " – $" + productPrice);
        }
    }
}
```

**Expected output** (assuming the HTML contains two qualifying cards):

```
Deluxe Coffee Maker – $149
Smart LED TV – $799
```

> **Common pitfall:** If a card doesn’t contain a `.title` element, `querySelector` returns `null` and calling `getTextContent()` would throw a `NullPointerException`. A defensive check (`if (titleElement != null)`) is advisable for production code.

---

## Step 4: Full, runnable example  

Putting everything together, here’s the complete program you can copy‑paste into your IDE. Remember to replace `YOUR_DIRECTORY/catalog.html` with the actual path to your HTML file.

```java
import com.aspose.html.dom.*;
import com.aspose.html.load.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document from a file
        Document htmlDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select product cards whose data-price attribute is greater than 100
        NodeList highPricedCards = htmlDoc.querySelectorAll(".product-card[data-price>100]");

        // Step 3: Iterate over the matching elements and extract title and price
        for (Node node : highPricedCards) {
            Element cardElement = (Element) node;
            String productTitle = cardElement.querySelector(".title").getTextContent();
            String productPrice = cardElement.getAttribute("data-price");

            // Step 4: Output the product information
            System.out.println(productTitle + " – $" + productPrice);
        }
    }
}
```

Save the file as `CssSelectorDemo.java`, compile with `javac`, and run `java CssSelectorDemo`. If everything is set up correctly, you’ll see the high‑priced products printed to the console.

---

## Step 5: Understanding the underlying concepts  

### Selecting HTML elements  

The `querySelectorAll` method accepts any valid CSS selector. That means you can combine class names, IDs, attribute filters, pseudo‑classes, and even descendant selectors. For example, `".category[data-active=true] a[href]"` would fetch all links inside active categories.

### Getting text content  

`Element.getTextContent()` returns the concatenated text of the element and its descendants, stripping away HTML tags. It’s the most reliable way to fetch visible text, unlike `innerHTML` which includes markup.

### Iterating over NodeList  

A `NodeList` implements `Iterable<Node>`, so you can use the enhanced `for‑each` loop shown above. If you need index‑based access, you can call `item(int index)` or convert it to a `List<Node>`.

### Filtering elements by attribute  

Attribute selectors support operators like `=`, `~=`, `|=`, `^=`, `$=`, `*=` and the numeric comparison operators (`>`, `<`, `>=`, `<=`). This gives you fine‑grained control without writing extra Java code.

---

## Step 6: Edge cases and variations  

- **Numeric vs. string comparison:** The selector `[data-price>100]` works because the attribute value can be parsed as a number. If your attribute contains non‑numeric characters (e.g., `"100USD"`), the comparison will fail. Strip the units first or use a custom filter in Java.
- **Case‑sensitive class names:** CSS selectors are case‑sensitive in XML mode. Make sure the class names in your HTML match exactly.
- **Multiple matches per card:** If a card contains several `.title` elements, `querySelector` returns the first one. Use `querySelectorAll(".title")` and loop if you need all titles.

---

## Step 7: Next steps – what else can you do?  

Now that you’ve mastered **how to query HTML**, consider extending the script:

1. **Write results to a CSV** – useful for feeding data into spreadsheets.
2. **Combine with HTTP client** – fetch remote pages on the fly using `java.net.http.HttpClient`.
3. **Apply more complex filters** – e.g., select items on sale (`[data-discount>0]`) or sort by price using Java streams.
4. **Integrate with a database** – store extracted products in SQLite or MySQL for later analysis.

All of these ideas reuse the same core concepts: **select HTML elements**, **filter elements by attribute**, **iterate over NodeList**, and **get text content**.

---

## Conclusion  

We’ve covered **how to query HTML** with Aspose.HTML for Java from start to finish. By loading a document, using a CSS selector that filters on `data-price`, looping through the resulting `NodeList`, and extracting both the title and price, you now have a solid pattern you can adapt to any scraping or data‑extraction task.

Give the code a spin, tweak the selector to match your own markup, and watch as the data flows out of the page and into your Java app. Happy coding!

---

![how to query html example](/images/query-html-example.png "how to query html example")

*Image shows console output of the program, illustrating the extracted product titles and prices.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}