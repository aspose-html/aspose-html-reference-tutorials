---
category: general
date: 2026-08-25
description: Learn how to create html document, select element css, modify html text
  and save html file using a simple Python script.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: en
lastmod: 2026-08-25
og_description: Create html document, select element css, modify html text and save
  html file in a few lines of Python. Follow this complete tutorial.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Create html document and edit its content with Python – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: How to create html document and edit its content in Python
url: /python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create html document and edit its content in Python

If you need to **create html document** from scratch and change its elements programmatically, this guide shows you exactly how. You’ll see a short, runnable script that creates a file, selects a paragraph with a CSS selector, updates the text, and writes the result back to disk.

Working with HTML in Python is common when generating reports, email templates, or static site content. By the end of this tutorial you will be able to **select element css**, **modify html text**, and **save html file** without leaving the comfort of your IDE.

## Prerequisites

Before you start, make sure you have:

* Python 3.9 or newer installed.
* The `beautifulsoup4` and `lxml` packages (install with `pip install beautifulsoup4 lxml`).
* Write permission to the directory where you plan to store the output file.

No additional tools are required; the standard library handles file I/O.

## Step 1: Install the required libraries

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` provides a convenient API for parsing and manipulating HTML, while `lxml` supplies a fast parser that understands CSS selectors.

## Step 2: Create the initial HTML document

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

The `BeautifulSoup` constructor builds a **create html document** object in memory. Using the `"lxml"` parser ensures full CSS selector support.

## Step 3: Select the paragraph element using a CSS selector

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

The `select_one` method implements **select element css** logic, returning the first matching tag. If the selector does not match anything, `para` will be `None`, so a defensive check is advisable in production code.

## Step 4: Modify the paragraph’s text content

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

Assigning to `para.string` performs a **modify html text** operation. BeautifulSoup updates the underlying DOM tree, so the change is reflected when the document is serialized.

## Step 5: Save the updated HTML to a file

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

The `open` call together with `write` implements **save html file** functionality. Using `prettify()` produces nicely indented output, which is helpful during debugging.

### Full script for quick copy‑paste

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

Running `python edit_html.py` creates `updated.html` containing:

```html
<p>
 New
</p>
```

## Common variations and edge cases

### Selecting multiple elements

If you need to **select element css** selectors that match several tags (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate over the list to apply changes to each element.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### Preserving existing attributes

When you replace the text, BeautifulSoup retains any attributes on the tag. For example:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### Handling missing elements gracefully

In production scripts, you often encounter malformed HTML. Wrap the selection in a conditional or try‑except block, as shown in Step 4, to avoid crashes.

### Writing to a specific directory

Replace `output_path` with an absolute or relative path:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

Make sure the directory exists; otherwise, Python will raise `FileNotFoundError`.

## Pro tips

* **Performance** – For large HTML files, prefer `lxml.etree` directly; BeautifulSoup adds a thin abstraction layer that is convenient but slightly slower.
* **Encoding** – Always open files with `encoding="utf-8"` to preserve non‑ASCII characters.
* **Testing** – After modification, you can verify the output with `assert "New" in open(output_path).read()` in a unit test.

## Conclusion

You now know how to **create html document**, use a **select element css** query to locate a node, **modify html text**, and finally **save html file** with Python. This pattern scales to more complex transformations such as bulk updates, attribute changes, or template generation.

Next, explore related topics like **how to edit html** using XPath expressions, generating full HTML pages with Jinja2, or automating batch processing of multiple files. Each of those builds on the core steps demonstrated here and expands your toolkit for programmatic HTML manipulation.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}