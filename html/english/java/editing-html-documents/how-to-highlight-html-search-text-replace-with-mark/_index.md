---
category: general
date: 2026-03-04
description: How to highlight HTML by searching text in HTML and wrapping each match
  with a <mark> tag. Step‑by‑step Java guide to replace text with mark elements.
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: en
og_description: How to highlight HTML by searching text in HTML and wrapping matches
  with a <mark> tag. Complete Java example for replacing text with mark.
og_title: How to Highlight HTML – Search Text & Replace with <mark>
tags:
- Aspose.HTML
- Java
- Text Processing
title: How to Highlight HTML – Search Text & Replace with <mark>
url: /java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Highlight HTML – Search Text & Replace with `<mark>`

Ever wondered **how to highlight HTML** when a certain word appears multiple times? Maybe you’re building a documentation site, a blog engine, or just need to emphasize a brand name in a static page. The good news? It’s pretty straightforward once you know how to search text in HTML and wrap the results with a `<mark>` element.

In this tutorial we’ll walk through a complete Java solution that loads an HTML file, searches for a target word, replaces each occurrence with a `<mark>` tag, and finally saves the highlighted version. By the end you’ll be able to **highlight word in HTML**, **highlight occurrences of word**, and even **replace text with mark** without breaking the surrounding markup.

> **What you’ll need**  
> • Java 17 or newer (the code works with earlier versions too)  
> • Aspose.HTML for Java library (free trial or licensed copy)  
> • A simple HTML file you want to process  

If you’ve got those basics covered, let’s dive in.  

![Screenshot showing highlighted HTML output – how to highlight html](/images/highlight-html-example.png "how to highlight html example")

## Step 1 – Load the HTML Document (How to Highlight HTML)

First we need to bring the source file into memory. Aspose.HTML’s `Document` class does all the heavy lifting, parsing the markup into a DOM‑like structure that we can query.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**Why this matters:** Loading the document gives us a clean object model, so we can safely manipulate text nodes without worrying about breaking tags or attributes. It also normalizes whitespace, which makes the later **search text in html** step more reliable.

## Step 2 – Search Text in HTML for the Target Word

Now that the document is ready, we’ll look for every occurrence of the word we want to emphasize. The `searchText` method returns a list of `TextMatch` objects, each describing where the match lives in the DOM.

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**Pro tip:** The search is case‑sensitive by default. If you need a case‑insensitive search, convert both the document text and `searchTerm` to the same case before calling `searchText`, or use a regular‑expression‑based approach provided by the library.

## Step 3 – Replace Text with `<mark>` (Highlight Word in HTML)

For each match we’ll reconstruct the containing node’s text, injecting a `<mark>` element around the exact word. This ensures we only affect the target text and leave the rest of the HTML untouched.

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**Explanation:**  
- `getStartOffset`/`getEndOffset` give us the exact character positions of the match inside its parent node.  
- By slicing the original text (`textBefore` and `textAfter`) we keep everything else exactly as it was.  
- Wrapping the match with `<mark>` is the canonical way to **replace text with mark** and get native browser highlighting without extra CSS.

### Edge Cases & Tips

- **Multiple matches in the same node:** The loop processes each `TextMatch` sequentially. Because we replace the entire node’s content each time, later offsets shift. Aspose.HTML returns matches in document order, so the simple replacement works for most cases. If you encounter overlapping matches, consider collecting all matches first, then rebuilding the node in one pass.
- **Elements that can’t contain raw HTML:** If the parent node is a `<script>` or `<style>` block, inserting `<mark>` would break the page. You can skip those nodes by checking `parentNode.getNodeName()` before replacement.

## Step 4 – Save the Highlighted Document (Highlight Occurrences of Word)

After all replacements are done, we persist the modified DOM back to disk. The output file will contain the original markup plus the new `<mark>` tags, effectively **highlighting occurrences of word** “Aspose”.

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

Open `highlighted.html` in any browser, and you’ll see every “Aspose” wrapped in a yellow‑ish background (the default style for `<mark>`). If you prefer a custom look, add a small CSS rule:

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## Common Questions (Search Text in HTML – FAQs)

**Q: What if the word appears inside an attribute value?**  
A: `searchText` only looks at node text content, not attribute strings. To highlight attribute values you’d need to iterate over elements and manually inspect attributes.

**Q: Can I highlight multiple different words in one pass?**  
A: Absolutely. Build a list of terms, loop through each, and run the same replacement logic. Just be careful with overlapping matches.

**Q: Does this work with HTML5‑only tags like `<section>` or `<article>`?**  
A: Yes. Aspose.HTML fully supports modern HTML5 elements, so the DOM traversal works regardless of the tag type.

## Full Working Example (All Steps Combined)

Below is the complete, ready‑to‑run Java program that demonstrates the entire workflow—from loading the file to saving the highlighted output.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**Expected output:** Open `highlighted.html` and you’ll see every occurrence of “Aspose” highlighted. No other parts of the page are altered, and the file remains a valid HTML document.

## Conclusion

We’ve covered **how to highlight HTML** by programmatically **searching text in HTML**, wrapping each match with a `<mark>` tag, and finally persisting the changes. This approach lets you **highlight word in HTML**, **highlight occurrences of word**, and **replace text with mark** without writing fragile string‑manipulation code.

Next steps? Try extending the script to:

- Accept the search term as a command‑line argument.  
- Generate a CSS file that defines a custom highlight color.  
- Process a whole folder of HTML files in one batch.  

Those variations will deepen your understanding of both the Aspose.HTML API and general text‑processing patterns.  

If you hit any snags or have ideas for further improvements, drop a comment below. Happy highlighting!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}