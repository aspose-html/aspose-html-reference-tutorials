---
category: general
date: 2026-04-11
description: Select div by class using Java – learn how to load HTML, wait for HTML
  load, and evaluate XPath Java efficiently.
draft: false
keywords:
- select div by class
- load html java
- java xpath nodeset
- wait for html load
- evaluate xpath java
language: en
og_description: Select div by class using Java – learn how to load HTML, wait for
  HTML load, and evaluate XPath Java efficiently.
og_title: Select div by class in Java – Complete XPath Guide
tags:
- Java
- XPath
- Aspose.HTML
title: Select div by class in Java – Complete XPath Guide
url: /java/creating-managing-html-documents/select-div-by-class-in-java-complete-xpath-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Select div by class in Java – Complete XPath Guide

Ever needed to **select div by class** in a Java project but weren’t sure which API would give you a reliable result? You’re not alone. Most developers hit the same wall when they try to parse an HTML file, wait for it to load, and then run an XPath expression that returns a `NodeSet`.  

In this tutorial we’ll walk through the exact steps to **load HTML in Java**, make sure the document is fully ready (yes, *wait for HTML load*), and finally **evaluate XPath Java** to pull out every `<div>` whose `class` attribute equals `"test"`. By the end you’ll have a ready‑to‑run code sample, a clear explanation of why each line matters, and a few tips to avoid common pitfalls.

---

## What You’ll Build

- Load an HTML file using Aspose.HTML for Java.  
- Pause execution until the document finishes loading.  
- Run a higher‑order XPath function (`filter`) that returns a **Java XPath NodeSet** of matching `<div>` elements.  
- Print the number of matches to the console.

No external libraries beyond Aspose.HTML are required, and the code works on Java 17 and newer.

---

## Prerequisites

- Java Development Kit (JDK) 17+ installed.  
- Aspose.HTML for Java JAR on your classpath (you can grab it from Maven Central).  
- A small `data.html` file containing some `<div class="test">` elements – we’ll create one in the next step.

---

## Step 1: Load HTML in Java with Aspose.HTML

The first thing you need is a valid `HTMLDocument` object. Aspose.HTML makes this a one‑liner, but you still have to point it at the right file path.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class XPath31Demo {
    public static void main(String[] args) throws Exception {

        // 👉 Step 1: Load the HTML document from disk
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/data.html");
```

**Why this matters:**  
`HTMLDocument` parses the file and builds a DOM tree that XPath can query later. If the file isn’t found, Aspose throws a `FileNotFoundException`, so double‑check the path or use an absolute reference.

---

## Step 2: Wait for HTML Load Before Querying

HTML parsing can be asynchronous, especially when the document contains external resources (scripts, images, etc.). Calling `waitForLoad()` guarantees the DOM is fully built.

```java
        // 👉 Step 2: Ensure the document is fully loaded before querying
        htmlDoc.waitForLoad();
```

**Pro tip:**  
Skipping `waitForLoad()` might give you an empty `NodeSet` because the parser hasn’t finished. In headless environments this call is practically free, so always include it.

---

## Step 3: Evaluate XPath Java to Get a NodeSet

Now we unleash the power of XPath 3.1’s `filter()` function. It iterates over all `<div>` elements and keeps only those whose `@class` equals `"test"`.

```java
        // 👉 Step 3: Use a higher‑order XPath function to select <div> elements with class="test"
        NodeList matchingDivs = htmlDoc.evaluate(
                "filter(//div, function($n){$n/@class='test'})",
                htmlDoc,
                XPathResultType.NODESET
        ).getNodeSet();
```

**Breakdown of the expression:**

| Part | Explanation |
|------|-------------|
| `//div` | Selects every `<div>` in the document. |
| `filter(..., function($n){...})` | Applies a lambda‑style function to each node `$n`. |
| `$n/@class='test'` | Returns `true` only when the `class` attribute equals `"test"`. |
| `XPathResultType.NODESET` | Tells Aspose we expect a collection of nodes. |

Because we asked for a **Java XPath NodeSet**, the result comes back as a `NodeList`, which we can iterate or query further.

---

## Step 4: Output the Result – Verify Your Query

Finally, let’s print how many `<div class="test">` elements we found.

```java
        // 👉 Step 4: Output the number of matching elements found
        System.out.println("Found " + matchingDivs.getLength() + " matching div(s).");
    }
}
```

**Expected output** (assuming `data.html` contains three matching divs):

```
Found 3 matching div(s).
```

If you see `0`, double‑check the class name spelling, the HTML file location, and whether you called `waitForLoad()`.

---

## Full Working Example

Below is the complete, copy‑paste‑ready program. Replace `YOUR_DIRECTORY` with the actual folder that holds `data.html`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class XPath31Demo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/data.html");

        // Step 2: Ensure the document is fully loaded before querying
        htmlDoc.waitForLoad();

        // Step 3: Use a higher‑order XPath function to select <div> elements with class="test"
        NodeList matchingDivs = htmlDoc.evaluate(
                "filter(//div, function($n){$n/@class='test'})",
                htmlDoc,
                XPathResultType.NODESET
        ).getNodeSet();

        // Step 4: Output the number of matching elements found
        System.out.println("Found " + matchingDivs.getLength() + " matching div(s).");
    }
}
```

> **Tip:** If you need to process each matching node (e.g., extract inner text), simply loop over `matchingDivs`:

```java
for (int i = 0; i < matchingDivs.getLength(); i++) {
    Element div = (Element) matchingDivs.item(i);
    System.out.println(div.getTextContent());
}
```

---

## Common Variations & Edge Cases

### Selecting Multiple Classes

If a `<div>` can have several classes (e.g., `class="test primary"`), change the XPath predicate to use `contains()`:

```xpath
filter(//div, function($n){contains($n/@class, 'test')})
```

### Case‑Insensitive Matching

XPath 3.1 doesn’t have a built‑in case‑insensitive operator, but you can normalize both sides:

```xpath
filter(//div, function($n){lower-case($n/@class) = 'test'})
```

### Large Documents

When parsing massive HTML files, consider streaming the document or increasing the JVM heap (`-Xmx2g`). The `waitForLoad()` call still works; it just waits longer.

---

## Pro Tips & Gotchas

- **Avoid hard‑coded paths.** Use `Paths.get("data.html").toAbsolutePath()` for portability.  
- **Check the Aspose.HTML version.** The `filter()` function is only available from version 22.7 onward.  
- **Remember to close resources.** `htmlDoc.dispose();` releases native memory—especially important in long‑running services.  
- **Debugging XPath:** If you’re unsure why a node isn’t selected, drop a simple `//div` query first and print the length; then refine the predicate.

---

## Image Illustration

![Select div by class example diagram](select-div-by-class.png "Diagram showing the flow from loading HTML to evaluating XPath and retrieving matching divs")

*Alt text:* select div by class example diagram illustrating load HTML, wait for HTML load, evaluate XPath Java, and retrieve a Java XPath NodeSet.

---

## Conclusion

We’ve just demonstrated how to **select div by class** in Java using Aspose.HTML, ensuring the document is fully loaded, and retrieving a **Java XPath NodeSet** with a concise `filter()` expression. The approach is fast, type‑safe, and works with modern XPath 3.1 features, making it a solid choice for any HTML‑parsing task.

Next steps? Try swapping the predicate for other attributes, experiment with `map` or `for-each` XPath functions, or integrate this snippet into a larger web‑scraping pipeline. You now have the building blocks to **load HTML Java**, **wait for HTML load**, and **evaluate XPath Java** like a pro.

Happy coding, and feel free to drop your questions in the comments—no problem is too small when it comes to mastering XPath in Java!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}