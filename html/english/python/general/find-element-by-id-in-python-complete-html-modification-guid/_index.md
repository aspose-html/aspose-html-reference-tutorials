---
category: general
date: 2026-06-16
description: find element by id using Python to change html title, modify html element,
  and write html file python quickly. Learn step‑by‑step.
draft: false
keywords:
- find element by id
- change html title
- write html file python
- modify html element
- change inner html
language: en
og_description: find element by id with Python, change html title, modify html element,
  and write html file python in a single, runnable guide.
og_title: find element by id in Python – Full HTML Editing Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: find element by id using Python to change html title, modify html element,
    and write html file python quickly. Learn step‑by‑step.
  headline: find element by id in Python – Complete HTML Modification Guide
  type: TechArticle
- description: find element by id using Python to change html title, modify html element,
    and write html file python quickly. Learn step‑by‑step.
  name: find element by id in Python – Complete HTML Modification Guide
  steps:
  - name: Expected Output
    text: 'Running the script produces a console message like:'
  - name: What if the HTML file contains multiple elements with the same ID?
    text: HTML standards dictate IDs must be unique, but real‑world pages sometimes
      violate that rule. `soup.find(id="title")` returns the **first** match. If you
      need to modify **all** matching elements, use `soup.find_all(id="title")` and
      loop over the result.
  - name: How do I preserve the original file’s line endings?
    text: "`BeautifulSoup.prettify()` normalizes line endings to `\n`. If you must
      keep Windows‑style `\r\n`, replace them after rendering:"
  - name: Can I use this approach for other attributes (e.g., `class`)?
    text: 'Absolutely. Replace `id` with any attribute:'
  type: HowTo
tags:
- python
- html-manipulation
- web-scraping
title: find element by id in Python – Complete HTML Modification Guide
url: /python/general/find-element-by-id-in-python-complete-html-modification-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# find element by id in Python – Complete HTML Modification Guide

Ever needed to **find element by id** in an HTML file and instantly update the page title? You’re not the only one. Whether you’re automating a static site migration or tweaking a template before deployment, being able to **change html title** programmatically saves hours of manual copy‑pasting.

In this tutorial we’ll walk through a real‑world example that shows exactly how to **find element by id**, **modify html element**, **change inner html**, and finally **write html file python**‑style. No external services, just pure Python and a couple of popular libraries. By the end you’ll have a ready‑to‑run script that you can drop into any project.

## What You’ll Learn

- How to load an HTML document safely.
- The exact call you need to **find element by id**.
- Why updating the `inner_html` property is the cleanest way to **change html title**.
- Steps to **write html file python** without losing formatting.
- Common pitfalls (encoding issues, missing IDs) and how to avoid them.

> **Prerequisite:** Python 3.8+ installed and a basic understanding of HTML structure. No prior experience with BeautifulSoup or lxml is required.

---

## Step 1: Set Up the Environment  

Before we dive into the code, let’s make sure the right packages are available. We’ll use **BeautifulSoup** for parsing and **lxml** as the parser backend—both are battle‑tested and lightweight.

```bash
pip install beautifulsoup4 lxml
```

> *Pro tip:* If you’re working inside a virtual environment, activate it first. This keeps your dependencies tidy and guarantees the script runs the same on every machine.

---

## Step 2: Load the HTML Document  

Now we’ll **find element by id**. The first thing to do is read the source file into memory. Using `Path` from `pathlib` ensures cross‑platform path handling.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
INPUT_PATH = Path("YOUR_DIRECTORY/input.html")

# Read the file with UTF‑8 encoding (the most common for web pages)
html_content = INPUT_PATH.read_text(encoding="utf-8")
```

> **Why this matters:** Directly opening the file with `open(..., 'r', encoding='utf-8')` works, but `Path.read_text` is a one‑liner that also raises a clear exception if the file isn’t found—making debugging easier.

---

## Step 3: Locate the Element by Its ID  

Here’s the core of our tutorial: **find element by id**. With BeautifulSoup you can call `find(id="title")` which returns the first tag whose `id` attribute matches.

```python
# Parse the HTML using the lxml parser for speed and accuracy
soup = BeautifulSoup(html_content, "lxml")

# Locate the element with id="title"
header = soup.find(id="title")

if header is None:
    raise ValueError("No element with id='title' found in the document.")
```

> **Explanation:**  
> - `soup.find(id="title")` is equivalent to the CSS selector `#title`.  
> - The guard clause (`if header is None`) prevents a *NoneType* error later, which is a frequent bug when the ID is misspelled or missing.

---

## Step 4: Change the Inner HTML (or Text)  

Now that we’ve **find element by id**, we can **change inner html**. If you only need plain text, `header.string = "New title"` works. For richer markup, assign to `header.string` or `header.clear()` followed by `header.append(...)`.

```python
# Update the element's inner HTML – this changes the page title
header.string = "New title"

# If you need to insert HTML tags inside the header, use:
# header.clear()
# header.append(BeautifulSoup("<strong>New title</strong>", "lxml"))
```

> **Why use `.string`?** It automatically escapes special characters, keeping the final HTML well‑formed. Directly setting `header.contents` can lead to malformed markup if you’re not careful.

---

## Step 5: Save the Modified Document – Write HTML File Python  

Finally, we’ll **write html file python**‑style. BeautifulSoup’s `prettify()` gives nicely indented output, but you can also use `str(soup)` to preserve the original formatting.

```python
# Path to the output HTML file
OUTPUT_PATH = Path("YOUR_DIRECTORY/output.html")

# Choose between prettified (human‑readable) or raw output
# raw_html = str(soup)          # Keeps original whitespace
pretty_html = soup.prettify()   # Adds indentation

# Write the modified HTML back to disk
OUTPUT_PATH.write_text(pretty_html, encoding="utf-8")
print(f"Modified file saved to {OUTPUT_PATH}")
```

> **Edge case:** If the original file used a different encoding (e.g., ISO‑8859‑1), you’ll need to detect it first. The `chardet` library can help, but for most modern sites UTF‑8 is the safe default.

---

## Full Working Example  

Putting it all together, here’s a single script you can copy‑paste and run. It demonstrates the entire flow from loading to saving.

```python
# modify_html_title.py
from pathlib import Path
from bs4 import BeautifulSoup

# ----------------------------------------------------------------------
# Configuration – adjust these paths to match your project layout
# ----------------------------------------------------------------------
INPUT_PATH = Path("YOUR_DIRECTORY/input.html")
OUTPUT_PATH = Path("YOUR_DIRECTORY/output.html")
TARGET_ID = "title"
NEW_TITLE = "New title"

# ----------------------------------------------------------------------
# Step 1: Load the HTML document
# ----------------------------------------------------------------------
html_content = INPUT_PATH.read_text(encoding="utf-8")
soup = BeautifulSoup(html_content, "lxml")

# ----------------------------------------------------------------------
# Step 2: Find element by ID
# ----------------------------------------------------------------------
header = soup.find(id=TARGET_ID)
if header is None:
    raise ValueError(f"No element with id='{TARGET_ID}' found.")

# ----------------------------------------------------------------------
# Step 3: Change inner HTML (the page title)
# ----------------------------------------------------------------------
header.string = NEW_TITLE

# ----------------------------------------------------------------------
# Step 4: Write the modified document back to disk
# ----------------------------------------------------------------------
OUTPUT_PATH.write_text(soup.prettify(), encoding="utf-8")
print(f"✅ Successfully updated '{TARGET_ID}' and saved to {OUTPUT_PATH}")
```

### Expected Output

Running the script produces a console message like:

```
✅ Successfully updated 'title' and saved to YOUR_DIRECTORY/output.html
```

If you open `output.html`, the element that originally looked like:

```html
<h1 id="title">Old title</h1>
```

will now read:

```html
<h1 id="title">New title</h1>
```

---

## Common Questions & Gotchas  

### What if the HTML file contains multiple elements with the same ID?  
HTML standards dictate IDs must be unique, but real‑world pages sometimes violate that rule. `soup.find(id="title")` returns the **first** match. If you need to modify **all** matching elements, use `soup.find_all(id="title")` and loop over the result.

```python
for header in soup.find_all(id="title"):
    header.string = NEW_TITLE
```

### How do I preserve the original file’s line endings?  
`BeautifulSoup.prettify()` normalizes line endings to `\n`. If you must keep Windows‑style `\r\n`, replace them after rendering:

```python
pretty_html = soup.prettify().replace("\n", "\r\n")
OUTPUT_PATH.write_text(pretty_html, encoding="utf-8")
```

### Can I use this approach for other attributes (e.g., `class`)?  
Absolutely. Replace `id` with any attribute:

```python
element = soup.find(class_="my-class")   # note the trailing underscore
```

---

## Pro Tips for Robust HTML Automation  

- **Validate before you write:** Use `html5lib` to parse the result and ensure no broken tags.
- **Backup original files:** Automate a copy step (`shutil.copy`) before overwriting.
- **Log changes:** A tiny CSV log (`csv.writer`) can help you track which files were updated during batch runs.
- **Batch processing:** Wrap the script in a `for file in Path('folder').glob('*.html'):` loop to **modify html element** across dozens of pages.

---

## Conclusion  

You now have a solid, production‑ready recipe to **find element by id**, **change html title**, **modify html element**, **change inner html**, and finally **write html file python**-style. The script is concise, easy to read, and covers the typical edge cases you’ll encounter when automating HTML updates.

Next steps? Try swapping the `title` element for a `<meta>` tag, or expand the script to replace placeholders throughout a whole site. You might also explore **lxml.etree** for ultra‑fast bulk transformations if performance becomes a concern.

Got a twist you’d like to share? Drop a comment below, and happy coding!  

![Python script that finds an element by id and changes the HTML title](https://example.com/images/find-element-by-id.png "Python script finding element by id and changing HTML title")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)
- [Advanced File Loading for HTML Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/advanced-file-loading-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}