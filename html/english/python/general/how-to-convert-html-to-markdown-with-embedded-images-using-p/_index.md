---
category: general
date: 2026-10-12
description: convert HTML to markdown quickly and learn how to embed images in markdown.
  This guide walks through html to markdown conversion python with full code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to embed images in markdown
- html to markdown conversion python
- how to convert html page to markdown
language: en
lastmod: 2026-10-12
og_description: convert HTML to markdown and embed images in markdown using Python.
  Follow this complete tutorial for reliable html to markdown conversion python.
og_image_alt: Screenshot showing a Python script that converts an HTML file to a markdown
  file with base64‑encoded images
og_title: Convert HTML to markdown with embedded images in Python – step‑by‑step guide
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: convert HTML to markdown quickly and learn how to embed images in markdown.
    This guide walks through html to markdown conversion python with full code.
  headline: How to convert HTML to markdown with embedded images using Python
  type: TechArticle
tags:
- markdown
- html
- python
- document conversion
title: How to convert HTML to markdown with embedded images using Python
url: /python/general/how-to-convert-html-to-markdown-with-embedded-images-using-p/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to convert HTML to markdown with embedded images using Python

If you need to **convert HTML to markdown** while preserving every image, this guide shows you exactly how to do it. By configuring the conversion engine to embed images as Base64, you get a single, self‑contained `.md` file that works everywhere—from GitHub READMEs to static site generators.

You’ll also learn **how to embed images in markdown**, why the built‑in resource handling options are the most reliable choice, and how to perform an **html to markdown conversion python** in just a few lines of code.

## What you’ll achieve

- Transform any local HTML page into a clean Markdown document.  
- Embed every image directly into the Markdown file as a Base64 string, eliminating broken links.  
- Run the process on any platform that supports Python 3.9+ and the GroupDocs Conversion library.

## Prerequisites

| Requirement | Reason |
|------------|--------|
| Python 3.9 or newer | Required by the GroupDocs Conversion SDK. |
| `groupdocs-conversion` package | Provides `Converter`, `HTMLDocument`, `MarkdownSaveOptions`, and `ResourceHandlingOptions`. |
| An existing HTML file (e.g., `page.html`) | The source you want to convert. |
| Write permission to the output folder | To save the generated `.md` file. |

Install the SDK with pip:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** Use a virtual environment (`python -m venv .venv`) to keep dependencies isolated.

## Step 1: Configure resource handling to embed images in markdown

When the conversion engine encounters an `<img>` tag, it can either copy the image to a separate folder or embed it directly. Embedding produces a Base64‑encoded data URI, which is exactly what **how to embed images in markdown** requires.

```python
from groupdocs.conversion import ResourceHandlingOptions

# Create a resource handling configuration
resource_options = ResourceHandlingOptions()
# Enable embedding of images as Base64 data URIs
resource_options.embed_images = True   # Embeds images directly in the Markdown file
```

**Why this matters:**  
Embedding guarantees that the Markdown file remains portable. If you share the `.md` file without the accompanying image folder, the images will still render correctly on any platform that supports data URIs (GitHub, GitLab, VS Code preview, etc.).

## Step 2: Set up Markdown save options using the resource configuration

The `MarkdownSaveOptions` class lets you pass the `resource_options` created above. It also lets you fine‑tune line endings, heading styles, and more, but for most cases the defaults work fine.

```python
from groupdocs.conversion import MarkdownSaveOptions

# Attach the resource handling to the markdown save options
markdown_options = MarkdownSaveOptions(resource_handling_options=resource_options)
```

**What happens under the hood:**  
During conversion, the engine scans the HTML DOM, converts each element to its Markdown equivalent, and replaces `<img src="...">` with `![alt text](data:image/...;base64,...)`. The `resource_options.embed_images` flag triggers this behavior.

## Step 3: Convert the HTML document to markdown and save the result

Now you bind everything together: load the source HTML, apply the save options, and write the output file.

```python
from groupdocs.conversion import Converter, HTMLDocument

# Path to the source HTML file
source_path = "YOUR_DIRECTORY/page.html"
# Desired output path for the markdown file
output_path = "YOUR_DIRECTORY/page.md"

# Perform the conversion
Converter.convert_html(
    HTMLDocument(source_path),
    markdown_options,
    output_path
)

print(f"✅ Conversion complete! Markdown saved to: {output_path}")
```

**Expected output:**  

- `page.md` contains Markdown text, headings, lists, and **embedded images** as Base64 strings.  
- Opening `page.md` in a Markdown viewer displays the original HTML layout, including all images, without any external assets.

### Full script for quick copy‑paste

```python
# convert_html_to_markdown.py
from groupdocs.conversion import (
    Converter,
    HTMLDocument,
    MarkdownSaveOptions,
    ResourceHandlingOptions,
)

def convert_html_to_markdown(src_html: str, dst_md: str) -> None:
    """Convert an HTML file to markdown with images embedded as Base64."""
    # 1️⃣ Embed images
    resource_opts = ResourceHandlingOptions()
    resource_opts.embed_images = True

    # 2️⃣ Prepare markdown options
    md_opts = MarkdownSaveOptions(resource_handling_options=resource_opts)

    # 3️⃣ Run conversion
    Converter.convert_html(
        HTMLDocument(src_html),
        md_opts,
        dst_md
    )
    print(f"✅ Markdown file created at: {dst_md}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    convert_html_to_markdown(
        src_html="YOUR_DIRECTORY/page.html",
        dst_md="YOUR_DIRECTORY/page.md"
    )
```

Run the script:

```bash
python convert_html_to_markdown.py
```

## Handling common edge cases

| Situation | Solution |
|-----------|----------|
| **Large images cause huge markdown files** | Limit image size before embedding by resizing them in the HTML or using an image‑optimization library (e.g., Pillow) before conversion. |
| **Relative image URLs point outside the project** | Ensure the HTML references are reachable, or copy those images into the same folder before conversion. |
| **You need separate image files instead of embedding** | Set `resource_options.embed_images = False` and provide a `resource_folder` path where images will be saved. |
| **Conversion fails on malformed HTML** | Pre‑process the HTML with `BeautifulSoup` (`html5lib` parser) to clean up broken tags before feeding it to the converter. |

## Verifying the result

Open the generated `page.md` in any Markdown viewer:

```bash
code YOUR_DIRECTORY/page.md   # VS Code preview
```

You should see the original headings, paragraphs, and images rendered correctly. If an image appears as a broken link, double‑check that `embed_images` is set to `True` and that the source HTML contains valid `<img>` tags.

## Next steps and related topics

- **Export to other formats** – The same `Converter` class can produce PDF, DOCX, or plain text. Swap `MarkdownSaveOptions` for `PdfSaveOptions` or `DocxSaveOptions`.  
- **Batch processing** – Loop over a directory of HTML files to produce a collection of Markdown documents.  
- **Custom image handling** – Implement a callback via `ResourceHandlingOptions` to store images in a CDN and replace the data URI with a CDN URL.  
- **Advanced markdown features** – Enable GitHub‑flavored markdown (tables, task lists) by adjusting `markdown_options` properties.

By mastering **html to markdown conversion python**, you now have a repeatable, production‑ready workflow that guarantees images stay with the content. Feel free to experiment with the options above and adapt the script to your own content pipelines.

---


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Create PDF from Markdown using Aspose HTML Converter (Java)](/html/english/java/conversion-html-to-other-formats/create-pdf-from-markdown-using-aspose-html-converter-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}