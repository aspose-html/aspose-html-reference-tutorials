---
category: general
date: 2026-04-23
description: How to use querySelectorAll in Java to filter elements by class, read
  attribute values, and iterate NodeList for product data extraction.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: en
og_description: How to use querySelectorAll in Java to filter elements by class, read
  attribute values, and iterate NodeList for product data extraction.
og_title: How to Use querySelectorAll in Java – Filter by Class
tags:
- Java
- HTML parsing
- DOM manipulation
title: How to Use querySelectorAll in Java – Filter by Class
url: /java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use querySelectorAll in Java – Filter by Class

How to use querySelectorAll in Java is the key when you need to grab specific elements from an HTML document. In this tutorial we’ll filter elements by class, read attribute values, and iterate a NodeList to pull product prices from a catalog page.  

Ever found yourself staring at a massive HTML file, wondering how to pull only the “on‑sale” cards without writing a custom parser? That’s exactly the problem we’ll solve here—no extra libraries beyond Aspose.HTML, and a handful of straightforward steps.

You’ll walk away with a complete, runnable program that:

* **Selects elements** using a CSS selector (`select elements css selector`),
* **Filters by class** (`filter elements by class`),
* **Reads a custom attribute** (`how to read attribute`),
* **Iterates the resulting NodeList** (`iterate nodelist java`).

No prior experience with Aspose.HTML is required—just a basic Java setup and an HTML file to test against.

![how to use querySelectorAll in Java example](https://example.com/images/queryselectorall-java.png "how to use querySelectorAll in Java")

---

## What You’ll Need

| Requirement | Why it matters |
|-------------|----------------|
| **Java 17+** | Modern language features and better module handling. |
| **Aspose.HTML for Java** (latest version) | Provides the `Document` class and CSS‑selector engine. |
| **catalog.html** (sample HTML) | The source we’ll query against. |
| **IDE or plain `javac`** | To compile and run the demo. |

If you haven’t added Aspose.HTML to your project yet, drop the JAR into your `libs` folder and add it to the classpath:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Step 1 – Load the HTML Document

Before you can query anything, you need a `Document` object that represents the HTML file. Think of it as loading a spreadsheet before you can read any cells.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Why this matters:** The `Document` class parses the markup into a DOM tree, enabling the CSS‑selector engine to work. Skipping this step would leave you with a plain string and no way to use `querySelectorAll`.

---

## Step 2 – Select Elements with a CSS Selector

Now comes the heart of the matter: **how to use querySelectorAll**. The method accepts any valid CSS selector, so you can be as precise—or as broad—as you like. For our scenario we want product cards that:

* have the class `product-card`,
* are also marked with the class `sale`,
* and carry a `data-price` attribute.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Explanation:**  
> * `.product-card.sale` → filters elements that contain **both** classes.  
> * `[data-price]` → ensures the attribute exists, effectively **filtering elements by class** **and** attribute in a single call.  
> * The result is a `NodeList`, which is an ordered collection you can iterate over.

If you ever need to **select elements css selector** for a different pattern, just change the string—no code rewrite required.

---

## Step 3 – Iterate the NodeList in Java

A `NodeList` behaves a lot like an array, but it doesn’t implement `Iterable`. That’s why we use a classic `for` loop—perfect for **iterate nodelist java** scenarios.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Why a `for` loop?**  
> It gives you direct access to the index, which can be handy for logging or conditional branching. If you prefer a `while` loop, the logic stays identical—just change the loop construct.

---

## Step 4 – Read the `data-price` Attribute

Now we finally answer **how to read attribute** values from an element. In the DOM API, `getAttribute` returns the raw string, exactly as it appears in the markup.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Tip:** If the attribute might be missing, `getAttribute` returns `null`. You can guard against that with a simple check:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Step 5 – Output the Results

Last but not least, we print each price to the console. This mirrors a real‑world scenario where you’d probably push the values into a database or an API payload.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Expected Console Output

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

If the selector finds no matching nodes, the loop simply never runs—no exception is thrown. That’s a nice safety net for **edge cases** where the catalog might be empty.

---

## Full Working Example

Putting it all together, here’s the complete file you can copy‑paste into `CssSelectorDemo.java`:

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

Save the file, compile, and run—watch the prices stream out. 🎉

---

## Common Questions & Pro Tips

| Question | Answer |
|----------|--------|
| *What if I need to select by tag name too?* | Just prepend the tag: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Can I chain multiple attribute filters?* | Absolutely. Example: `[data-price][data-stock]` will keep only elements that have **both** attributes. |
| *Is `querySelectorAll` case‑sensitive?* | Yes—CSS selectors treat class and attribute names as case‑sensitive in HTML5. |
| *How do I handle a huge HTML file?* | Aspose.HTML streams the document, but you can also limit the selector to a subtree (`someElement.querySelectorAll(...)`). |
| *What

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}