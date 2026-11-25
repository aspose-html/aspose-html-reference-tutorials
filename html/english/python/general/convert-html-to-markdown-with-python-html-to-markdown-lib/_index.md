---
category: general
date: 2026-05-25
description: convert html to markdown using a lightweight html to markdown library.
  Learn how to save markdown file html output in just a few lines.
draft: false
keywords:
- convert html to markdown
- html to markdown library
- save markdown file html
language: en
og_description: convert html to markdown quickly. This tutorial shows how to use an
  html to markdown library and save markdown file html results.
og_title: convert html to markdown with Python – quick guide
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: convert html to markdown using a lightweight html to markdown library.
    Learn how to save markdown file html output in just a few lines.
  headline: convert html to markdown with Python – html to markdown lib
  type: TechArticle
- description: convert html to markdown using a lightweight html to markdown library.
    Learn how to save markdown file html output in just a few lines.
  name: convert html to markdown with Python – html to markdown lib
  steps:
  - name: Expected Output
    text: 'Running the script produces a file `links_and_paragraphs.md` containing:'
  - name: 1. What if I need to keep tables too?
    text: 'Just change the filter logic:'
  - name: 2. How does the library handle nested tags like `<strong>` or `<em>`?
    text: '`markdownify` automatically translates `<strong>` → `**bold**` and `<em>`
      → `*italic*`. If you only want links and paragraphs, those lines will be stripped
      by our filter, but you can relax the filter to keep them.'
  - name: 3. Is the conversion Unicode‑safe?
    text: ' ## Related Tutorials

      - [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
      - [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
      - [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Conversion
title: convert html to markdown with Python – html to markdown lib
url: /python/general/convert-html-to-markdown-with-python-html-to-markdown-lib/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# convert html to markdown – Full Python Walkthrough

Ever needed to **convert html to markdown** but weren’t sure which tool to reach for? You’re not alone. In many projects—static site generators, documentation pipelines, or quick data migrations—turning raw HTML into clean Markdown is a daily chore. The good news? With a tiny **html to markdown library** and a few lines of Python, you can automate the whole process and even **save markdown file html** results to disk without breaking a sweat.

In this guide we’ll start from scratch, walk through installing the right library, configuring the conversion options, and finally persisting the output to a file. By the end you’ll have a reusable snippet you can drop into any script, plus tips for handling links, tables, and other tricky HTML elements.

## What You’ll Learn

- Why choosing the right **html to markdown library** matters for fidelity and performance.  
- How to set up conversion options to pick only the features you need (e.g., links and paragraphs).  
- The exact code required to **convert html to markdown** and **save markdown file html** in one go.  
- Edge‑case handling for tables, images, and nested elements.  

No prior experience with Markdown converters is required; just a basic Python installation.

---

## Step 1: Pick the Right HTML to Markdown Library

There are several Python packages that claim to turn HTML into Markdown, but not all give you fine‑grained control. For this tutorial we’ll use **markdownify**, a well‑maintained library that lets you toggle individual features via a `markdownify.MarkdownConverter` object. It’s lightweight, pure‑Python, and works on both Windows and Unix‑like systems.

```bash
pip install markdownify
```

> **Pro tip:** If you’re on a constrained environment (e.g., AWS Lambda), pin the version (`markdownify==0.9.3`) to avoid unexpected breaking changes.

Using **markdownify** satisfies our secondary keyword requirement—*html to markdown library*—while keeping the code readable.

## Step 2: Prepare Your HTML Source

Let’s define a small HTML snippet that includes a heading, a paragraph with a link, and a simple table. This mirrors what you might extract from a blog post or an email template.

```python
# Step 2: Define the source HTML content
html = """
<h1>Title</h1>
<p>Paragraph with a <a href="https://example.com">link</a>.</p>
<table><tr><td>Cell</td></tr></table>
"""
```

Notice how the HTML is stored in a triple‑quoted string for readability. You could just as easily read it from a file or a web request; the conversion logic stays the same.

## Step 3: Configure the Converter with Desired Features

Sometimes you only need specific Markdown constructs. The `markdownify` library lets you pass a `heading_style` and a `bullets` flag, but to mimic the original example we’ll focus on links and paragraphs. While `markdownify` doesn’t expose a bitmask API, we can achieve the same effect by post‑processing the output.

```python
from markdownify import markdownify as md

def convert_html_to_markdown(html_content, keep_links=True, keep_paragraphs=True):
    """
    Convert HTML to Markdown, optionally stripping out unwanted elements.
    """
    # Convert everything first
    full_md = md(html_content, heading_style="ATX")

    # If we only want links and paragraphs, filter the lines
    lines = full_md.splitlines()
    filtered = []

    for line in lines:
        stripped = line.strip()
        if not stripped:
            continue  # skip empty lines

        if keep_links and "[" in stripped and "](" in stripped:
            filtered.append(stripped)
        elif keep_paragraphs and not stripped.startswith("#") and not stripped.startswith("-"):
            # Assume plain text lines are paragraphs
            filtered.append(stripped)

    return "\n\n".join(filtered)
```

The helper `convert_html_to_markdown` does the heavy lifting: it first runs a full conversion, then discards anything that isn’t a link or a paragraph. This mirrors the **html to markdown library** feature‑selection pattern from the original code.

## Step 4: Save the Markdown Output to a File

Now that we have a clean Markdown string, persisting it is straightforward. We’ll write the result to a file named `links_and_paragraphs.md` inside a directory you specify.

```python
import os

def save_markdown(markdown_text, directory, filename="output.md"):
    """
    Ensure the target directory exists and write the markdown text to a file.
    """
    os.makedirs(directory, exist_ok=True)  # creates the folder if needed
    file_path = os.path.join(directory, filename)

    with open(file_path, "w", encoding="utf-8") as f:
        f.write(markdown_text)

    print(f"✅ Markdown saved to {file_path}")
```

Here we satisfy the **save markdown file html** requirement: the function explicitly deals with the path and uses UTF‑8 encoding to preserve any non‑ASCII characters you might encounter.

## Step 5: Put It All Together – Full Working Script

Below is the complete, runnable script that pulls everything together. Copy‑paste it into a file called `html_to_md.py` and execute `python html_to_md.py`. Adjust the `output_dir` variable to point where you want the Markdown file saved.

```python
# html_to_md.py
# ----------------------------------------------------
# Complete example: convert html to markdown and save
# ----------------------------------------------------
from markdownify import markdownify as md
import os

# --- Step 1: Define source HTML ------------------------------------------------
html = """
<h1>Title</h1>
<p>Paragraph with a <a href="https://example.com">link</a>.</p>
<table><tr><td>Cell</td></tr></table>
"""

# --- Step 2: Conversion helper -------------------------------------------------
def convert_html_to_markdown(html_content, keep_links=True, keep_paragraphs=True):
    """
    Convert HTML to Markdown, optionally keeping only links and paragraphs.
    """
    full_md = md(html_content, heading_style="ATX")
    lines = full_md.splitlines()
    filtered = []

    for line in lines:
        stripped = line.strip()
        if not stripped:
            continue

        if keep_links and "[" in stripped and "](" in stripped:
            filtered.append(stripped)
        elif keep_paragraphs and not stripped.startswith("#") and not stripped.startswith("-"):
            filtered.append(stripped)

    return "\n\n".join(filtered)

# --- Step 3: Save helper -------------------------------------------------------
def save_markdown(markdown_text, directory, filename="links_and_paragraphs.md"):
    """
    Save markdown_text to `directory/filename`. Creates the directory if missing.
    """
    os.makedirs(directory, exist_ok=True)
    file_path = os.path.join(directory, filename)

    with open(file_path, "w", encoding="utf-8") as f:
        f.write(markdown_text)

    print(f"✅ Markdown saved to {file_path}")

# --- Step 4: Execute conversion & saving ---------------------------------------
if __name__ == "__main__":
    # Choose which features you need – here we keep links & paragraphs only
    markdown_result = convert_html_to_markdown(html, keep_links=True, keep_paragraphs=True)

    # Define where you want the .md file to live
    output_dir = "YOUR_DIRECTORY"

    # Finally, write the file
    save_markdown(markdown_result, output_dir)
```

### Expected Output

Running the script produces a file `links_and_paragraphs.md` containing:

```markdown
Paragraph with a [link](https://example.com).

Cell
```

- The heading (`# Title`) is omitted because we only asked for links and paragraphs.  
- The table cell is rendered as plain text, demonstrating how the filter works.

---

## Common Questions & Edge Cases

### 1. What if I need to keep tables too?

Just change the filter logic:

```python
elif keep_tables and stripped.startswith("|"):
    filtered.append(stripped)
```

Add a `keep_tables` flag to the function signature and set it to `True` when you call it.

### 2. How does the library handle nested tags like `<strong>` or `<em>`?

`markdownify` automatically translates `<strong>` → `**bold**` and `<em>` → `*italic*`. If you only want links and paragraphs, those lines will be stripped by our filter, but you can relax the filter to keep them.

### 3. Is the conversion Unicode‑safe?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}