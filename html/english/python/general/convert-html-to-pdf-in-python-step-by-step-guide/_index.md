---
category: general
date: 2026-08-06
description: Convert HTML to PDF in Python with a complete example. Learn to generate
  PDF from HTML, save HTML as PDF, and handle common edge cases.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: en
lastmod: 2026-08-06
og_description: Convert HTML to PDF in Python and automate document creation. Follow
  this guide to generate PDF from HTML, save HTML as PDF, and customize output.
og_image_alt: Example of convert html to pdf script in Python
og_title: Convert HTML to PDF in Python – comprehensive tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: Convert HTML to PDF in Python – step‑by‑step guide
url: /python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to PDF in Python – step‑by‑step guide

If you need to **convert HTML to PDF** quickly, this tutorial shows a complete solution in Python. You will see how to generate PDF from HTML, save HTML as PDF, and control the conversion process without leaving your code.

The guide walks you through installing a reliable library, loading an HTML document, performing the conversion, and verifying the result. By the end you can create PDF from HTML file in any Python project, whether the source is a static page or dynamically generated markup.

## What you will learn

* Install the `pdfkit` and `wkhtmltopdf` dependencies required for HTML‑to‑PDF conversion.  
* Load an HTML document from disk or a string.  
* Generate PDF from HTML with custom page size, margin, and encoding options.  
* Save HTML as PDF using a single function call.  
* Handle typical edge cases such as missing assets, Unicode characters, and large files.  

**Prerequisites** – Python 3.8+ and basic familiarity with file I/O. No external services are required.

## Convert HTML to PDF – overall workflow

The conversion process consists of three logical phases:

1. **Preparation** – install the converter and ensure the `wkhtmltopdf` binary is reachable.  
2. **Input handling** – read the HTML file or build the markup programmatically.  
3. **Output generation** – invoke the converter, write the PDF file, and confirm the result.

Each phase is covered in a dedicated step below.

## Step 1: Install required libraries

`pdfkit` provides a thin Python wrapper around the widely used `wkhtmltopdf` engine. Install both with `pip` and verify the binary path.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

If you prefer a portable binary, download the appropriate release from the [wkhtmltopdf GitHub page](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) and place it in a directory that is added to your `PATH`. The script later checks the path automatically.

## Step 2: Load the HTML document

You can read a static file, fetch remote content, or construct HTML on the fly. The example below loads a local file called `sample.html` located in a directory you define.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

Reading the file as a Unicode string ensures that characters such as “é”, “ß”, or Asian glyphs are preserved during the conversion. This step is essential when you **generate PDF from HTML** that contains international text.

## Step 3: Generate PDF from HTML

`pdfkit.from_string` converts a string containing HTML markup into a PDF file. You can pass a dictionary of options to control page size, margins, and header/footer behavior.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

The call above **creates PDF from HTML file** stored in `sample.pdf`. If the source HTML references local CSS or images, the `enable‑local‑file‑access` flag lets `wkhtmltopdf` resolve those resources.

### Why this approach works

* `pdfkit` delegates the heavy lifting to `wkhtmltopdf`, which renders HTML with the WebKit engine, guaranteeing high fidelity to the original layout.  
* Providing an options dictionary lets you fine‑tune the output without modifying the HTML itself.  
* Using `from_string` keeps the workflow in memory, which is useful when the HTML is generated on the fly.

## Step 4: Save HTML as PDF and verify output

After the conversion, you may want to confirm that the PDF exists and is readable. The snippet below checks the file size and opens the PDF with the default system viewer (platform‑specific).

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

Running the script prints a success message and launches the PDF viewer so you can instantly confirm that the layout matches the original HTML. This step completes the **save html as pdf** cycle.

## Step 5: Advanced options – create PDF from HTML file with custom settings

Sometimes you have a physical HTML file on disk and prefer `pdfkit.from_file` instead of loading the content yourself. This method is handy when the HTML already includes complex relative paths.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

You can also embed a cover page, table of contents, or JavaScript execution flags by extending the `options` dictionary. For example, to add a cover page:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

These tweaks demonstrate **how to convert HTML to PDF** for more sophisticated publishing pipelines.

## Common pitfalls and how to avoid them

| Issue | Cause | Remedy |
|-------|-------|--------|
| Images or CSS do not appear | `wkhtmltopdf` blocks local file access by default | Add `"enable-local-file-access": None` to the options dictionary |
| Unicode characters become garbled | Missing `encoding` option or reading file with the wrong charset | Always set `"encoding": "UTF-8"` and read the HTML file with UTF‑8 |
| PDF is blank | Incorrect path to `wkhtmltopdf` binary | Provide the path explicitly: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Large HTML files cause timeout | Default timeout too short | Set `"javascript-delay": "2000"` or increase the timeout with `"timeout": "60"` |

Addressing these issues ensures a reliable **generate pdf from html** process across different environments.

## Full script – end‑to‑end example

Save the following as `html_to_pdf.py` and run it with `python html_to_pdf.py`. Adjust `YOUR_DIRECTORY` to point at your project folder.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}