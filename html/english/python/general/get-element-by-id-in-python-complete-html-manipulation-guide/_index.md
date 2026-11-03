---
category: general
date: 2026-05-31
description: Learn how to get element by id, change background colour HTML, read HTML
  text and set HTML attribute using Python. Step‑by‑step tutorial.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: en
og_description: Get element by id, read HTML text, set HTML attribute and change background
  colour HTML using Python in a single, easy‑to‑follow guide.
og_title: Get element by id in Python – Full HTML Manipulation Tutorial
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: Get element by id in Python – Complete HTML Manipulation Guide
url: /python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get element by id in Python – Complete HTML Manipulation Guide

Ever needed to **get element by id** from an HTML page while writing a quick Python script? You’re not alone—most developers hit that exact roadblock when they start crawling sites or tweaking local reports. The good news? With a handful of lines of code you can read the element’s text, change its background colour, and even set new attributes, all without leaving your editor.

In this tutorial we’ll walk through a real‑world example: loading a local `sample.html`, pulling the element whose ID is `main‑content`, printing its inner text, and finally swapping the background colour to a light gray. By the end you’ll also know **how to read HTML text**, **how to set HTML attribute**, and why **manipulate HTML with Python** is a handy skill in any automation toolbox.

## What You’ll Need

Before we dive in, make sure you have:

- **Python 3.9+** (any recent version works)
- The **`lxml`** library (or **BeautifulSoup** if you prefer) – we’ll use `lxml.html` because it gives a clean `get_element_by_id`‑style API.
- A tiny HTML file named `sample.html` sitting in a folder called `YOUR_DIRECTORY`. Feel free to copy the snippet below into that file:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

That’s it—no fancy frameworks, just plain Python and a static HTML file.

## Step 1: Install the Required Library

If you haven’t installed `lxml` yet, fire up a terminal and run:

```bash
pip install lxml
```

*Pro tip:* Using a virtual environment keeps your global Python tidy, especially when you start juggling multiple projects.

## Step 2: Load the HTML Document

Now we’ll read the file into an `lxml.html` document object. Think of this as turning the raw text into a navigable tree.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

Running this prints “Document loaded successfully.” If the file can’t be found, Python will raise a `FileNotFoundError`—good to catch early before you chase a phantom element.

## Step 3: Get element by id

Here’s the heart of the matter. `lxml` gives us a convenient `get_element_by_id` method that mirrors the DOM API you’d use in JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

When the element exists, you’ll see “Element found!” printed to the console. This is the **get element by id** step that powers most of our later manipulations.

## Step 4: How to read HTML text

Once you have the element, extracting its visible text is a breeze. The `text_content()` method returns everything inside, stripped of tags.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Expected output:

```
Inner text: Hello, world! This is the original text.
```

You might wonder, *what if the element contains nested tags?* `text_content()` still works—it concatenates all descendant text nodes, giving you a clean string you can log, store, or feed into another algorithm.

## Step 5: How to set HTML attribute

Changing or adding attributes is just as straightforward. The `set` method lets you assign any attribute name you like.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Output:

```
New attribute value: true
```

That line demonstrates **how to set HTML attribute** on the fly. You can replace `"data-modified"` with `"class"`, `"title"` or any other attribute the element supports.

## Step 6: Change background colour HTML

Now for the visual tweak. To change the background colour, we inject a `style` attribute that overrides the default.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

After running the script, the `div` in `sample.html` will look like this when you open it in a browser:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

That’s the **change background colour html** technique you can reuse for any element—just swap the colour code.

## Step 7: Manipulate HTML with Python – Putting It All Together

Below is the full, runnable script that combines every step. Save it as `modify_html.py` and execute it from the same directory as your `YOUR_DIRECTORY` folder.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### What the script does, line by line

1. **Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.  
2. **Loads** `sample.html` and aborts with a clear error if the file is missing.  
3. **Retrieves** the element using **get element by id**.  
4. **Prints** the element’s text—showing **how to read HTML text**.  
5. **Adds** a custom attribute, illustrating **how to set HTML attribute**.  
6. **Changes** the background colour, fulfilling the **change background colour html** requirement.  
7. **Writes** the updated markup to `sample_modified.html`, so you can open it in a browser and see the changes.

Running the script yields console output similar to:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Open `sample_modified.html` and you’ll notice the gray background behind the text—proof that **manipulate HTML with python** really works.

## Common Pitfalls & How to Avoid Them

- **Missing ID** – If the target element doesn’t exist, `get_element_by_id` returns `None`. Always check for `None` before accessing properties; otherwise you’ll hit an `AttributeError`.  
- **Encoding issues** – When reading non‑ASCII pages, pass `encoding='utf-8'` to `html.parse` or ensure your file is saved in UTF‑8.  
- **Overwriting existing styles** – Setting the `style` attribute replaces any previous inline styles. If you need to preserve existing rules, read the current `style` value first, append your new rule, then write it back.  
- **File permissions** – Writing back to the same folder may fail on read‑only systems. Choose a writable output path, as we did with `sample_modified.html`.

## Extending the Example

Now that you’ve mastered the basics, consider these next steps:

- **Loop over multiple IDs** – Use a list of IDs and iterate with a `for` loop to batch‑process sections of a page.  
- **Replace text content** – Call `elem.text = "New text"` to alter the visible string.  
- **Add child elements** – Use `


## What Should You Learn Next?

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}