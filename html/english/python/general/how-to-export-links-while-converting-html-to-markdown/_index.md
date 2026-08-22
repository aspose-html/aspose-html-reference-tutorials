---
category: general
date: 2026-08-22
description: How to export links from HTML and convert it to a markdown file, including
  paragraphs. Step‑by‑step guide for HTML to markdown conversion.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export links
- convert html to markdown
- how to convert html
- how to extract paragraphs
- html to markdown file
language: en
lastmod: 2026-08-22
og_description: How to export links from an HTML document and convert it to a markdown
  file, including paragraphs. Follow this complete tutorial for reliable HTML to markdown
  conversion.
og_image_alt: How to export links while converting HTML to Markdown
og_title: How to export links while converting HTML to Markdown – step-by-step guide
schemas:
- author: GroupDocs
  dateModified: '2026-08-22'
  description: How to export links from HTML and convert it to a markdown file, including
    paragraphs. Step‑by‑step guide for HTML to markdown conversion.
  headline: How to export links while converting HTML to Markdown
  type: TechArticle
tags:
- HTML conversion
- Markdown
- Python
title: How to export links while converting HTML to Markdown
url: /python/general/how-to-export-links-while-converting-html-to-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to export links while converting HTML to Markdown

If you need to **how to export links** from an HTML page and turn the result into a clean **html to markdown file**, this guide shows you the exact steps. You’ll also discover **how to extract paragraphs** so the markdown output contains the main content you care about. By the end of the tutorial you can answer the question “**how to convert html** to markdown” with a ready‑to‑run script.

Exporting links and extracting paragraphs are common tasks when you migrate web content to static sites, documentation portals, or headless CMS back‑ends. The approach below works with the GroupDocs Conversion SDK for Python, but the concepts apply to any library that lets you configure export features.

---

## What you’ll need

- Python 3.9 or newer  
- `groupdocs-conversion` package (install with `pip install groupdocs-conversion`)  
- An HTML file you want to process (e.g., `input.html`)  
- Basic familiarity with Python scripting  

---

## How to export links with HTML to Markdown conversion

The first major step is configuring the conversion so that only the desired features—links and paragraphs—are written to the **html to markdown file**. The SDK lets you set a bitmask of `MarkdownFeature` values; we combine `LINKS` and `PARAGRAPHS` to keep the output focused.

```python
# Import the required classes from the GroupDocs Conversion SDK
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

# Step 1: Load the source HTML document
html_doc = HTMLDocument("YOUR_DIRECTORY/input.html")

# Step 2: Create Markdown save options and select the features to export
markdown_options = MarkdownSaveOptions()
# Export only links and paragraphs from the HTML
markdown_options.features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

# Step 3: Convert the HTML to Markdown using the configured options
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)

print(f"Conversion complete. Markdown saved to {output_path}")
```

### Why this works

- **`HTMLDocument`** parses the original file and builds a DOM that the converter can walk.  
- **`MarkdownSaveOptions`** gives you fine‑grained control over what the SDK writes. Setting `features` to `LINKS | PARAGRAPHS` tells the engine to ignore images, tables, or scripts, which reduces noise in the final **html to markdown file**.  
- **`Converter.convert`** performs the heavy lifting. It respects the feature mask, extracts anchor tags (`<a>`) and paragraph tags (`<p>`), and writes them using standard Markdown syntax.

---

## How to convert HTML to Markdown with full content (optional)

If you later decide you need the entire page—not just links and paragraphs—simply adjust the feature mask:

```python
# Export everything the SDK supports (links, paragraphs, images, tables, etc.)
markdown_options.features = MarkdownFeature.ALL
```

Running the same conversion now produces a complete **html to markdown file** that mirrors the original layout. This demonstrates **how to convert html** in a flexible way: you control the output by toggling feature flags.

---

## How to extract paragraphs only

Sometimes you only care about the textual bodies of an article, not the hyperlinks. You can isolate paragraphs by setting the mask to `PARAGRAPHS` alone:

```python
markdown_options.features = MarkdownFeature.PARAGRAPHS
output_path = "YOUR_DIRECTORY/only_paragraphs.md"
Converter.convert(html_doc, markdown_options, output_path)
```

The resulting markdown will contain clean, line‑wrapped text without any link markup. This snippet answers the question **how to extract paragraphs** from an HTML source.

---

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Empty output file | The source HTML contains no `<a>` or `<p>` tags that match the selected features. | Verify the HTML structure or broaden the feature mask (e.g., include `HEADINGS`). |
| Encoding problems | The HTML uses a non‑UTF‑8 charset and the SDK reads it incorrectly. | Pass an explicit encoding to `HTMLDocument`, e.g., `HTMLDocument(path, encoding="iso-8859-1")`. |
| Over‑writing existing markdown | Running the script multiple times replaces the previous file. | Add a timestamp to the output filename or check `os.path.exists` before writing. |

**Pro tip:** When processing many files in a folder, wrap the conversion logic in a loop and log each result. This gives you a clear audit trail and makes it easy to resume after a failure.

---

## Full script you can copy‑paste

Below is a self‑contained Python file (`convert_links_paragraphs.py`) that you can run directly. It includes argument parsing so you can specify input and output paths without editing the code.

```python
#!/usr/bin/env python3
"""
convert_links_paragraphs.py

A complete example that shows how to export links and extract paragraphs
when converting HTML to a markdown file using GroupDocs Conversion SDK.
"""

import argparse
import os
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeature, Converter

def convert_html_to_md(input_html: str, output_md: str, features: int) -> None:
    """Perform the conversion with the given feature mask."""
    if not os.path.isfile(input_html):
        raise FileNotFoundError(f"Input file not found: {input_html}")

    # Load the HTML document
    html_doc = HTMLDocument(input_html)

    # Configure markdown options
    md_options = MarkdownSaveOptions()
    md_options.features = features

    # Run the conversion
    Converter.convert(html_doc, md_options, output_md)
    print(f"✅ Conversion finished – markdown saved to: {output_md}")

def main() -> None:
    parser = argparse.ArgumentParser(
        description="How to export links while converting HTML to Markdown."
    )
    parser.add_argument("input", help="Path to the source HTML file.")
    parser.add_argument(
        "output",
        help="Path for the resulting markdown file (e.g., links_and_paragraphs.md).",
    )
    parser.add_argument(
        "--links",
        action="store_true",
        help="Include links in the markdown output.",
    )
    parser.add_argument(
        "--paragraphs",
        action="store_true",
        help="Include paragraphs in the markdown output.",
    )
    args = parser.parse_args()

    # Build the feature mask based on user flags
    selected_features = 0
    if args.links:
        selected_features |= MarkdownFeature.LINKS
    if args.paragraphs:
        selected_features |= MarkdownFeature.PARAGRAPHS

    # Default to both links and paragraphs if no flag is provided
    if selected_features == 0:
        selected_features = MarkdownFeature.LINKS | MarkdownFeature.PARAGRAPHS

    try:
        convert_html_to_md(args.input, args.output, selected_features)
    except Exception as exc:
        print(f"❌ Conversion failed: {exc}")

if __name__ == "__main__":
    main()
```

**How to run**

```bash
python convert_links_paragraphs.py YOUR_DIRECTORY/input.html YOUR_DIRECTORY/links_and_paragraphs.md --links --paragraphs
```

The command above demonstrates **how to export links** and **how to extract paragraphs** in a single call. Omit `--links` or `--paragraphs` to tailor the output to your needs.

---

## Verification – what the output looks like

Given the following simple HTML (`input.html`):

```html
<!DOCTYPE html>
<html>
<head><title>Sample page</title></head>
<body>
  <p>Welcome to the tutorial.</p>
  <p>Visit <a href="https://example.com">our site</a> for more info.</p>
</body>
</html>
```

Running the script with both flags produces `links_and_paragraphs.md`:

```markdown
Welcome to the tutorial.

Visit [our site](https://example.com) for more info.
```

You can see that only the two paragraphs and the hyperlink are present—exactly what you asked for when you searched **how to export links** while performing **convert html to markdown**.

---

## Next steps and related topics

- **How to convert html to markdown** with images: add `MarkdownFeature.IMAGES` to the mask.  
- **How to extract paragraphs** and then post‑process


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Markdown to HTML Java - Convert with Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)
- [Convert HTML to Markdown – Complete C# Guide](/html/english/java/conversion-html-to-other-formats/convert-html-to-markdown-complete-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}