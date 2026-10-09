---
category: general
date: 2026-10-09
description: Learn how to embed images while converting HTML to Markdown in Python
  using Aspose.HTML. Includes embed images as Base64 and markdown with embedded images.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed images
- convert html to markdown
- html to markdown python
- embed images as base64
- markdown with embedded images
language: en
lastmod: 2026-10-09
og_description: How to embed images while converting HTML to Markdown in Python. This
  guide shows embed images as Base64 and produces markdown with embedded images.
og_image_alt: Screenshot of a Markdown file that contains embedded images generated
  by a Python HTML‑to‑Markdown conversion
og_title: How to embed images when converting HTML to Markdown in Python
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn how to embed images while converting HTML to Markdown in Python
    using Aspose.HTML. Includes embed images as Base64 and markdown with embedded
    images.
  headline: How to embed images when converting HTML to Markdown in Python
  type: TechArticle
- description: Learn how to embed images while converting HTML to Markdown in Python
    using Aspose.HTML. Includes embed images as Base64 and markdown with embedded
    images.
  name: How to embed images when converting HTML to Markdown in Python
  steps:
  - name: '**Resize images before conversion** – Use Pillow (`pip install pillow`)
      to shrink images to a reasonable resolution (e.g., 800 px width) before embedding.'
    text: '**Resize images before conversion** – Use Pillow (`pip install pillow`)
      to shrink images to a reasonable resolution (e.g., 800 px width) before embedding.'
  - name: '**Limit embedding to specific formats** – If you only need PNGs embedded,
      adjust `resource_opts` to filter by MIME type:'
    text: '**Limit embedding to specific formats** – If you only need PNGs embedded,
      adjust `resource_opts` to filter by MIME type:'
  - name: Import Aspose.HTML classes and create `MarkdownSaveOptions`.
    text: Import Aspose.HTML classes and create `MarkdownSaveOptions`.
  - name: Set `ResourceHandlingOptions.embed_resources` and `embed_images_as_base64`
      to `True`.
    text: Set `ResourceHandlingOptions.embed_resources` and `embed_images_as_base64`
      to `True`.
  - name: Attach those options to the markdown save settings.
    text: Attach those options to the markdown save settings.
  - name: Call `Converter.convert` with the source HTML and destination Markdown paths.
    text: Call `Converter.convert` with the source HTML and destination Markdown paths.
  type: HowTo
tags:
- Python
- Aspose.HTML
- Markdown conversion
- Image embedding
title: How to embed images when converting HTML to Markdown in Python
url: /python/general/how-to-embed-images-when-converting-html-to-markdown-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to embed images when converting HTML to Markdown in Python

If you need to **how to embed images** during an HTML‑to‑Markdown conversion, this guide gives you a complete, ready‑to‑run solution. Using Aspose.HTML for Python you can embed images as Base‑64 strings so the resulting Markdown file contains the images inline. This eliminates broken links and makes the document portable.

In addition to embedding images, the tutorial shows you how to **convert HTML to Markdown** in a Pythonic way, covering the *html to markdown python* workflow, configuring **embed images as Base64**, and producing **markdown with embedded images** that works in any Markdown viewer.

By the end of this article you will have a single script that:

* Reads an HTML file from disk.  
* Embeds every referenced image directly into the Markdown output as a Base‑64 data URI.  
* Saves the final Markdown file ready for distribution or version control.

## Prerequisites

Before you start, make sure you have:

* Python 3.8 or newer installed.  
* A valid Aspose.HTML for Python license (the free trial works for evaluation).  
* `pip install aspose-html` executed in your virtual environment.  
* An HTML file (`input.html`) that references local or remote images.

If any of these items are missing, install them now to avoid runtime errors.

## Step 1: Set up the Aspose.HTML environment

First, import the classes you need and create a `MarkdownSaveOptions` instance. The `MarkdownSaveOptions` object holds conversion settings, including the resource handling options we will configure later.

```python
# Step 1: Import required Aspose.HTML classes
from aspose.html import Converter, ResourceHandlingOptions, MarkdownSaveOptions

# Initialize Markdown save options (you can customize other settings here)
markdown_opts = MarkdownSaveOptions()
```

**Why this step matters:**  
`Converter` performs the heavy lifting, while `MarkdownSaveOptions` tells the converter exactly how to treat resources such as images, scripts, and stylesheets. Without initializing `markdown_opts`, you cannot attach the resource‑handling configuration that enables image embedding.

## Step 2: Configure resource handling to embed images as Base64

Aspose.HTML provides `ResourceHandlingOptions`. Setting `embed_resources = True` tells the converter to replace external image references with Base‑64 data URIs.

```python
# Step 2: Create and configure resource handling options
resource_opts = ResourceHandlingOptions()
resource_opts.embed_resources = True          # Embed images directly in the output
resource_opts.embed_images_as_base64 = True   # Explicitly request Base64 encoding for images

# Attach the resource options to the markdown save options
markdown_opts.resource_handling_options = resource_opts
```

**Why this step matters:**  
When `embed_resources` is `True`, the converter scans the HTML for `<img>` tags, fetches each image, encodes it, and injects a `data:image/...;base64,` URI into the Markdown. This produces **markdown with embedded images**, which is ideal for documentation that must travel with the source file (e.g., in a Git repository).

## Step 3: Perform the conversion from HTML to Markdown

Now you can call `Converter.convert`, passing the source HTML path, the target Markdown path, and the configured `markdown_opts`.

```python
# Step 3: Define source and destination paths
html_path = "YOUR_DIRECTORY/input.html"
markdown_path = "YOUR_DIRECTORY/with_images.md"

# Step 4: Convert HTML to Markdown, embedding images
Converter.convert(html_path, markdown_path, markdown_opts)
```

**Why this step matters:**  
`Converter.convert` reads the HTML, processes all resources according to the options you set, and writes a Markdown file that contains the same visual content—images included—without external dependencies.

## Step 4: Verify the generated Markdown

Open `with_images.md` in any Markdown previewer (VS Code, GitHub, Typora, etc.). You should see the images rendered exactly as they appeared in the original HTML. The image links will look similar to:

```markdown
![Alt text](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...)
```

If the previewer shows broken images, double‑check that:

* The original HTML referenced images that are reachable (local files exist, remote URLs are accessible).  
* The `embed_images_as_base64` flag is set to `True`.  

## Step 5: Handling large images and performance considerations

Embedding very large images can inflate the Markdown file size dramatically. Here are two practical tips:

1. **Resize images before conversion** – Use Pillow (`pip install pillow`) to shrink images to a reasonable resolution (e.g., 800 px width) before embedding.  
2. **Limit embedding to specific formats** – If you only need PNGs embedded, adjust `resource_opts` to filter by MIME type:

```python
resource_opts.allowed_image_formats = ["png"]  # Only embed PNG images
```

These adjustments keep the Markdown lightweight while still providing the portability you need.

## Common pitfalls and how to resolve them

| Issue | Cause | Fix |
|-------|-------|-----|
| Images appear as broken links | `embed_resources` left as `False` | Ensure `resource_opts.embed_resources = True`. |
| Markdown file size > 10 MB | Very large high‑resolution images | Resize images or embed only essential ones. |
| Remote images not embedded | Network timeout or blocked URL | Verify internet connectivity or download images locally before conversion. |
| Unexpected characters in Base64 string | Binary file not read correctly | Make sure the image files are not corrupted and have proper file permissions. |

## Extending the solution: Convert multiple HTML files in a batch

If you need to process a folder of HTML files, wrap the conversion logic in a loop:

```python
import os

input_dir = "YOUR_DIRECTORY/html_files"
output_dir = "YOUR_DIRECTORY/markdown_output"

for filename in os.listdir(input_dir):
    if filename.lower().endswith(".html"):
        src_path = os.path.join(input_dir, filename)
        dst_path = os.path.join(output_dir, os.path.splitext(filename)[0] + ".md")
        Converter.convert(src_path, dst_path, markdown_opts)
        print(f"Converted {filename} → {os.path.basename(dst_path)}")
```

This snippet demonstrates **convert html to markdown** at scale while preserving the **embed images as base64** behavior for each file.

## Recap

You now know **how to embed images** when you **convert HTML to Markdown** using Python. The key steps are:

1. Import Aspose.HTML classes and create `MarkdownSaveOptions`.  
2. Set `ResourceHandlingOptions.embed_resources` and `embed_images_as_base64` to `True`.  
3. Attach those options to the markdown save settings.  
4. Call `Converter.convert` with the source HTML and destination Markdown paths.  

The result is **markdown with embedded images** that can be shared without worrying about missing assets.

## Next steps

* Explore other `ResourceHandlingOptions` such as `embed_stylesheets` if you need inline CSS.  
* Combine this workflow with a static site generator (e.g., MkDocs) to build documentation pipelines.  
* Experiment with different image formats and compression levels to balance quality and file size.

Feel free to adapt the script to your own project requirements, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Convert markdown to html – Java guide with PDF output](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}