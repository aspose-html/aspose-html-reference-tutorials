---
category: general
date: 2026-07-18
description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file in
  Python and also convert HTML to MHTML using simple libraries.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: en
lastmod: 2026-07-18
og_description: Convert HTML to EPUB in Python with a clear, runnable example. Also
  learn how to load HTML file in Python and convert HTML to MHTML in minutes.
og_image_alt: Diagram showing convert html to epub workflow
og_title: Convert HTML to EPUB in Python – Full Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
url: /python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide

Ever wondered how to **convert HTML to EPUB** without pulling your hair out? You're not the only one—developers constantly need to turn web pages into e‑books for offline reading, and doing it in Python is surprisingly painless. In this tutorial we'll walk through loading an HTML file in Python, converting that HTML to EPUB, and even turning the same source into MHTML for email‑friendly archives.

By the end of the guide you'll have a ready‑to‑run script that takes a single `sample.html` file and spits out both `sample.epub` and `sample.mhtml`. No mystery, just clear code and explanations.

---

![Conversion pipeline diagram](https://example.com/images/convert-html-epub.png "Diagram showing convert html to epub workflow")

## What You'll Build

- **Load an HTML file in Python** using the built‑in `pathlib` and `io` modules.  
- **Convert HTML to EPUB** with the `ebooklib` library, which handles the EPUB container format for you.  
- **Convert HTML to MHTML** (also known as MHT) using the `email` package, creating a single‑file web archive that browsers can open directly.  

We'll also cover:

- Required dependencies and how to install them.  
- Error handling so your script fails gracefully.  
- How to customize metadata like title and author for the EPUB file.  

Ready? Let’s dive in.

---

## Prerequisites

Before we start coding, make sure you have:

1. **Python 3.9+** – the syntax used here works on any recent version.  
2. **pip** – to install third‑party packages.  
3. A simple HTML file, e.g., `sample.html`, placed in a folder you control.  

If you already have those, great—skip to the next section.  

> **Pro tip:** Keep your HTML well‑formed (proper `<head>` and `<body>` sections). While `ebooklib` will try to fix minor issues, a clean source saves you headaches later.

---

## Step 1 – Install the Required Libraries

We need two external packages:

- **ebooklib** – for EPUB generation.  
- **beautifulsoup4** – optional, but handy for cleaning up the HTML before conversion.

Run this in your terminal:

```bash
pip install ebooklib beautifulsoup4
```

> **Why these libraries?** `ebooklib` builds the ZIP‑based EPUB structure for you, handling the `META‑INF` folder, `content.opf`, and `toc.ncx` automatically. `beautifulsoup4` lets us tidy up the HTML, ensuring the final e‑book renders correctly on all readers.

---

## Step 2 – Load the HTML File in Python

Loading an HTML file is straightforward, but we’ll wrap it in a tiny helper function that returns a **BeautifulSoup** object for later processing.

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**Explanation:**  
- `Path` gives us OS‑independent file handling.  
- Using `read_text` avoids manual `open`/`close` boilerplate.  
- Returning a `BeautifulSoup` object means we can later strip out scripts, fix broken tags, or inject a stylesheet before we **convert HTML to EPUB**.

---

## Step 3 – Convert HTML to EPUB

Now that we can **load HTML file in Python**, let’s transform it into a clean EPUB. The function below accepts a `BeautifulSoup` object, a destination path, and optional metadata.

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**Why this works:**  
- `ebooklib.epub.EpubBook` abstracts the ZIP container and required manifest files.  
- We generate a UUID as the identifier to avoid duplicate IDs if you create many books.  
- The `spine` tells readers the order of chapters; a single‑chapter book is sufficient for most simple HTML sources.  

**Running the conversion:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

When you execute the script, you’ll see a green check‑mark confirming the EPUB file’s location.

---

## Step 4 – Convert HTML to MHTML

MHTML (or MHT) bundles the HTML and all its resources (images, CSS) into a single MIME file. Python’s `email` package can build this format without external dependencies.

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**Key points:**  

- The `multipart/related` MIME type tells browsers that the HTML part and its resources belong together.  
- We loop through `<img>` tags to embed images; if you don’t need images, you can skip that block.  
- `Content-Location` uses a `file://` URI so browsers can resolve the resources internally.  

**Calling the function:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Now you have both `sample.epub` and `sample.mhtml` sitting side‑by‑side.

---

## Full Script – All Steps in One File

Below is the complete, ready‑to‑run script that combines everything. Save it as `convert_html.py` and replace `YOUR_DIRECTORY` with the path that holds your `sample.html`.

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
convert_html.py

A tiny utility that demonstrates:
- How to load an HTML file in Python
- How to convert HTML to EPUB (convert html to epub)
- How to convert HTML to MHTML (convert html to mhtml)

Author: Your Name
Date: 2026‑07‑18
"""

from pathlib import Path
import uuid
import mimetypes


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [How to Convert EPUB to Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}