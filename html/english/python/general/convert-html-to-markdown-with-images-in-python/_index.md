---
category: general
date: 2026-11-17
description: Convert HTML to markdown with images in Python – learn how to convert
  HTML quickly while exporting images intact.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to convert html
- export html with images
- markdown conversion with images
language: en
lastmod: 2026-11-17
og_description: Convert HTML to markdown with images in Python. This tutorial shows
  how to convert HTML while exporting images, giving you a complete, ready‑to‑run
  solution.
og_image_alt: Diagram showing convert html to markdown workflow with image extraction
og_title: Convert HTML to markdown with images in Python – quick guide
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Convert HTML to markdown with images in Python – learn how to convert
    HTML quickly while exporting images intact.
  headline: Convert HTML to markdown with images in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Image extraction
title: Convert HTML to markdown with images in Python
url: /python/general/convert-html-to-markdown-with-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to markdown with images in Python

If you need to **convert HTML to markdown** while keeping images as separate files, this guide shows you exactly how to do it. You’ll get a complete, runnable example that handles external resources, so your markdown output references the original images correctly.

Exporting HTML with images often trips up simple converters because they either drop the images or embed them as base64 strings. By configuring the resource handling options, you retain the original image files and produce clean markdown that can be version‑controlled or edited later.

In this tutorial you will:

* Load an HTML document from disk.  
* Configure the converter to **export HTML with images** as separate files.  
* Save the result as markdown using the **markdown conversion with images** options.  

The only prerequisite is a recent version of the Aspose.HTML for Python library (or any compatible API that provides `HTMLDocument`, `ResourceHandlingOptions`, `MarkdownSaveOptions`, and `Converter`). You also need Python 3.8+ and write permission to the output folder.

---

## Prerequisites and installation

1. Install the Aspose.HTML package:

   ```bash
   pip install aspose-html
   ```

2. Verify the installation:

   ```python
   import aspose.html as ah
   print(ah.__version__)   # should print the installed version, e.g., 22.9
   ```

> **Pro tip:** Use a virtual environment to avoid version conflicts with other projects.

---

## Step 1: Load the source HTML document

The first step is to create an `HTMLDocument` object that represents the source file. This object parses the markup and builds a DOM tree that the converter can traverse.

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*Why this matters* – Loading the document gives the library full control over the markup, allowing it to resolve relative URLs and apply resource handling later.

---

## Step 2: Configure external resource handling

When you **export HTML with images**, you usually want the images saved beside the markdown file rather than embedded. The `ResourceHandlingOptions` class lets you specify that behavior.

```python
from aspose.html import ResourceHandlingOptions

resource_options = ResourceHandlingOptions()
resource_options.save_external_resources = True   # keep images as separate files
```

Setting `save_external_resources` to `True` instructs the converter to copy each external resource (images, CSS, fonts) to a folder next to the markdown output. The markdown file will contain relative links pointing to those copies.

---

## Step 3: Attach the resource handling configuration to markdown options

`MarkdownSaveOptions` controls how the conversion to markdown occurs. By assigning the `resource_handling_options` property, you enable the **markdown conversion with images** feature.

```python
from aspose.html import MarkdownSaveOptions

markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

If you omit this step, the converter will strip image references or embed them as data URIs, which defeats the purpose of exporting images.

---

## Step 4: Perform the conversion

Finally, call `Converter.convert` with the source document, the target path, and the options you prepared.

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/sample.md"
Converter.convert(html_doc, output_path, markdown_options)
```

After the call completes, you will find:

* `sample.md` – the markdown version of the original HTML.  
* A sub‑folder named `sample_files` (or similar) containing every image referenced in the HTML.

---

## Full working script

Putting all pieces together gives you a single script you can run from the command line:

```python
# convert_html_to_markdown.py
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, MarkdownSaveOptions, Converter

def convert_html_to_markdown(html_file: str, markdown_file: str):
    """
    Convert an HTML file to markdown while exporting images as separate files.
    """
    # 1. Load the HTML document
    html_doc = HTMLDocument(html_file)

    # 2. Set up resource handling to keep images external
    res_opts = ResourceHandlingOptions()
    res_opts.save_external_resources = True

    # 3. Attach resource handling to markdown options
    md_opts = MarkdownSaveOptions()
    md_opts.resource_handling_options = res_opts

    # 4. Convert and save
    Converter.convert(html_doc, markdown_file, md_opts)
    print(f"Conversion complete: {markdown_file}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    src_html = os.path.abspath("YOUR_DIRECTORY/sample.html")
    dst_md   = os.path.abspath("YOUR_DIRECTORY/sample.md")

    convert_html_to_markdown(src_html, dst_md)
```

**Expected output**

```
Conversion complete: /absolute/path/YOUR_DIRECTORY/sample.md
```

After execution, open `sample.md` in any markdown editor. Image links will appear as:

```markdown
![Alt text](sample_files/image1.png)
```

The images themselves reside in the `sample_files` folder, ready for version control or further processing.

---

## Handling common edge cases

| Situation                              | Recommended approach |
|----------------------------------------|----------------------|
| **Missing image files**                | The converter logs a warning and leaves a broken link. Verify that all `<img src>` attributes point to reachable resources before conversion. |
| **Relative URLs that point outside the project folder** | Use `ResourceHandlingOptions.base_url` to provide a base URL so the converter can resolve the paths correctly. |
| **Large HTML files with many images**  | Set `resource_options.max_resource_size` (if available) to limit the size of resources that are copied. |
| **Non‑PNG/JPEG image formats**        | The library automatically copies the original format. Ensure the target markdown viewer supports the format (e.g., SVG). |
| **Write‑permission errors**           | Run the script with appropriate permissions or choose an output directory where you have write access. |

---

## Tips for a smooth **markdown conversion with images**

* Keep the output folder clean: delete the `*_files` directory before each run if you want a fresh set of images.  
* Use meaningful `alt` attributes in the original HTML; they become the markdown image captions automatically.  
* If you need to embed images as base64 (for a single‑file markdown), set `resource_options.save_external_resources = False`. This is the opposite of **export html with images**, but useful for email or documentation embeds.  
* When converting a batch of files, wrap the script in a loop and adjust `resource_options.resource_folder` to avoid name collisions.

---

## Frequently asked questions

**Q: Does this work with HTML fragments that lack a full `<html>` wrapper?**  
A: Yes. `HTMLDocument` can parse fragments; the converter treats them as


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to embed images in HTML to Markdown conversion using Python](/html/english/python/general/how-to-embed-images-in-html-to-markdown-conversion-using-pyt/)
- [Convert HTML to Markdown – Complete Guide with CSS & Images](/html/english/python/general/convert-html-to-markdown-complete-guide-with-css-images/)
- [Convert HTML to Markdown with Aspose – Complete Python Guide](/html/english/python/general/convert-html-to-markdown-with-aspose-complete-python-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}