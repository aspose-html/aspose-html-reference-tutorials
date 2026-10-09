---
category: general
date: 2026-10-09
description: Learn how to create HTML, how to add body, and how to insert paragraph
  using Python. Step‑by‑step code shows how to set text and how to append child elements.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to create html
- how to add body
- how to insert paragraph
- how to set text
- how to append child
language: en
lastmod: 2026-10-09
og_description: How to create HTML with Python. Follow this tutorial to learn how
  to add body, how to insert paragraph, how to set text, and how to append child elements.
og_image_alt: Diagram illustrating how to create HTML using Python’s xml.dom.minidom
og_title: How to create HTML programmatically – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn how to create HTML, how to add body, and how to insert paragraph
    using Python. Step‑by‑step code shows how to set text and how to append child
    elements.
  headline: How to create HTML programmatically – a complete guide
  type: TechArticle
tags:
- HTML generation
- Python
- DOM manipulation
title: How to create HTML programmatically – a complete guide
url: /python/general/how-to-create-html-programmatically-a-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create HTML programmatically – a complete guide

If you need to **how to create html** from scratch, this tutorial shows you exactly that. You’ll also discover **how to add body**, **how to insert paragraph**, **how to set text**, and **how to append child** elements using Python’s standard library. By the end of the guide you have a fully‑formed HTML document you can save to disk or embed in a web response.

Creating HTML programmatically removes the risk of manual typing errors and lets you generate dynamic markup based on data. The steps below work with Python 3.11 or newer and require no third‑party packages, so you can run the code in any environment that supports the standard library.

## Prerequisites

- Python 3.11+ installed
- Basic familiarity with Python functions and objects
- An editor or IDE for running scripts (e.g., VS Code, PyCharm, or a simple terminal)

No external libraries are required because the solution uses `xml.dom.minidom`, which is part of Python’s built‑in `xml` package.

## How to create HTML with Python’s xml.dom.minidom

The first step is to import the DOM implementation and create a new document object. This document will serve as the container for all subsequent nodes.

```python
"""Create a minimal HTML document using xml.dom.minidom."""
from xml.dom.minidom import Document

def build_html():
    # Step 1: Create a new HTML document
    doc = Document()
    # The document itself does not contain any elements yet.
    return doc
```

*Why this matters:* `Document()` gives you a clean slate that follows the W3C DOM specification, making it easy to **how to create html** structures that are well‑formed and serializable.

## How to add body to the document

After the `<html>` root element is created, you need a `<body>` element where visible content lives. This step demonstrates **how to add body** correctly.

```python
def add_body(doc: Document):
    # Step 2: Create the <html> root element and attach it to the document
    html_elem = doc.createElement('html')
    doc.appendChild(html_elem)

    # Step 2 continued: Add a <body> element to the document
    body_elem = doc.createElement('body')
    html_elem.appendChild(body_elem)   # This is how to append child elements
    return body_elem
```

*Why this matters:* The `<body>` tag is required for any visible markup. By using `appendChild`, you follow the DOM’s **how to append child** pattern, ensuring the hierarchy is preserved.

## How to insert paragraph into the body

With a `<body>` in place, you can now demonstrate **how to insert paragraph** elements. Paragraphs are the most common block‑level containers for text.

```python
def insert_paragraph(body_elem):
    # Step 3: Create a <p> element
    p_elem = body_elem.ownerDocument.createElement('p')
    body_elem.appendChild(p_elem)   # This shows how to append child again
    return p_elem
```

*Why this matters:* Inserting a `<p>` tag gives you a semantic container for text. Using `ownerDocument` guarantees the new element belongs to the same document, which is essential for a valid DOM tree.

## How to set text for the paragraph

Now that you have a `<p>` element, you need to place actual content inside it. This snippet explains **how to set text** for a DOM node.

```python
def set_paragraph_text(p_elem, text):
    # Step 4: Create a text node and attach it to the paragraph
    text_node = p_elem.ownerDocument.createTextNode(text)
    p_elem.appendChild(text_node)   # This is another example of how to append child
```

*Why this matters:* Text nodes are the only way to store raw characters inside an element. Using `createTextNode` follows the standard **how to set text** approach and avoids encoding issues.

## How to append child elements correctly (full example)

Putting the pieces together shows the complete **how to create html**, **how to add body**, **how to insert paragraph**, **how to set text**, and **how to append child** workflow in a single, runnable script.

```python
from xml.dom.minidom import Document

def build_html():
    # Create the document
    doc = Document()

    # Add <html> and <body>
    html_elem = doc.createElement('html')
    doc.appendChild(html_elem)

    body_elem = doc.createElement('body')
    html_elem.appendChild(body_elem)   # how to append child

    # Insert a paragraph
    p_elem = doc.createElement('p')
    body_elem.appendChild(p_elem)      # how to insert paragraph and how to append child

    # Set paragraph text
    text_node = doc.createTextNode('Hello, Aspose!')
    p_elem.appendChild(text_node)      # how to set text and how to append child

    return doc

if __name__ == '__main__':
    # Build the HTML document
    document = build_html()

    # Serialize to a pretty‑printed string
    html_string = document.toprettyxml(indent='  ', encoding='UTF-8')
    # Write to a file for inspection
    with open('output.html', 'wb') as f:
        f.write(html_string)

    print('HTML file "output.html" created successfully.')
```

**Expected output (`output.html`):**

```html
<?xml version="1.0" encoding="UTF-8"?>
<html>
  <body>
    <p>Hello, Aspose!</p>
  </body>
</html>
```

*Why this matters:* The script demonstrates every required operation in one place. You can run it as a standalone file, and the generated `output.html` can be opened in any browser to verify that the paragraph appears as expected.

## Common variations and edge cases

- **Adding multiple paragraphs:** Call `insert_paragraph` repeatedly and pass each new `<p>` to `set_paragraph_text`. Remember to **how to append child** each new node to the `<body>`.
- **Setting attributes (e.g., class or id):** Use `element.setAttribute('class', 'my-class')` before appending children. This does not affect the **how to set text** flow but enriches the markup.
- **Generating UTF‑8 characters:** The `toprettyxml` call already outputs UTF‑8. Ensure your source strings are Unicode literals (prefix with `u` in older Python versions) to avoid encoding errors.
- **Avoiding empty text nodes:** If you create a `<p>` without calling **how to set text**, the browser may render an empty line. Always attach a text node or remove the element if it remains empty.

## Pro tips

- **Reuse the document object:** Creating a new `Document` for every tiny snippet can be expensive. Keep a single document alive when generating large pages.
- **Validate the output:** Use `xml.dom.minidom.parseString` on the generated string to catch malformed markup early.
- **Performance tip:** For very large HTML files, consider streaming the output with `xml.sax` instead of building the entire DOM in memory.

## Conclusion

You now know **how to create html** using Python’s built‑in DOM API, **how to add body**, **how to insert paragraph**, **how to set text**, and **how to append child** elements in a clean, repeatable pattern. The complete example can be copied, modified, and integrated into web frameworks, email generators, or static site pipelines.

Next, explore related topics such as **how to add head elements**, **how to embed CSS**, and **how to generate tables with DOM**. Each of those builds on the same principles demonstrated here, so you can extend this foundation confidently.

Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create HTML and Add CSS Style Element – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/how-to-create-html-and-add-css-style-element-step-by-step-gu/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Append Child in Java DOM – Complete Aspose.HTML Guide](/html/english/java/editing-html-documents/how-to-append-child-in-java-dom-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}