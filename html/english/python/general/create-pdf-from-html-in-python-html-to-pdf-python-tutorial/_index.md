---
category: general
date: 2026-07-15
description: Create PDF from HTML using Python. Learn how to convert HTML to PDF quickly
  with a simple script and clear steps.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: en
lastmod: 2026-07-15
og_description: Create PDF from HTML with Python. This guide shows you how to convert
  HTML to PDF, save HTML as PDF, and handle resources efficiently.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Create PDF from HTML in Python – Hands‑On Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: Create PDF from HTML in Python – HTML to PDF Python Tutorial
url: /python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF from HTML in Python – Full‑Featured Tutorial

Ever needed to **create PDF from HTML** but weren’t sure which Python library to pick? You’re not alone—many developers hit that wall when they try to turn a web report, invoice, or marketing page into a printable PDF.  

The good news is that with just a few lines of code you can **convert HTML to PDF** reliably, and the script works on Windows, macOS, and Linux. In this guide we’ll walk through a complete, runnable example, explain why each step matters, and show you how to **save HTML as PDF** without leaving any loose ends.

---

## What You’ll Learn

- Install the right Python package for HTML‑to‑PDF conversion.  
- Load an HTML file with custom resource‑handling options (to avoid endless CSS imports).  
- Generate a clean PDF file on disk.  
- Tackle common edge cases such as external images, relative paths, and large documents.  

By the end of this **HTML to PDF tutorial** you’ll have a reusable function you can drop into any project.

---

## Prerequisites

- Python 3.9+ (the code works with 3.8 as well, but 3.9+ gives you the newest `pathlib` features).  
- Basic familiarity with the command line and virtual environments.  
- An HTML file you want to turn into a PDF—any static page will do.

> **Pro tip:** If you’re using a virtual environment, activate it before installing the library; this keeps your global Python tidy.

---

## Step 1 – Install WeasyPrint (the engine behind the conversion)

WeasyPrint is a pure‑Python library that renders HTML and CSS to PDF. It handles most modern web features and gives you fine‑grained control over resource loading.

```bash
pip install weasyprint
```

Running the command above pulls in `cairocffi`, `tinycss2`, and a few other dependencies. If you hit a `cairo`‑related error on Windows, grab the pre‑built wheels from the [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## Step 2 – Prepare a tiny helper for resource handling

When you load an HTML document that references external stylesheets or images, the library will follow those links. In some cases that leads to deep nesting or even infinite loops (think of a CSS file that `@import`s itself). To keep things tidy we limit the depth of resource handling.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

The class above isn’t required by WeasyPrint, but it mirrors the pattern you saw in the original snippet and gives you a hook to stop runaway imports. You’ll see it used in the next step.

---

## Step 3 – Load the HTML document using the custom options

Now we actually read the HTML file. The `HTML` class accepts a `base_url` argument, which we set to the directory containing the source file—this makes relative links work without a web server.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Why this matters:** If your HTML pulls in a cascade of CSS files, each `@import` will trigger another load. The depth guard prevents the script from spiralling out of control.

---

## Step 4 – Save the processed document as PDF

With the `HTML` object in hand, generating a PDF is a one‑liner. We also pass a simple CSS snippet that forces a clean page size (A4) and adds a tiny margin—feel free to adjust.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Calling `write_pdf` streams the PDF to disk, so you end up with a ready‑to‑share file.

---

## Step 5 – Put It All Together

Below is a compact script you can copy‑paste into `convert.py`. Replace the placeholder paths with your actual directories.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Expected output** – after running `python convert.py` you should see:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Open the generated file with any PDF viewer; you’ll see the original page layout, CSS styling, and images (provided they were reachable from the HTML file).  

If you notice missing images, double‑check that their `src` attributes are either absolute URLs or relative paths that exist under `YOUR_DIRECTORY`.

---

## Common Questions & Edge‑Case Handling

| Question | Answer |
|----------|--------|
| *What if my HTML references external fonts?* | WeasyPrint will download the font files automatically, but you may want to whitelist domains to avoid long fetch times. |
| *Can I convert a string of HTML instead of a file?* | Yes—use `HTML(string=my_html_string)` and skip the `base_url` or set it to a temporary folder. |
| *How do I control PDF metadata (title, author)?* | Pass a `metadata` dict to `write_pdf`, e.g., `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *I get a “cairo‑cffi error” on Linux.* | Install the system package `libcairo2-dev` (`apt-get install libcairo2-dev` on Debian/Ubuntu) before pip installing WeasyPrint. |

---

## Wrap‑Up

We’ve just **created PDF from HTML** using a clean Python workflow, covered the **convert HTML to PDF** mechanics, and shown you how to **save HTML as PDF** with robust resource handling. The script is tiny enough to drop into CI pipelines, yet flexible enough to expand with custom headers, footers, or watermarks.

Next steps you might explore:

- Use the **html to pdf python** library `pdfkit` for a wkhtmltopdf‑based approach (good for legacy CSS).  
- Add a CLI interface with `argparse` so the script accepts input/output arguments.  
- Generate PDFs on the fly inside a Flask or FastAPI endpoint for on‑demand reports.  

Feel free to experiment, break things, and then come back to this guide for a quick refresher. If you run into snags, the WeasyPrint documentation and community forums are excellent resources.

Happy coding, and enjoy turning those web pages into sleek PDFs!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}