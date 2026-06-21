---
category: general
date: 2026-06-07
description: How to add prefix to HTML headings using Python. Learn to select multiple
  headings, change HTML titles, and save modified HTML efficiently.
draft: false
keywords:
- how to add prefix
- select multiple headings
- save modified html
- change html titles
- modify html with python
language: en
og_description: How to add prefix to HTML headings using Python. This tutorial shows
  how to select multiple headings, change HTML titles, and save modified HTML in just
  a few lines.
og_title: How to Add Prefix to HTML Headings with Python – Quick Guide
schemas:
- author: Aspose
  dateModified: '2026-06-07'
  description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  headline: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to add prefix to HTML headings using Python. Learn to select multiple
    headings, change HTML titles, and save modified HTML efficiently.
  name: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
  steps:
  - name: Verify the changes in a diff tool.
    text: Verify the changes in a diff tool.
  - name: Roll back instantly if something looks off.
    text: Roll back instantly if something looks off.
  - name: Keep the original untouched for audit purposes.
    text: Keep the original untouched for audit purposes.
  type: HowTo
tags:
- Python
- HTML
- Automation
- Web Scraping
title: How to Add Prefix to HTML Headings with Python – Step‑by‑Step Guide
url: /python/general/how-to-add-prefix-to-html-headings-with-python-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Add Prefix to HTML Headings with Python – Complete Tutorial

How to add prefix to HTML headings using Python is a common need when you maintain a site that gets frequent updates. In this guide we’ll walk through selecting multiple headings, changing HTML titles, and saving the modified HTML—all without leaving your editor.  

If you’ve ever wondered whether you can automate the “mark as updated” badge across dozens of pages, you’re in the right place. We’ll also touch on how to **modify html with python** in a way that scales, so you won’t have to open each file manually.

## What You’ll Achieve

By the end of this tutorial you’ll be able to:

* **Select multiple headings** (`h1`, `h2`, `h3`) in a single pass.  
* **Add a custom prefix** (e.g., `[Updated]`) to every heading’s text.  
* **Save modified html** back to disk, preserving the original file structure.  
* Understand the trade‑offs between different Python HTML parsers, and pick the one that fits your project.

No external services, no heavy frameworks—just pure Python and a couple of well‑maintained libraries.

---

## How to Add Prefix to Heading Text in Python

Below is a minimal, runnable example that demonstrates the core idea. It uses the **`lxml`** library together with **`cssselect`** for selector support, which mirrors the `query_selector_all` method you saw in the original snippet.

```python
# -------------------------------------------------
# Step 0: Install dependencies (run once)
# -------------------------------------------------
# pip install lxml cssselect

# -------------------------------------------------
# Step 1: Load the HTML document
# -------------------------------------------------
from lxml import html

# Replace with your actual file path
input_path = "YOUR_DIRECTORY/article.html"
with open(input_path, "r", encoding="utf-8") as f:
    doc = html.fromstring(f.read())

# -------------------------------------------------
# Step 2: Select multiple headings (h1, h2, h3)
# -------------------------------------------------
# The CSS selector "h1, h2, h3" grabs all three levels.
headings = doc.cssselect("h1, h2, h3")

# -------------------------------------------------
# Step 3: Add the prefix "[Updated] " to each heading
# -------------------------------------------------
prefix = "[Updated] "
for heading in headings:
    # Preserve existing whitespace but prepend our tag
    heading.text = f"{prefix}{heading.text_content().strip()}"

# -------------------------------------------------
# Step 4: Save the modified HTML
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/article_updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

print(f"✅ Finished! Modified file saved to {output_path}")
```

**Expected output** (excerpt from `article_updated.html`):

```html
<h1>[Updated] Introduction to Machine Learning</h1>
<h2>[Updated] Data Pre‑processing Steps</h2>
<h3>[Updated] Feature Engineering Techniques</h3>
```

Notice how each heading now starts with the `[Updated]` tag—exactly what we wanted when we asked **how to add prefix** to our titles.

### Why This Approach Works

* **`lxml` + `cssselect`** gives you full CSS‑selector power, making the “select multiple headings” step a one‑liner.  
* The `text_content()` method safely extracts the inner text, avoiding HTML entities or child tags.  
* Writing back with `pretty_print=True` keeps the file human‑readable, which is handy for version control diffs.

---

## Selecting Multiple Headings with CSS Selectors

If you’re coming from a JavaScript background, the `cssselect` syntax will feel right at home. The selector `"h1, h2, h3"` is a **comma‑separated list**, meaning “grab any element that matches *any* of these three”.  

You could also broaden the scope:

```python
# Grab every heading from h1 through h6
all_headings = doc.cssselect("h1, h2, h3, h4, h5, h6")
```

Or narrow it down to a specific section:

```python
# Only headings inside the <article> tag
article_headings = doc.cssselect("article h1, article h2, article h3")
```

These tiny tweaks let you **select multiple headings** with laser precision, which is especially useful when you have a massive documentation site and only want to update a subsection.

---

## Saving Modified HTML Files Safely

When you **save modified html**, you want to avoid corrupting the original file. The pattern shown above writes to a new file (`article_updated.html`). That way you can:

1. Verify the changes in a diff tool.  
2. Roll back instantly if something looks off.  
3. Keep the original untouched for audit purposes.

If you prefer an in‑place edit, just swap the paths:

```python
import shutil
shutil.move(output_path, input_path)  # Overwrites the original
```

But remember: **always back up** before overwriting, especially on production servers.

---

## Changing HTML Titles vs. Headings

You might wonder whether “changing HTML titles” is the same as prefixing headings. In HTML terminology, the `<title>` tag lives inside `<head>` and controls the browser tab title, whereas headings (`<h1>…<h3>`) appear in the page body.

If you need to **change html titles** as well, the same `lxml` workflow applies:

```python
# Change the <title> tag
title_elem = doc.find(".//title")
if title_elem is not None:
    title_elem.text = f"{prefix}{title_elem.text}"
```

Now both the page title and the visible headings carry the same `[Updated]` flag—perfect for SEO audits where you want consistency across meta‑data and on‑page content.

---

## Alternative Libraries for modify html with python

While `lxml` is fast and feature‑rich, you might already be using **BeautifulSoup** (bs4) in your project. Here’s the same logic in a more “pythonic” style:

```python
from bs4 import BeautifulSoup

with open(input_path, "r", encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")

for tag in soup.select("h1, h2, h3"):
    tag.string = f"{prefix}{tag.get_text(strip=True)}"

with open(output_path, "w", encoding="utf-8") as f:
    f.write(str(soup.prettify()))
```

Both libraries let you **modify html with python**, so pick the one that matches your existing stack. `BeautifulSoup` shines when you need forgiving parsing of malformed markup, while `lxml` offers superior speed for large batches.

---

## Pro Tips & Common Pitfalls

* **Encoding matters** – always open files with `encoding="utf-8"` to avoid Unicode errors on non‑ASCII characters.  
* **Avoid double‑prefixing** – if you run the script twice, you’ll get `[Updated] [Updated] …`. Guard against this by checking `heading.text.startswith(prefix)`.  
* **Preserve whitespace** – the `strip()` call removes stray spaces, keeping the output tidy.  
* **Batch processing** – wrap the whole flow in a `for file in pathlib.Path("YOUR_DIRECTORY").glob("*.html"):` loop to update an entire folder with a single command.  

---

## Full Working Example: Batch Update a Directory

Below is a compact script that iterates over every `.html` file in a directory, prefixes headings, updates the `<title>`, and writes a new file with `_updated` appended.

```python
import pathlib
from lxml import html

prefix = "[Updated] "
source_dir = pathlib.Path("YOUR_DIRECTORY")
output_dir = source_dir / "updated"
output_dir.mkdir(exist_ok=True)

for html_path in source_dir.glob("*.html"):
    # Load
    with open(html_path, "r", encoding="utf-8") as f:
        doc = html.fromstring(f.read())

    # Headings
    for h in doc.cssselect("h1, h2, h3"):
        if not h.text_content().startswith(prefix):
            h.text = f"{prefix}{h.text_content().strip()}"

    # Title
    title_elem = doc.find(".//title")
    if title_elem is not None and not title_elem.text.startswith(prefix):
        title_elem.text = f"{prefix}{title_elem.text}"

    # Save
    out_path = output_dir / f"{html_path.stem}_updated.html"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write(html.tostring(doc, pretty_print=True, encoding="unicode"))

    print(f"✅ Processed {html_path.name} → {out_path.name}")
```

Run it once, and every HTML file in `YOUR_DIRECTORY` gets a fresh `[Updated]` badge—no manual editing required.

---

## Conclusion

We’ve covered **how to add prefix** to HTML headings using Python, demonstrated how to **select multiple headings**, shown you how to **save modified html** safely, and even touched on **change html titles** for a complete overhaul. By leveraging either `lxml` or `BeautifulSoup`, you now have a solid toolbox for **modify html with python** in real‑world projects.

Next steps? Try adding timestamps instead of a static tag, or generate a changelog file that lists every file you touched. You could also hook this script into a CI pipeline so every deployment automatically


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}