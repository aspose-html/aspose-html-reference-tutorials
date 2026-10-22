---
category: general
date: 2026-10-21
description: Learn how to convert HTML to PNG quickly. This tutorial also covers export
  webpage to PNG and convert HTML file to PNG with Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: en
lastmod: 2026-10-21
og_description: Convert HTML to PNG with Python. Follow this clear guide to export
  webpage to PNG, handle edge cases, and automate image generation.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: Convert HTML to PNG in Python – complete programming guide
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: How to convert HTML to PNG in Python – step‑by‑step guide
url: /python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to PNG in Python – complete programming guide

If you need to **convert HTML to PNG**, this guide shows you a reliable way to do it with plain Python. Whether you’re exporting a static report, generating thumbnails for a gallery, or automating screenshots for testing, you’ll get a full, runnable solution in minutes.

You’ll also see how to **export webpage to PNG**, understand the difference between converting an HTML file versus a live URL, and learn the best practices for handling large pages or dynamic content. No external services are required—just a few Python packages and a short script.

## Prerequisites

Before you start, make sure you have:

- Python 3.9+ installed (the code works on Windows, macOS, and Linux)
- Access to a terminal or command prompt
- Basic familiarity with Python’s package manager (`pip`)

You’ll need the `imgkit` package (a thin wrapper around `wkhtmltoimage`) and the `wkhtmltoimage` binary itself. Both are free and open‑source.

## Step 1: Install the required tools

The first step is to install `wkhtmltoimage` and the Python wrapper that talks to it.

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **Why this step matters** – `wkhtmltoimage` renders HTML using the WebKit engine, producing pixel‑perfect PNGs. `imgkit` simply forwards your options to the binary, so you get the same quality you would from a browser.

## Step 2: Verify the installation

Run a quick check to confirm that the binary is reachable from Python.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

If the script prints the path to `wkhtmltoimage`, you’re ready to convert HTML to PNG. If you get an `OSError`, double‑check that the binary is on your system `PATH`.

## Step 3: Write a reusable conversion function

Encapsulating the logic in a function makes it easy to **convert HTML file to PNG** or **export webpage to PNG** from anywhere in your project.

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **Why we wrap both `from_file` and `from_url`** – The same function now supports **how to convert HTML to image** for local files and live webpages, keeping your code DRY (Don’t Repeat Yourself).

## Step 4: Convert a local HTML file to PNG

Place an HTML file called `sample.html` in a folder named `assets`. Then call the helper we just defined:

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### Expected output

Running the script prints:

```
✅ Successfully saved PNG to: output/sample.png
```

A new file `output/sample.png` now contains a pixel‑perfect snapshot of `sample.html`. Opening it in any image viewer shows the rendered page exactly as it would appear in a browser.

## Step 5: Export a live webpage to PNG

If you need to **export webpage to PNG** for a URL that changes frequently (e.g., a dashboard), just pass the URL string instead of a file path.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Why adjust viewport size?

Web pages designed for desktop screens often look cramped if rendered at a small width. By increasing the `width` and `height` options, you capture the full layout, which is especially useful for **export webpage to PNG** tasks.

## Step 6: Handle common edge cases

### 6.1 Large pages or infinite scroll

For pages that load content lazily (e.g., infinite scroll), increase the JavaScript delay and optionally set a larger viewport:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Authentication‑protected pages

If a page requires a session cookie, you can embed the cookie header:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Missing images or fonts

`wkhtmltoimage` respects the `--disable-local-file-access` flag for security. If your HTML references local assets, enable them explicitly:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Step 7: Verify the result programmatically (optional)

Sometimes you need to confirm that the PNG was generated correctly (e.g., in CI pipelines). The following snippet checks the file size and dimensions:

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

If the PNG passes these checks, you can safely use it in downstream processes such as PDF generation, email attachments, or machine‑learning pipelines.

## Conclusion

You now have a complete, production‑ready method to **convert HTML to PNG** using Python. The guide covered:

- Installing `wkhtmltoimage` and `imgkit`
- Verifying the environment
- A reusable `convert_html_to_png` function that handles both local files and URLs
- Real‑world examples for **export webpage to PNG**, **how to convert HTML to image**, and **convert HTML file to PNG**
- Edge‑case handling for large pages, authentication, and local assets
- Optional verification steps for CI/CD pipelines

Feel free to experiment with additional `imgkit` options—such as `zoom`, `crop-h`, or `crop-w`—to fine‑tune the output for your specific use case. For next steps, you might explore:

- Converting the PNGs into a PDF report (`img2pdf` library)
- Automating batch conversion of an entire folder of HTML files
- Using Selenium for pages that require full browser rendering (e.g., heavy JavaScript frameworks)

Happy coding, and enjoy the pixel‑perfect screenshots!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to PNG – Complete Python Guide](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Convert HTML to PNG in Python – Complete Streaming Save Guide](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}