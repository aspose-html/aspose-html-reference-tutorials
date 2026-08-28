---
category: general
date: 2026-06-29
description: Convert HTML to Markdown quickly using Python. Learn resource handling
  options, keep images external, and generate clean .md files.
draft: false
keywords:
- convert html to markdown
- HTML to Markdown conversion
- resource handling options
- external image assets
- Python HTML conversion
language: en
og_description: Convert HTML to Markdown with Python in minutes. This guide covers
  resource handling, external assets, and full code examples.
og_title: Convert HTML to Markdown – Complete Python Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Convert HTML to Markdown quickly using Python. Learn resource handling
    options, keep images external, and generate clean .md files.
  headline: Convert HTML to Markdown – Step‑by‑Step Python Guide
  type: TechArticle
- description: Convert HTML to Markdown quickly using Python. Learn resource handling
    options, keep images external, and generate clean .md files.
  name: Convert HTML to Markdown – Step‑by‑Step Python Guide
  steps:
  - name: What the Settings Do
    text: '| Setting | Effect | |---------|--------| | `save_external_resources` |
      Saves each referenced image as a separate file instead of embedding it. | |
      `external_resources_folder` | Relative path (from the output markdown) where
      images will be written. |'
  - name: Expected Output
    text: '- `complex.md` – a markdown file containing clean headings, lists, and
      image references like `![Alt text](assets/image1.png)`. - `assets/` – a folder
      next to the markdown file containing every image that was referenced in the
      original HTML.'
  - name: 1️⃣ Images with Query Strings
    text: Some legacy sites append timestamps to image URLs (`pic.png?v=123`). Aspose
      strips the query part automatically, but if you notice missing images, double‑check
      the `external_resources_folder` permissions and ensure the source path is reachable.
  - name: 2️⃣ Inline Styles That Don't Translate
    text: 'Markdown doesn’t have a native concept for CSS. If your HTML relies heavily
      on `<style>` blocks, the converter will drop them. You can preserve critical
      styling by converting those sections to HTML blocks inside markdown:'
  - name: 3️⃣ Tables with Merged Cells
    text: Aspose does its best to flatten merged cells into markdown tables, but complex
      `rowspan`/`colspan` layouts may lose alignment. In those cases, consider exporting
      the table as an HTML snippet within the markdown, or manually edit the generated
      markdown.
  - name: 4️⃣ Large Documents and Memory Usage
    text: 'For massive HTML files (hundreds of megabytes), load the document in streaming
      mode:'
  type: HowTo
tags:
- Python
- HTML
- Markdown
- File conversion
title: Convert HTML to Markdown – Step‑by‑Step Python Guide
url: /python/general/convert-html-to-markdown-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to Markdown – Complete Python Tutorial

Ever needed to **convert HTML to Markdown** but kept running into broken image links or messy formatting? You're not alone. Many developers hit that wall when migrating legacy web content into clean, version‑controlled markdown repositories.  

In this tutorial we’ll walk through a **full, runnable example** that shows you exactly how to convert HTML to Markdown while preserving images as separate files. By the end you’ll have a reusable script, understand the *why* behind each setting, and know how to tweak the process for edge cases like inline CSS or embedded SVGs.

---

## What This Guide Covers

- Installing the right Python library (Aspose.HTML for Python)  
- Loading an HTML document from disk  
- Configuring **resource handling options** so images stay as external assets  
- Setting up **MarkdownSaveOptions** and linking the resource configuration  
- Running the conversion and verifying the output  

No prior experience with Aspose is required; just a basic Python setup and a folder of HTML files. Let’s get started.

---

## Prerequisites

Before diving into code, make sure you have:

1. **Python 3.9+** installed (the latest stable release is preferred).  
2. **pip** available to install packages.  
3. A copy of the **Aspose.HTML for Python via .NET** package (`aspose-html`) – it handles the heavy lifting of parsing HTML and emitting Markdown.  
4. An example HTML file (`complex.html`) that contains images, tables, and a few custom styles.  

If you’re missing any of these, run the following in your terminal:

```bash
python -m pip install aspose-html
```

> **Pro tip:** Use a virtual environment (`python -m venv venv`) to keep dependencies isolated.

---

## Step 1 – Load the Source HTML Document

The first thing we do is tell Aspose where our source file lives. The `HTMLDocument` class reads the file into a DOM‑like structure that the converter can work with.

```python
from aspose.html import HTMLDocument

# Replace the path with the location of your HTML file
html_path = "YOUR_DIRECTORY/complex.html"
html_doc = HTMLDocument(html_path)
print(f"Loaded document: {html_doc.url}")
```

> **Why this matters:** Loading the document upfront lets the library resolve relative links (like `<img src="images/pic.png">`) against the file’s location, which is essential when we later **convert HTML to markdown** and keep images external.

---

## Step 2 – Configure Resource Handling to Keep Images Separate

If you simply call the converter, Aspose will embed every image as a Base64 string inside the markdown. That’s rarely what you want for a clean repo. Instead, we enable **external image assets** and point the library to a folder where those images will be saved.

```python
from aspose.html import ResourceHandlingOptions

resource_options = ResourceHandlingOptions()
resource_options.save_external_resources = True          # Keep images external
resource_options.external_resources_folder = "assets"    # Sub‑folder for assets

print("Resource handling configured:")
print(f"  Save external: {resource_options.save_external_resources}")
print(f"  Assets folder: {resource_options.external_resources_folder}")
```

### What the Settings Do

| Setting | Effect |
|---------|--------|
| `save_external_resources` | Saves each referenced image as a separate file instead of embedding it. |
| `external_resources_folder` | Relative path (from the output markdown) where images will be written. |

> **Edge case:** If your HTML contains CSS `url()` references, those will also be treated as external resources. Make sure the `assets` folder is included in your version control if you plan to share the markdown.

---

## Step 3 – Attach the Resource Options to Markdown Save Settings

Now we create a `MarkdownSaveOptions` instance and plug the resource handling we just defined. This object tells the converter exactly how to serialize the document.

```python
from aspose.html import MarkdownSaveOptions

markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options

print("Markdown save options ready.")
```

> **Why we need this step:** Without attaching the `resource_handling_options`, the converter would ignore our external‑resource preferences and fall back to the default (inline Base64). This is the crucial link that makes our **HTML to Markdown conversion** tidy.

---

## Step 4 – Perform the Conversion

Finally, we invoke the static `Converter.convert_html` method, providing the source document, the markdown options, and the destination path.

```python
from aspose.html import Converter

output_md = "YOUR_DIRECTORY/complex.md"
Converter.convert_html(html_doc, markdown_options, output_md)

print(f"Conversion complete! Markdown saved to: {output_md}")
```

### Expected Output

- `complex.md` – a markdown file containing clean headings, lists, and image references like `![Alt text](assets/image1.png)`.  
- `assets/` – a folder next to the markdown file containing every image that was referenced in the original HTML.

Open `complex.md` in any markdown viewer (VS Code, Typora, GitHub) and you should see the same visual structure as the original HTML, but now in a lightweight text format.

---

## Handling Common Pitfalls

### 1️⃣ Images with Query Strings

Some legacy sites append timestamps to image URLs (`pic.png?v=123`). Aspose strips the query part automatically, but if you notice missing images, double‑check the `external_resources_folder` permissions and ensure the source path is reachable.

### 2️⃣ Inline Styles That Don't Translate

Markdown doesn’t have a native concept for CSS. If your HTML relies heavily on `<style>` blocks, the converter will drop them. You can preserve critical styling by converting those sections to HTML blocks inside markdown:

```markdown
<div>
  <style>
    .highlight { background:#ff0; }
  </style>
  <p class="highlight">Important text</p>
</div>
```

### 3️⃣ Tables with Merged Cells

Aspose does its best to flatten merged cells into markdown tables, but complex `rowspan`/`colspan` layouts may lose alignment. In those cases, consider exporting the table as an HTML snippet within the markdown, or manually edit the generated markdown.

### 4️⃣ Large Documents and Memory Usage

For massive HTML files (hundreds of megabytes), load the document in streaming mode:

```python
html_doc = HTMLDocument(html_path, load_options=LoadOptions(streaming=True))
```

This reduces RAM consumption at the cost of slightly slower processing.

---

## Full Script You Can Copy‑Paste

Below is the complete, ready‑to‑run script that incorporates all the steps and tips above. Save it as `convert_html_to_md.py` and adjust the paths accordingly.

```python
# convert_html_to_md.py
# -------------------------------------------------
# Python script to convert an HTML file to Markdown
# while keeping images as external assets.
# -------------------------------------------------

from aspose.html import (
    HTMLDocument,
    ResourceHandlingOptions,
    MarkdownSaveOptions,
    Converter,
)

def convert_html_to_markdown(
    html_path: str,
    markdown_path: str,
    assets_folder: str = "assets",
) -> None:
    """
    Convert HTML to Markdown with external image handling.

    Parameters
    ----------
    html_path : str
        Path to the source HTML file.
    markdown_path : str
        Destination path for the generated .md file.
    assets_folder : str, optional
        Sub‑folder (relative to markdown_path) where images will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(html_path)

    # Configure resource handling
    resource_opts = ResourceHandlingOptions()
    resource_opts.save_external_resources = True
    resource_opts.external_resources_folder = assets_folder

    # Set up markdown options and attach resource handling
    md_opts = MarkdownSaveOptions()
    md_opts.resource_handling_options = resource_opts

    # Perform the conversion
    Converter.convert_html(html_doc, md_opts, markdown_path)

    print(f"✅ Conversion finished! 🎉")
    print(f"   Markdown: {markdown_path}")
    print(f"   Images  : {assets_folder}/ (if any)")

if __name__ == "__main__":
    # -----------------------------------------------------------------
    # Update these paths before running the script
    # -----------------------------------------------------------------
    SOURCE_HTML = "YOUR_DIRECTORY/complex.html"
    DEST_MD    = "YOUR_DIRECTORY/complex.md"
    ASSETS_DIR = "assets"

    convert_html_to_markdown(SOURCE_HTML, DEST_MD, ASSETS_DIR)
```

Run it with:

```bash
python convert_html_to_md.py
```

You’ll see the same confirmation messages as in the step‑by‑step section, and the `assets` folder will appear next to `complex.md`.

---

## Bonus: Visual Overview

![convert html to markdown workflow diagram](/images/convert-html-to-markdown-diagram.png "Diagram showing the convert html to markdown process with resource handling")

*Alt text:* Diagram illustrating the flow from loading HTML, configuring resource handling, to saving Markdown with external assets.

*(If you don’t have the image, just imagine a simple flowchart – the alt text still satisfies SEO.)*

---

## Conclusion

You now have a **complete, production‑ready method to convert HTML to markdown** using Python. By explicitly configuring **resource handling options**, you keep images cleanly separated, which is ideal for version‑controlled documentation or static‑site generators.  

From here you might:

- Automate batch conversion for an entire folder of HTML files.  
- Extend the script to replace broken links with absolute URLs.  
- Integrate it into a CI pipeline that builds documentation on every commit.  

Feel free to experiment—swap `MarkdownSaveOptions` for `HtmlSaveOptions` if you ever need the reverse, or play with `LoadOptions` to fine‑tune parsing.  

Happy converting, and may your markdown stay tidy! 🚀


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}