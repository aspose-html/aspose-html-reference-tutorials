---
category: general
date: 2026-09-16
description: Learn to convert HTML to markdown quickly, export HTML as markdown and
  keep images intact with a simple Python script.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- export html as markdown
- save html page as markdown
- how to convert html to markdown
- markdown conversion with images
language: en
lastmod: 2026-09-16
og_description: Convert HTML to markdown and preserve images. This tutorial shows
  you how to export HTML as markdown using a concise Python script.
og_image_alt: convert html to markdown script output showing markdown file with images
og_title: Convert HTML to markdown with images – step‑by‑step Python guide
schemas:
- author: GroupDocs
  dateModified: '2026-09-16'
  description: Learn to convert HTML to markdown quickly, export HTML as markdown
    and keep images intact with a simple Python script.
  headline: How to convert HTML to markdown with images using Python
  type: TechArticle
- description: Learn to convert HTML to markdown quickly, export HTML as markdown
    and keep images intact with a simple Python script.
  name: How to convert HTML to markdown with images using Python
  steps:
  - name: '**Validate the source HTML** – malformed markup can cause missing elements
      in the markdown output. Use tools like `html5lib` or browser dev tools to clean
      up the HTML first.'
    text: '**Validate the source HTML** – malformed markup can cause missing elements
      in the markdown output. Use tools like `html5lib` or browser dev tools to clean
      up the HTML first.'
  - name: '**Keep the output folder writable** – the script needs permission to create
      the resource sub‑folder.'
    text: '**Keep the output folder writable** – the script needs permission to create
      the resource sub‑folder.'
  - name: '**Version‑control the markdown** – once generated, commit the `.md` files
      to your repository; the accompanying resource folder should be added to `.gitignore`
      if you don’t need version history for binary assets.'
    text: '**Version‑control the markdown** – once generated, commit the `.md` files
      to your repository; the accompanying resource folder should be added to `.gitignore`
      if you don’t need version history for binary assets.'
  - name: '**Test the markdown rendering** – open the resulting file in a markdown
      viewer (e.g., VS Code, Typora) to ensure images display as expected.'
    text: '**Test the markdown rendering** – open the resulting file in a markdown
      viewer (e.g., VS Code, Typora) to ensure images display as expected.'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Document conversion
title: How to convert HTML to markdown with images using Python
url: /python/general/how-to-convert-html-to-markdown-with-images-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to convert HTML to markdown with images using Python

If you need to **convert HTML to markdown** and keep all linked images, this guide gives you a complete, ready‑to‑run solution. Whether you’re migrating a blog, extracting documentation, or building a static‑site generator, the steps below let you **export HTML as markdown** in just a few seconds.

You’ll learn how to **save HTML page as markdown**, handle resource copying automatically, and avoid common pitfalls such as broken image links. The tutorial assumes you have basic Python knowledge and a recent version of the conversion library installed.

## Prerequisites

Before you start, make sure you have:

* Python 3.8+ installed (the code works on Windows, macOS, and Linux)
* The `groupdocs-conversion` (or compatible) package that provides `HTMLDocument`, `MarkdownSaveOptions`, `ResourceHandlingOptions`, and `Converter`. Install it with:

```bash
pip install groupdocs-conversion
```

* An HTML file you want to convert, e.g., `page.html`, located in a folder you can reference as `YOUR_DIRECTORY`.

> **Pro tip:** Keep your HTML and the target markdown folder together; the script will copy images into a sub‑folder next to the markdown file.

## Step 1: Load the HTML document you want to convert

The first operation creates an `HTMLDocument` object that represents the source file. This object gives the converter access to the DOM, styles, and linked resources.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you wish to convert
doc = HTMLDocument("YOUR_DIRECTORY/page.html")
```

*Why this matters*: Loading the document isolates it from the file system, allowing the converter to work with a clean, in‑memory representation. If the file path is incorrect, the constructor raises a clear `FileNotFoundError`, which you can catch for better error handling.

## Step 2: Create Markdown save options

`MarkdownSaveOptions` lets you fine‑tune how the output markdown is generated. For most scenarios the defaults are fine, but you must enable resource handling to keep images.

```python
from groupdocs.conversion import MarkdownSaveOptions

# Prepare options for the markdown output
opt = MarkdownSaveOptions()
```

*Why this matters*: The options object is where you control things like line endings, heading levels, and image handling. Without creating it, you would rely on the library’s defaults, which may omit images.

## Step 3: Configure resource handling to copy all linked resources

Images, CSS files, and other assets referenced in the HTML need to be saved alongside the markdown file. Setting `copy_resources` to `True` tells the converter to duplicate those files into a folder next to the markdown output.

```python
from groupdocs.conversion import ResourceHandlingOptions

# Enable copying of linked resources (images, CSS, etc.)
opt.resource_handling_options = ResourceHandlingOptions()
opt.resource_handling_options.copy_resources = True
```

*Why this matters*: If you skip this step, the generated markdown will contain image URLs that point to the original location, which often breaks when the markdown is moved. Enabling resource copying ensures a **markdown conversion with images** that works offline.

## Step 4: Convert the HTML document to Markdown using the configured options

Finally, invoke the `Converter.convert` method, passing the source document, the destination path, and the options you prepared.

```python
from groupdocs.conversion import Converter

# Perform the conversion
Converter.convert(doc, "YOUR_DIRECTORY/page.md", opt)
```

When the script finishes, you’ll find `page.md` in the same directory, and a sub‑folder named `page_files` (or similar) containing every image and stylesheet that was referenced in the original HTML.

### Expected output

Open `page.md` in any text editor. You should see markdown syntax for headings, paragraphs, lists, and image links that look like this:

```markdown
# Sample Title

Here is a paragraph from the original HTML.

![Alt text](page_files/image1.png)
```

All images are now stored locally, making the markdown file portable.

## Full, runnable script

Below is the complete script that combines all four steps. Save it as `convert_html_to_md.py` and run it with `python convert_html_to_md.py`.

```python
# convert_html_to_md.py
# This script converts an HTML file to markdown and copies all linked resources.
# It demonstrates a reliable "convert html to markdown" workflow with images.

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, ResourceHandlingOptions, Converter

# ------------------------------------------------------------
# Configuration – adjust these paths for your environment
# ------------------------------------------------------------
INPUT_HTML = "YOUR_DIRECTORY/page.html"   # Path to the source HTML file
OUTPUT_MD = "YOUR_DIRECTORY/page.md"      # Desired markdown output path

def main():
    # Step 1: Load the HTML document
    doc = HTMLDocument(INPUT_HTML)

    # Step 2: Create markdown save options
    opt = MarkdownSaveOptions()

    # Step 3: Enable resource copying so images stay linked
    opt.resource_handling_options = ResourceHandlingOptions()
    opt.resource_handling_options.copy_resources = True

    # Step 4: Execute the conversion
    Converter.convert(doc, OUTPUT_MD, opt)

    print(f"Conversion complete! Markdown saved to: {OUTPUT_MD}")

if __name__ == "__main__":
    main()
```

Run the script, and the console will confirm the conversion:

```
Conversion complete! Markdown saved to: YOUR_DIRECTORY/page.md
```

## Handling edge cases and common questions

| Question | Answer |
|----------|--------|
| **What if the HTML contains external images (e.g., `https://example.com/img.png`)?** | The converter downloads those images into the resource folder, provided the URL is reachable. If the server blocks the request, the image link will remain unchanged; you can manually download and place the file in the resource folder. |
| **Can I customize the image folder name?** | Yes. Set `opt.resource_handling_options.resource_folder_name = "my_images"` before conversion. |
| **How do I convert multiple HTML files in a batch?** | Wrap the conversion logic in a loop that iterates over a list of file paths. Re‑use the same `MarkdownSaveOptions` instance for efficiency. |
| **Is there a way to strip CSS styles?** | Set `opt.resource_handling_options.copy_css = False`. This removes linked CSS files while keeping the markdown content. |
| **Will tables be converted correctly?** | The library translates HTML tables to markdown table syntax. Complex nested tables may need manual adjustment. |

## Best practices for reliable **export html as markdown**

1. **Validate the source HTML** – malformed markup can cause missing elements in the markdown output. Use tools like `html5lib` or browser dev tools to clean up the HTML first.
2. **Keep the output folder writable** – the script needs permission to create the resource sub‑folder.
3. **Version‑control the markdown** – once generated, commit the `.md` files to your repository; the accompanying resource folder should be added to `.gitignore` if you don’t need version history for binary assets.
4. **Test the markdown rendering** – open the resulting file in a markdown viewer (e.g., VS Code, Typora) to ensure images display as expected.

## Conclusion

You now have a solid, production‑ready method to **convert HTML to markdown** while preserving images, which satisfies the need to **save HTML page as markdown** and **export HTML as markdown** in a single, automated step. By configuring `ResourceHandlingOptions`, the script guarantees a clean **markdown conversion with images** that works across platforms.

Next, consider exploring related topics such as **how to convert HTML to markdown** for large documentation sets, integrating the script into a CI pipeline, or extending it to support other output formats like PDF or DOCX. Happy converting!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}