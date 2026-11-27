---
category: general
date: 2026-11-27
description: Create SVG document and save SVG file using Python. Learn to export vector
  as SVG and generate a SVG image quickly.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: en
lastmod: 2026-11-27
og_description: Create SVG document and save SVG file with Python. This guide shows
  you how to export vector as SVG and produce a SVG image in minutes.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Create SVG document and save SVG file using Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Create SVG document and save SVG file with Python
url: /python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create SVG document and save SVG file with Python

If you need to **create SVG document** from scratch, this guide walks you through the entire process. You’ll see how to **save SVG file** on disk, export the vector as SVG, and end up with a ready‑to‑use SVG image in just a few lines of code.

Generating scalable graphics programmatically is useful for reports, UI icons, or any situation where you want resolution‑independent images. By the end of this tutorial you’ll be able to answer “**how to create SVG**?” for simple shapes and extend the pattern to complex vector artwork.

## What you’ll need

- Python 3.8 or newer  
- The `svgwrite` package (installable via `pip`)  
- A writable directory for the output file  

No external graphics editors are required; everything runs from the command line.

## Step 1: Install the `svgwrite` library

`svgwrite` provides a clean, Pythonic API for building SVG markup. Install it once with:

```bash
pip install svgwrite
```

> **Pro tip:** Use a virtual environment (`python -m venv .venv`) to keep dependencies isolated.

## Step 2: Create SVG document

Now we actually **create SVG document** objects. The `Drawing` class represents the root `<svg>` element and handles namespaces automatically.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

The `Drawing` instance is the entry point for all subsequent SVG operations. By specifying `size` we set the canvas dimensions, which influences how browsers render the image.

## Step 3: Add a red circle element

Adding shapes is straightforward. The `circle` method creates a `<circle>` element; we then attach it to the root.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Why we choose a circle: circles are vector primitives that demonstrate scalability without any loss of quality, making the output ideal for testing **export vector as SVG** workflows.

## Step 4: Save SVG file

Finally, write the markup to disk. This step fulfills the **save SVG file** requirement and produces a file you can open in any browser or vector editor.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

When you run the script, you’ll see a console message confirming the location of the generated file.

### Expected output

The resulting `circle.svg` contains:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Opening the file in a browser displays a crisp red circle, and because it’s vector‑based you can zoom indefinitely without pixelation.

## Step 5: Common variations and edge cases

### Exporting more complex vectors

If you need to **export vector as SVG** for multi‑shape illustrations, simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`, `path`, etc.). For example:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Handling Unicode and text

SVG supports text elements with full Unicode support. Use `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` to embed multilingual labels.

### Saving to a different location

When **save SVG image** to a user‑specified folder, validate the path to avoid permission errors:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Minifying the output

For production pipelines, you might want a smaller file size. Pass `pretty=False` to `dwg.tostring()` and write the result manually:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## How to create SVG with alternative libraries (optional)

While `svgwrite` is lightweight and pure‑Python, other ecosystems exist:

- **cairosvg** – converts PNG, PDF, or HTML to SVG.  
- **lxml** – lets you build SVG markup manually using XML APIs.  

Choosing a library depends on your project’s complexity and existing dependencies.

## Conclusion

You now know how to **create SVG document**, add vector shapes, and **save SVG file** using Python. The complete solution demonstrates the steps to **export vector as SVG**, generate a **SVG image**, and answer the common query **how to create SVG** programmatically.

From here you can:

- Extend the script with loops to generate charts or icons automatically.  
- Integrate the SVG output into web applications or email templates.  
- Explore animation by adding `<animate>` elements with `svgwrite`.

Experiment with different shapes, colors, and gradients to fully harness the power of scalable vector graphics in your Python projects. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create SVG Document – Add a Circle and Save as SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Load SVG File Python – Complete Guide to Export, Embed & Convert](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}