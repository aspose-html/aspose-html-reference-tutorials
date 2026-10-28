---
category: general
date: 2026-10-28
description: 'convert html to markdown using Python: learn to extract links from HTML
  and save as GitLab‑flavored Markdown in just three steps.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- how to convert html document
language: en
lastmod: 2026-10-28
og_description: convert html to markdown quickly with Python. This guide shows how
  to extract links from HTML and produce GitLab‑flavored Markdown in three easy steps.
og_image_alt: Screenshot of Python script converting HTML to GitLab‑flavored Markdown
  with extracted links
og_title: Convert HTML to Markdown and extract links with Python
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: 'convert html to markdown using Python: learn to extract links from
    HTML and save as GitLab‑flavored Markdown in just three steps.'
  headline: How to convert HTML to Markdown and extract links in Python
  type: TechArticle
- description: 'convert html to markdown using Python: learn to extract links from
    HTML and save as GitLab‑flavored Markdown in just three steps.'
  name: How to convert HTML to Markdown and extract links in Python
  steps:
  - name: Multiple input sources
    text: 'If you need to batch‑process a folder of HTML files, wrap the conversion
      in a loop:'
  - name: Missing links
    text: When an HTML document contains no `<a>` elements, the converter still creates
      a valid Markdown file containing only the permitted paragraphs. No additional
      error handling is required, but you can check `save_options.features` if you
      need to enforce the presence of links.
  - name: Custom output encoding
    text: 'If your target system expects UTF‑8 with a BOM, set the encoding on the
      `MarkdownSaveOptions`:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Conversion
title: How to convert HTML to Markdown and extract links in Python
url: /python/general/how-to-convert-html-to-markdown-and-extract-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to convert HTML to Markdown and extract links in Python

If you need to **convert HTML to Markdown**, this tutorial gives you a complete, ready‑to‑run solution. You’ll see how to extract links from HTML, choose the GitLab‑flavored Markdown formatter, and save the result with just a few lines of code.

The guide covers everything you need: required packages, loading HTML from different sources, configuring `MarkdownSaveOptions`, and handling edge cases such as missing links or custom output directories. By the end you’ll be able to answer the question *how to convert HTML document* into clean, link‑rich Markdown for any downstream workflow.

## Prerequisites

- Python 3.8 or newer
- `aspose-html` package (the official Aspose.HTML library for Python)
- Basic familiarity with Python scripts and file I/O

You can install the library with:

```bash
pip install aspose-html
```

> **Pro tip:** Use a virtual environment to keep dependencies isolated.

## Step 1: Load the HTML content

The first step is to create an `HTMLDocument` object. Aspose.HTML accepts a string, a file path, or a URL, so you can pick the source that matches your project.

```python
from aspose.html import HTMLDocument

# Example 1: Load from a raw HTML string
html_string = "<h1>Title</h1><p>Sample <a href='https://example.com'>link</a></p>"
html_doc = HTMLDocument(html_string)

# Example 2: Load from a local file
# html_doc = HTMLDocument("input.html")

# Example 3: Load from a remote URL
# html_doc = HTMLDocument("https://www.example.com")
```

> **Why this matters:** Loading the document once gives you a DOM‑like object that the converter can traverse, ensuring that all links and paragraph nodes are available for extraction.

## Step 2: Configure Markdown save options

`MarkdownSaveOptions` lets you control the output format and which HTML features are translated. To **extract links from HTML** while keeping paragraphs, enable the `LINK` and `PARAGRAPH` features and select the GitLab formatter.

```python
from aspose.html import MarkdownSaveOptions

save_options = MarkdownSaveOptions()
# Use GitLab‑flavored Markdown (supports task lists, tables, etc.)
save_options.formatter = MarkdownSaveOptions.Formatter.GIT

# Export only links and paragraphs – other tags (e.g., images) are ignored
save_options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

> **Why this matters:** Limiting features reduces noise in the output and guarantees that the resulting Markdown contains only the elements you care about—perfect for documentation pipelines or static site generators.

## Step 3: Convert the HTML document and write the file

Now call `Converter.convert_html`, passing the document, the options, and the destination path.

```python
from aspose.html import Converter

output_path = "output.md"  # Change to your desired directory/file name
Converter.convert_html(html_doc, save_options, output_path)
print(f"Markdown file saved to {output_path}")
```

Running the script produces a file `output.md` with the following content:

```markdown
# Title

Sample [link](https://example.com)
```

Notice that only the heading, paragraph, and link appear—exactly what we asked for when configuring `save_options`.

## Handling common variations and edge cases

### Multiple input sources

If you need to batch‑process a folder of HTML files, wrap the conversion in a loop:

```python
import pathlib
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

input_folder = pathlib.Path("html_inputs")
output_folder = pathlib.Path("markdown_outputs")
output_folder.mkdir(exist_ok=True)

options = MarkdownSaveOptions()
options.formatter = MarkdownSaveOptions.Formatter.GIT
options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)

for html_path in input_folder.glob("*.html"):
    doc = HTMLDocument(str(html_path))
    md_path = output_folder / (html_path.stem + ".md")
    Converter.convert_html(doc, options, str(md_path))
    print(f"Converted {html_path.name} → {md_path.name}")
```

### Missing links

When an HTML document contains no `<a>` elements, the converter still creates a valid Markdown file containing only the permitted paragraphs. No additional error handling is required, but you can check `save_options.features` if you need to enforce the presence of links.

### Custom output encoding

If your target system expects UTF‑8 with a BOM, set the encoding on the `MarkdownSaveOptions`:

```python
save_options.encoding = "utf-8-sig"
```

## Full, runnable example

Putting everything together, here’s a self‑contained script you can copy‑paste and run immediately:

```python
# convert_html_to_markdown.py
# -------------------------------------------------
# Demonstrates how to convert HTML to Markdown while
# extracting only links and paragraphs using Aspose.HTML.
# -------------------------------------------------

from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def main():
    # 1️⃣ Load HTML – replace this with your own source if needed
    html = "<h1>Title</h1><p>Sample <a href='https://example.com'>link</a></p>"
    document = HTMLDocument(html)

    # 2️⃣ Configure Markdown options (GitLab flavor, links + paragraphs only)
    options = MarkdownSaveOptions()
    options.formatter = MarkdownSaveOptions.Formatter.GIT
    options.features = (
        MarkdownSaveOptions.Features.LINK |
        MarkdownSaveOptions.Features.PARAGRAPH
    )

    # 3️⃣ Convert and save
    output_file = "output.md"
    Converter.convert_html(document, options, output_file)
    print(f"✅ Markdown saved to {output_file}")

if __name__ == "__main__":
    main()
```

Execute with:

```bash
python convert_html_to_markdown.py
```

You’ll see `output.md` containing the expected Markdown representation.

## Conclusion

You now know how to **convert HTML to Markdown** in Python, extract links from HTML, and control the output format with `MarkdownSaveOptions`. This approach works for single files, batches, or even remote URLs, giving you a flexible foundation for documentation generators, static site pipelines, or data‑extraction scripts.

**Next steps**

- Experiment with other `MarkdownSaveOptions.Features` such as `TABLE` or `IMAGE` to include more HTML elements.
- Switch the formatter to `MarkdownSaveOptions.Formatter.CommonMark` if you need strict CommonMark compliance.
- Combine this conversion with a static‑site generator (e.g., MkDocs) to automate content publishing.

Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to Markdown Python – extract links & paragraphs](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [Convert HTML to Markdown in Python – GitLab Flavored Guide](/html/english/python/general/convert-html-to-markdown-in-python-gitlab-flavored-guide/)
- [Convert HTML to Markdown with Python – Complete Guide](/html/english/python/general/convert-html-to-markdown-with-python-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}