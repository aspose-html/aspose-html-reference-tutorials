---
category: general
date: 2026-10-02
description: convert HTML to Markdown in Python with a complete example. Learn how
  to save HTML as Markdown, choose formatters, and enable specific features.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- save html as markdown
- how to convert html
- html to markdown conversion
- html to markdown python
language: en
lastmod: 2026-10-02
og_description: convert HTML to Markdown in Python with practical code, formatter
  options, and feature flags. Follow this guide to save HTML as Markdown quickly.
og_image_alt: Screenshot of Python code converting HTML to Markdown
og_title: Convert HTML to Markdown in Python – full tutorial
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: convert HTML to Markdown in Python with a complete example. Learn how
    to save HTML as Markdown, choose formatters, and enable specific features.
  headline: How to convert HTML to Markdown in Python – step‑by‑step guide
  type: TechArticle
- description: convert HTML to Markdown in Python with a complete example. Learn how
    to save HTML as Markdown, choose formatters, and enable specific features.
  name: How to convert HTML to Markdown in Python – step‑by‑step guide
  steps:
  - name: Enabling only the needed features
    text: You can fine‑tune the output by turning on specific feature flags. In this
      example we keep **links** and **paragraphs** while disabling images, tables,
      and other constructs.
  - name: Expected output (`output.md`)
    text: '```markdown # Project Overview'
  - name: Missing or malformed `href` attributes
    text: 'If an `<a>` tag lacks a valid `href`, the converter inserts the link text
      without a URL. To preserve readability, you may want to post‑process the Markdown:'
  - name: Converting large HTML files
    text: 'For multi‑megabyte HTML files, stream the input to avoid loading the entire
      markup into memory:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
title: How to convert HTML to Markdown in Python – step‑by‑step guide
url: /python/general/how-to-convert-html-to-markdown-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to convert HTML to Markdown in Python – step‑by‑step guide

If you need to **convert HTML to Markdown**, this guide shows you a complete, runnable solution in Python. You’ll see how to **save HTML as Markdown**, pick the right formatter, and enable only the features you care about.

Converting HTML to Markdown is a common task when you want lightweight documentation, static‑site content, or version‑controlled text files. This tutorial covers everything from installing the library to handling edge cases, so you can apply the technique to any HTML source.

## Prerequisites

Before you start, make sure you have:

* Python 3.8 or newer installed.
* `pip` access to install third‑party packages.
* Basic familiarity with HTML tags and Markdown syntax.

No additional system dependencies are required because the conversion library is pure Python.

## Install the GroupDocs Conversion library

The code sample uses the **GroupDocs.Conversion** Python package, which provides `HTMLDocument`, `MarkdownSaveOptions`, and `Converter`. Install it with:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** Use a virtual environment (`python -m venv venv`) to keep the package isolated from other projects.

## Step 1: Create an `HTMLDocument` from a string

The first step is to wrap your raw HTML in an `HTMLDocument` instance. This object abstracts the source, whether it comes from a string, a file, or a remote URL.

```python
from groupdocs.conversion import HTMLDocument

# Example HTML – you can replace this with any valid markup
html_content = "<h1>Title</h1><p>Hello <a href='https://example.com'>world</a></p>"
html_doc = HTMLDocument(html_content)
```

*Why this matters:* `HTMLDocument` parses the markup once, allowing the converter to work with a normalized representation instead of raw text.

## Step 2: Configure `MarkdownSaveOptions`

`MarkdownSaveOptions` lets you control the output format and which Markdown features are emitted. The library supports two formatters:

* **DEFAULT** – standard CommonMark‑compatible Markdown.
* **GIT** – Git‑flavored Markdown (adds tables, strikethrough, etc.).

For most version‑control scenarios, the **GIT** formatter is preferred.

```python
from groupdocs.conversion import MarkdownSaveOptions

md_opts = MarkdownSaveOptions()
md_opts.formatter = MarkdownSaveOptions.Formatter.GIT
```

### Enabling only the needed features

You can fine‑tune the output by turning on specific feature flags. In this example we keep **links** and **paragraphs** while disabling images, tables, and other constructs.

```python
md_opts.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

*Why this matters:* Limiting features reduces the size of the generated file and prevents unexpected Markdown elements that downstream tools might not support.

## Step 3: Convert the document

With the source `HTMLDocument` and the configured `MarkdownSaveOptions`, conversion is a single call to `Converter.convert`. Provide an absolute or relative path for the output file.

```python
from groupdocs.conversion import Converter

output_path = "output.md"
Converter.convert(html_doc, output_path, md_opts)
```

After the call finishes, `output.md` contains the Markdown representation of the original HTML.

## Full script you can run today

Below is the complete, self‑contained script that incorporates all previous steps. Save it as `html_to_md.py` and run `python html_to_md.py`.

```python
# html_to_md.py
# Complete example that converts HTML to Markdown using GroupDocs.Conversion

from groupdocs.conversion import Converter, HTMLDocument, MarkdownSaveOptions

# 1️⃣  Create the HTMLDocument – replace the string with your own HTML source
html_content = """
<h1>Project Overview</h1>
<p>Welcome to the <a href="https://github.com/example">example repo</a>.</p>
<ul>
  <li>Feature A</li>
  <li>Feature B</li>
</ul>
"""
html_doc = HTMLDocument(html_content)

# 2️⃣  Prepare Markdown save options
md_opts = MarkdownSaveOptions()
md_opts.formatter = MarkdownSaveOptions.Formatter.GIT  # Git‑flavored Markdown
md_opts.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH |
    MarkdownSaveOptions.Features.LIST      # include lists for this example
)

# 3️⃣  Perform the conversion
output_path = "output.md"
Converter.convert(html_doc, output_path, md_opts)

print(f"Conversion complete – Markdown saved to {output_path}")
```

### Expected output (`output.md`)

```markdown
# Project Overview

Welcome to the [example repo](https://github.com/example).

- Feature A
- Feature B
```

The output matches the original HTML structure while exposing only the features we enabled (links, paragraphs, and lists).

## Handling common edge cases

### Missing or malformed `href` attributes

If an `<a>` tag lacks a valid `href`, the converter inserts the link text without a URL. To preserve readability, you may want to post‑process the Markdown:

```python
import re

def fix_broken_links(md_text):
    # Replace stray brackets like [text]() with just the text
    return re.sub(r'\[([^\]]+)\]\(\)', r'\1', md_text)

with open(output_path, "r+", encoding="utf-8") as f:
    content = f.read()
    f.seek(0)
    f.write(fix_broken_links(content))
    f.truncate()
```

### Converting large HTML files

For multi‑megabyte HTML files, stream the input to avoid loading the entire markup into memory:

```python
with open("large_input.html", "r", encoding="utf-8") as src:
    html_doc = HTMLDocument(src.read())
```

The conversion process itself remains unchanged because `HTMLDocument` abstracts away the source size.

## Alternative formatters

If you prefer plain CommonMark rather than Git‑flavored output, switch the formatter:

```python
md_opts.formatter = MarkdownSaveOptions.Formatter.DEFAULT
```

This yields a more minimal Markdown file, useful when you target platforms that do not support Git extensions.

## Related tasks you might explore next

* **Convert Markdown back to HTML** – useful for previewing documentation.
* **Export HTML to PDF** – another common **html to markdown conversion**‑adjacent workflow.
* **Batch process a folder of HTML files** – loop over files and reuse the same `MarkdownSaveOptions` instance.

All of these follow the same pattern: create a source document, configure save options, and call `Converter.convert`.

## Conclusion

You now know how to **convert HTML to Markdown** in Python, how to **save HTML as Markdown** with precise feature control, and why selecting the right formatter matters for downstream tools. The example demonstrates a clean, reusable approach that works for single strings, files, or URLs, and it includes tips for handling missing links and large inputs.

Feel free to experiment with additional `MarkdownSaveOptions.Features` (e.g., `IMAGE`, `TABLE`) to tailor the output to your project's needs. If you found this guide helpful, share it with teammates or link to it from your project documentation. Happy converting!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}