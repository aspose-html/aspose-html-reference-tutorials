---
category: general
date: 2026-10-02
description: Learn how to create SVG document in Python, save SVG to file, and export
  SVG image with a short, complete script.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: en
lastmod: 2026-10-02
og_description: Create SVG document in Python and export SVG image with this practical
  tutorial. Follow the script, save SVG to file, and reuse the vector graphic instantly.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Create SVG document in Python – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: How to create SVG document and export it as an image in Python
url: /python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create SVG document and export it as an image in Python

If you need to **create SVG document** programmatically, this tutorial shows you exactly how to do it with Python. You’ll see a complete script that builds a simple circle, saves the SVG to file, and produces an exportable SVG image you can embed anywhere.

Generating scalable vector graphics from code removes the manual effort of drawing shapes in a GUI editor. By the end of this guide you can integrate SVG creation into data‑visualisation pipelines, automated report generators, or any project that requires crisp, resolution‑independent graphics.

## Prerequisites

Before you start, ensure you have:

- Python 3.8 or newer installed
- The `svgwrite` library (install with `pip install svgwrite`)
- Write permission to the directory where the SVG will be saved

These requirements keep the example lightweight and compatible with most environments.

## Step 1: Install and import the SVG library

The first step is to add the third‑party library that provides a convenient API for SVG creation.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` abstracts the XML structure of an SVG file, letting you focus on geometry instead of raw markup.

## Step 2: Create an SVG document object

Now you can **create SVG document** by instantiating `svgwrite.Drawing`. This object represents the root `<svg>` element and holds all subsequent shapes.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

The `size` argument defines the rendered pixel dimensions, while `viewBox` establishes a coordinate system that matches the geometry you’ll define later.

## Step 3: Add a circle element

A circle is defined by its centre (`cx`, `cy`) and radius (`r`). Use the `circle` helper to attach these attributes.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

The circle sits in the middle of the 100 × 100 canvas, leaving a 10‑pixel margin on each side. Adjust `fill` and `stroke` to match your design language.

## Step 4: Save the SVG to file

With the graphic assembled, you can **save SVG to file** using the `save` method. This writes well‑formed XML that browsers and vector editors understand.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

The file `circle.svg` now resides in the current working directory. You can open it in a web browser, Inkscape, or any tool that supports the SVG format.

## Step 5: Verify the exported SVG image

Open the saved file in a browser to confirm the output. You should see a centered circle with the specified colors. The raw XML looks like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Because SVG is vector‑based, you can scale the image without loss of quality, making it ideal for responsive web designs or high‑resolution print.

## Pro tip: Export SVG as PNG or JPEG

If you need a raster version, combine the SVG file with a conversion tool such as **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

This step demonstrates **export SVG image** to a bitmap format, useful when downstream systems cannot render SVG directly.

## Common variations and edge cases

| Variation | How to handle |
|-----------|---------------|
| Multiple shapes | Call `dwg.add()` for each new element (rect, line, path). |
| Dynamic dimensions | Compute `size` and `viewBox` from data before creating `Drawing`. |
| Text labels | Use `dwg.text("Label", insert=("10", "20"))` and style with `font_size` and `fill`. |
| Re‑using the document | Keep the `Drawing` object in memory and call `save()` whenever you need an updated file. |
| Large files | Stream the output using `dwg.tostring()` and write to a file object manually to avoid memory spikes. |

Addressing these scenarios ensures your **how to generate SVG** script scales from simple icons to complex diagrams.

## Full script recap

Below is the complete, runnable example that incorporates all steps and optional conversion:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Running this script produces `circle.svg` and, if `cairosvg` is installed, `circle.png`. Both files are ready for inclusion in web pages, reports, or further processing.

## Conclusion

You now know how to **create SVG document** in Python, **save SVG to file**, and **export SVG image** for broader use. The example covers the essential API calls, explains why each step matters, and offers extensions for more complex graphics. 

Next, explore additional **SVG Python tutorial** topics such as drawing paths, applying gradients, and animating elements. Integrating these techniques will let you generate dynamic, data‑driven vector graphics directly from your Python applications. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}