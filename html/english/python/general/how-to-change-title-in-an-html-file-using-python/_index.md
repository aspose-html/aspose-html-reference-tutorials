---
category: general
date: 2026-09-19
description: Learn how to change title in an HTML file with Python. This guide covers
  reading HTML, updating the title tag, and saving the modified HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change title
- update html title
- read html with python
- load html file python
- save modified html
language: en
lastmod: 2026-09-19
og_description: How to change title in an HTML file with Python. Follow this complete
  example to read HTML, update the title tag, and save the modified document.
og_image_alt: Diagram showing how to change title in an HTML file using Python
og_title: How to change title in an HTML file using Python – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Learn how to change title in an HTML file with Python. This guide covers
    reading HTML, updating the title tag, and saving the modified HTML.
  headline: How to change title in an HTML file using Python
  type: TechArticle
tags:
- Python
- HTML
- Web scraping
title: How to change title in an HTML file using Python
url: /python/general/how-to-change-title-in-an-html-file-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to change title in an HTML file using Python

If you need to **how to change title** in an HTML document programmatically, Python makes the job straightforward. In this tutorial you’ll read an HTML file, update the `<title>` element, and save the modified HTML back to disk—all with clear, runnable code.

Changing the page title is a common step when you generate static sites, customize scraped pages, or automate SEO updates. By the end of this guide you’ll know how to **update html title**, how to **read html with python**, and how to **save modified html** safely.

## Prerequisites

Before you start, make sure you have:

- Python 3.8 or newer installed  
- The `beautifulsoup4` package (`pip install beautifulsoup4`)  
- An HTML file you want to edit (the example uses `index.html` in a folder you choose)  

No external services are required; everything runs locally.

## Step 1: Load the HTML file with Python  

The first task is to **load html file python**‑style. Using `BeautifulSoup` gives you a forgiving parser that works with imperfect markup.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Define the directory that holds the original HTML
html_dir = Path("YOUR_DIRECTORY")
original_path = html_dir / "index.html"

# Read the file contents (this is how you **read html with python**)
with original_path.open(encoding="utf-8") as f:
    html_content = f.read()

# Parse the document
soup = BeautifulSoup(html_content, "html.parser")
```

*Why this step matters:*  
`BeautifulSoup` builds a tree representation, letting you query and modify elements without manual string handling. The `html.parser` built‑in is fast and requires no extra binaries.

## Step 2: Locate the `<title>` element  

HTML documents usually contain a single `<title>` tag inside `<head>`. We retrieve the first occurrence, which satisfies the **update html title** requirement.

```python
# Find the first <title> element; BeautifulSoup returns None if missing
title_tag = soup.find("title")

if title_tag is None:
    # If the document lacks a <title>, create one inside <head>
    head_tag = soup.find("head")
    if head_tag is None:
        # As a safety net, add a <head> element at the top
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

# Show the current title (useful for debugging)
print("Current title:", title_tag.string)
```

*Why we check for `None`*:  
Some HTML fragments omit the title. Adding it automatically prevents later errors and keeps the script robust.

## Step 3: Change the title text  

Now we **update html title** by assigning new text to the tag’s string. This is the core of the **how to change title** operation.

```python
new_title = "New Title"

# Replace the existing title text
title_tag.string = new_title

print("Updated title:", title_tag.string)
```

The `string` attribute represents the text node inside `<title>`. Overwriting it updates the DOM in memory.

## Step 4: Save the modified HTML  

Finally, write the altered document to a new file. This fulfills the **save modified html** step and leaves the original untouched.

```python
# Define the output path
modified_path = html_dir / "index_modified.html"

# Write the prettified HTML back to disk
with modified_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_path}")
```

`prettify()` formats the output with indentation, making the file easy to read after the change.

### Expected output

Running the script on a sample `index.html` that originally contains:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Old Title</title>
</head>
<body>
    <h1>Welcome</h1>
</body>
</html>
```

produces console output similar to:

```
Current title: Old Title
Updated title: New Title
Modified HTML saved to YOUR_DIRECTORY/index_modified.html
```

The saved `index_modified.html` will now start with:

```html
<!DOCTYPE html>
<html>
 <head>
  <title>
   New Title
  </title>
 </head>
 <body>
  <h1>
   Welcome
  </h1>
 </body>
</html>
```

## Full script for quick copy‑paste

Below is the complete, ready‑to‑run program that combines all four steps. Save it as `change_title.py` and adjust `YOUR_DIRECTORY` as needed.

```python
# change_title.py
from pathlib import Path
from bs4 import BeautifulSoup

# ----------------------------------------------------------------------
# Configuration – change these values to match your environment
# ----------------------------------------------------------------------
html_dir = Path("YOUR_DIRECTORY")          # Folder containing index.html
original_file = html_dir / "index.html"
modified_file = html_dir / "index_modified.html"
new_title = "New Title"                    # Desired title text
# ----------------------------------------------------------------------

# 1️⃣ Load the HTML file (read html with python)
with original_file.open(encoding="utf-8") as f:
    html_content = f.read()

soup = BeautifulSoup(html_content, "html.parser")

# 2️⃣ Locate or create the <title> element
title_tag = soup.find("title")
if title_tag is None:
    head_tag = soup.find("head")
    if head_tag is None:
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

print("Current title:", title_tag.string)

# 3️⃣ Update the title (how to change title)
title_tag.string = new_title
print("Updated title:", title_tag.string)

# 4️⃣ Save the modified HTML (save modified html)
with modified_file.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_file}")
```

Run the script:

```bash
python change_title.py
```

You’ll see the console messages and a new `index_modified.html` file with the updated title.

## Additional tips and edge cases

| Situation | What to do |
|-----------|------------|
| **Multiple `<title>` tags** | `soup.find_all("title")` returns a list; update the first element or iterate if you need to change all. |
| **Encoding problems** | Open files with `encoding="utf-8-sig"` if a BOM is present, or detect encoding with `chardet`. |
| **Large HTML files** | Use `lxml` parser (`BeautifulSoup(html_content, "lxml")`) for better performance. |
| **Preserving original formatting** | If you must keep the exact whitespace, write `str(soup)` instead of `prettify()`. |
| **Automating across many files** | Wrap the logic in a function and loop over `Path.rglob("*.html")`. |

These variations keep the core **how to change title** logic intact while adapting to real‑world projects.

## Conclusion

You now know how to **how to change title** in any HTML document using Python. The tutorial covered reading HTML, locating the `<title>` tag, updating its text, and **saving modified html** safely. With the full script you can integrate this pattern into static‑site generators, SEO pipelines, or any automation that requires dynamic title changes.

Next, explore related topics such as **read html with python** for extracting meta tags, or **load html file python** techniques for handling malformed markup. Experiment with batch processing to update titles across an entire website—your new skill is the foundation for many web‑automation tasks. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Save HTML with Aspose.Html – Complete C# Guide](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Render HTML to PNG – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}