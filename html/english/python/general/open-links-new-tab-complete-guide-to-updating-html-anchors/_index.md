---
category: general
date: 2026-07-05
description: Open links new tab using Python – learn how to add target blank, change
  link target, use attribute contains selector, and save modified html effortlessly.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: en
og_description: Open links new tab quickly. This tutorial shows how to add target
  blank, change link target, and save modified html with Python.
og_title: Open Links New Tab – Step‑by‑Step HTML Update Guide
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Open Links New Tab – Complete Guide to Updating HTML Anchors
url: /python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Open Links New Tab – Complete Guide to Updating HTML Anchors

Ever needed to **open links new tab** on a static HTML page but weren’t sure where to start? You’re not alone. Many developers hit this snag when cleaning up legacy sites or adding accessibility tweaks. In this tutorial we’ll walk through a practical solution that **adds target blank**, **changes link target**, and safely **saves modified html**—all with a few lines of Python.

We’ll also cover how to use an **attribute contains selector** so you only touch the anchors you really care about (for example, every link pointing to *example.com*). By the end, you’ll have a reusable script that you can drop into any project, no matter how big or small.

## What You’ll Learn

- Load an HTML file into a manipulable document object.  
- Select `<a>` elements whose `href` attribute contains a specific substring.  
- **Add target blank** and set the `rel="noopener"` attribute to improve security.  
- **Save modified html** back to disk without losing formatting.  

No external dependencies beyond the standard library and **beautifulsoup4** (a tiny install). If you’re already using a different parser, the concepts translate directly.

---

## Prerequisites

- Python 3.8+ installed on your machine.  
- Basic familiarity with HTML and Python.  
- `beautifulsoup4` package (`pip install beautifulsoup4`).  

That’s it—no heavyweight frameworks required.

---

## Step 1: Load the HTML Document

First things first: we need to read the source file and hand it to BeautifulSoup. Think of this as opening a blank canvas where you can draw new attributes.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Why this matters:** Using `Path` keeps the code OS‑agnostic, and `html.parser` is built‑in, so you don’t need extra parsers for simple tasks.

---

## Step 2: Use an Attribute Contains Selector to Find the Right Links

We only want to touch anchors that point to *example.com*. The CSS selector `a[href*='example.com']` does exactly that—`*=` means “contains”. BeautifulSoup’s `select` method understands this syntax.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro tip:** If you need a case‑insensitive match, switch to a small loop that checks `if 'example.com' in a.get('href', '').lower()`.

Now `anchor_elements` holds every link we care about, ready for the next transformation.

---

## Step 3: Change Link Target – Add Target Blank and Secure the Link

Opening a link in a new tab is as simple as setting `target="_blank"`. However, modern browsers recommend also adding `rel="noopener"` (or `noreferrer`) to prevent the newly opened page from accessing the original window via `window.opener`. This tiny security tweak can stop phishing attacks.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Why we use direct dictionary assignment:** It automatically creates the attribute if it’s missing, and overwrites it if it already exists—perfect for a **change link target** operation.

---

## Step 4: Save Modified HTML Back to Disk

The final step is to write the updated markup to a new file. Keeping the original untouched lets you revert if something goes wrong.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **What `prettify()` does:** It formats the HTML with nice indentation, making the saved file easier to read and diff later. If you prefer the original whitespace, replace `prettify()` with `str(soup)`.

---

## Full Script – One‑Click Solution

Below is the complete, ready‑to‑run script. Save it as `update_links.py` and execute `python update_links.py` from your terminal.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Expected Result

Suppose `links.html` originally contained:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

After running the script, `links-updated.html` will look like:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Only the link to *example.com* received the **add target blank** attributes, demonstrating that our **attribute contains selector** worked exactly as intended.

---

## Common Questions & Edge Cases

### What if a link already has a `rel` attribute?

Our loop overwrites it with `"noopener"`. If you need to preserve existing values (e.g., `"nofollow"`), concatenate instead:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### How to handle multiple domains?

Just expand the selector list:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### Does `prettify()` change the original HTML structure?

It re‑indents but doesn’t alter tag order or attribute values. If you must keep the exact original whitespace, replace `prettify()` with `str(soup)` as mentioned earlier.

---

## Pro Tips for Production‑Ready Scripts

- **Backup before overwriting:** Add a copy step (`shutil.copy`) to keep the original file safe.  
- **Logging instead of print:** Use the `logging` module for scalable projects.  
- **Batch processing:** Loop over a directory with `Path.rglob("*.html")` to update many files in one run.  

These tweaks turn a simple **open links new tab** script into a robust utility for any web‑maintenance workflow.

---

## Conclusion

You now have a solid, reusable method to **open links new tab** across any static HTML collection. By leveraging an **attribute contains selector**, you can **change link target** precisely where you need it, **add target blank**, and **save modified html** without losing formatting. 

Give it a spin on a test page, then scale up to your whole site. Need to tweak the selector for PDFs, PDFs, or other domains? Just adjust the CSS string—everything else stays the same.

Feel free to drop a comment if you run into quirks, or share how you extended the script for your own projects. Happy coding, and may all your anchors open exactly where you want them!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}