---
category: general
date: 2026-07-02
description: Create SVG document quickly with Python. Learn to save SVG file, generate
  a basic SVG image, and export SVG from code in just a few lines.
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: en
og_description: Create SVG document easily. This guide shows how to generate SVG,
  save SVG file, and export SVG from code with a clean Python example.
og_title: Create SVG Document – Quick Python Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: Create SVG Document – Step‑by‑Step Guide for Beginners
url: /python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create SVG Document – Step‑by‑Step Guide for Beginners

Ever wondered how to **create SVG document** without opening a graphics editor? You're not the only one. Whether you need a tiny icon for a web page or a dynamic chart generated on the fly, being able to **create SVG document** programmatically saves time and keeps everything version‑controlled.

In this tutorial we’ll walk through a complete, runnable example that shows you exactly how to **create SVG document**, **save SVG file**, and even answer the lingering “**how to generate SVG**” question that pops up when you’re automating graphics. By the end you’ll have a red square sitting on disk, and you’ll know how to **export SVG from code** for any future project.

## What You’ll Need

Before we dive in, make sure you have:

* Python 3.9 or newer (the standard library does all the heavy lifting)
* A text editor or IDE you like—VS Code, PyCharm, or even Notepad will do
* Write permission to a folder where you’ll **save SVG file** (we’ll use a `output/` directory)

No external packages are required, so the setup is literally a couple of minutes.

## Step 1: Set Up the SVG Helper Functions (Create the Document)

First things first: we need a tiny helper that builds the XML structure behind an SVG. Think of this as the canvas on which we’ll **create basic SVG image** elements later.

```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**Why this step matters:** The `SVGDocument` class abstracts away the low‑level XML fiddling. By wrapping it in a class we keep the rest of the code clean, which is a best practice when you **export SVG from code** in larger applications.

## Step 2: Add a Rectangle – The Core of a **Create Basic SVG Image** Example

Now that we have a document object, let’s sprinkle in a red square. This is the heart of the **create basic SVG image** portion of the tutorial.

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**Explanation:**  
* The rectangle’s `x` and `y` coordinates give it a 10‑pixel margin so it doesn’t sit flush against the edge.  
* Using a dictionary for attributes makes the code readable and mirrors how you’d **save SVG file** attributes in any XML‑based format.  
* If you ever need to **how to generate SVG** shapes other than rectangles, just change the tag to `"circle"` or `"path"` and adjust the attribute dictionary accordingly.

## Step 3: Persist the SVG – Finally **Save SVG File** to Disk

We’ve built the document in memory; now we’ll write it out. This is the moment where the abstract **create SVG document** becomes a tangible file you can open in a browser.

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**What you’ll see:** Opening `output/square.svg` in Chrome, Firefox, or any SVG‑aware viewer will display a simple red square with a thin white border (the background of the SVG canvas). That’s the proof that we’ve successfully **exported SVG from code**.

## Full Script – One‑File Solution

Below is the entire script, ready to copy‑paste into `create_svg.py`. Running `python create_svg.py` will generate the file described above.

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### Expected Output

Running the script prints:

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

And the generated `square.svg` looks like this (simplified view):

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

Opening the file renders a crisp red square—exactly what we set out to **create basic SVG image**.

## Extending the Example – Common Questions Answered

### How can I add text or other shapes?

Just call `svg.create_element("text", {...})` or `svg.create_element("circle", {...})` and append them just like the rectangle. The same **how to generate SVG** logic applies.

### What if I need to **export SVG from code** with a transparent background?

Remove any `fill` attribute from the root `<svg>` element or set `fill="none"` on shapes that should be transparent. The XML stays valid; browsers will render the transparency automatically.

### Can I **save SVG file** with pretty‑printed formatting?

`ElementTree` writes compact XML by default. For a human‑readable version, you can use `xml.dom.minidom` to re‑format:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

Replace `svg.save(output_path)` with `pretty_save(svg, output_path)`.

### What about performance for large SVGs?

When generating thousands of elements, consider building a list of `ET.Element` objects first and then extending the root in one go. This reduces the number of tree mutations and speeds up the **save SVG file** operation.

## Pro Tips & Pitfalls

* **Pro tip:** Always use absolute paths (or `pathlib.Path`) when **saving SVG file**; relative paths can break when your script runs from a different working directory.  
* **Watch out for:** Forgetting to register the SVG namespace. Without `ET.register_namespace("", SVGDocument.SVG_NS)`, the output will contain a redundant `ns0` prefix that some browsers misinterpret.  
* **Typical mistake:** Mixing integer and string types in attribute values. XML expects strings, so we cast everything with `str()`—the helper class does this for you, but if you bypass it, you might get a `TypeError`.  

## Conclusion

We’ve just walked through a complete, end‑to‑end example that shows how to **create SVG document**, **save SVG file**, and answer


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}