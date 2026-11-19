---
category: general
date: 2026-07-31
description: Learn how to create SVG document, add a circle, and save SVG file quickly.
  Export graphic as SVG with a few lines of Python code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: en
lastmod: 2026-07-31
og_description: Create SVG document, add a circle, and save SVG file in seconds. This
  guide shows you how to export graphic as SVG with clear, runnable code.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Create SVG Document – Add a Circle and Save as SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: Create SVG Document – Add a Circle and Save as SVG
url: /python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create SVG Document – Add a Circle and Save as SVG

Ever needed to **create SVG document** from code but weren’t sure where to start? You’re not alone; many developers hit that wall when they first dabble with vector graphics. In this tutorial we’ll walk through a tiny, self‑contained example that shows you how to **add circle to SVG**, then **save SVG file** so you can **export graphic as SVG** for use on the web or in design tools.

We’ll keep things lightweight: just a few lines of Python, a popular SVG helper library, and a dash of explanation. By the end you’ll have a ready‑to‑use `circle.svg` sitting in your folder, and you’ll understand why each step matters—no vague “see docs” shortcuts.

## What You’ll Need

- Python 3.8+ (any recent version works)
- The `svgwrite` package – install it with `pip install svgwrite`
- A text editor or IDE (VS Code, PyCharm, or even Notepad will do)
- Write permission to the directory where you want the file saved

That’s it. No heavyweight dependencies, no external services.

## Step 1: Set Up the SVG Document

Creating an SVG document is as simple as instantiating a `Drawing` object from `svgwrite`. Think of this object as the blank canvas where every shape lives.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Why this matters:** The `Drawing` class handles all the XML boilerplate for you—namespaces, headers, and the root `<svg>` element. By specifying a filename up front we already know where the file will end up, which makes the later **save svg file** step trivial.

### Pro tip
If you plan to generate many files in a loop, give each `Drawing` a unique name or use `io.BytesIO` to keep everything in memory until you’re ready to write.

## Step 2: Add a Circle to the SVG

Now that the document exists, let’s **add circle to SVG**. The `add()` method accepts any shape object; a `Circle` is perfect for a simple red dot in the center.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Why we use `center` and `radius` variables:** Hard‑coding numbers makes the code harder to read and maintain. By naming the values we clarify intent—this circle sits smack‑in‑the‑middle of a 200 × 200 canvas and is large enough to be noticeable.

### Edge case – Transparent background
If you need a transparent background (the default for SVG), you can skip setting a `fill` on the root. For a white background, add:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Place this before adding the circle so the rectangle sits underneath.

## Step 3: Save the SVG File

With the shape in place, the final act is to **save SVG file**. The `save()` method writes the XML to disk, and because we already gave the `Drawing` a filename, a single call does the job.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **What happens under the hood?** `svgwrite` serializes the element tree to a string, adds the XML declaration, and writes it using UTF‑8 encoding. If the target directory doesn’t exist, Python will raise a `FileNotFoundError`; make sure the path is valid or create it with `os.makedirs()`.

### Bonus: Export graphic as SVG programmatically

If you need the SVG content as a string—for example, to embed it in an HTML email—you can call `dwg.tostring()` instead of `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Full Working Example

Putting it all together, here’s a complete, ready‑to‑run script:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Expected output:** After running the script, you’ll see a `circle.svg` file in the same folder. Opening it in a browser or any vector editor shows a red circle centered on a white square—exactly what we programmed.

## Common Questions & Gotchas

- **What if I want a different shape?** Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>` string. The API is consistent across shapes.
- **Can I embed the SVG directly in HTML?** Absolutely. The file you just created can be referenced with `<img src="circle.svg" alt="Red circle">` or inlined with `<svg>` tags.
- **Why not write raw XML?** You could, but libraries like `svgwrite` handle namespace quirks and make the code far more maintainable—especially when you start adding gradients or animations.

## Conclusion

You now know how to **create SVG document**, **add circle to SVG**, and **save SVG file** so you can **export graphic as SVG** with just a handful of Python lines. The pattern scales: replace the circle with any vector shape, loop over data to generate charts, or batch‑process assets for a design system. 

Next steps? Try adding text labels, experimenting with gradients, or generating a whole gallery of icons in a single script. If you’re curious about more advanced features, check out the `svgwrite` documentation on groups (`<g>`), transforms, and animation support.

Happy coding, and may your vectors always stay crisp!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}