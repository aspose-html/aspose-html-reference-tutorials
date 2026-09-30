---
category: general
date: 2026-08-03
description: Convert HTML to Markdown using Python. Learn how to extract links from
  HTML and extract paragraphs from HTML in a single, efficient conversion.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- extract paragraphs from html
language: en
lastmod: 2026-08-03
og_description: Convert HTML to Markdown in Python with a concise example that shows
  how to extract links from HTML and extract paragraphs from HTML while saving the
  result as a Markdown file.
og_image_alt: Screenshot of Python code converting an HTML file to Markdown with selected
  links and paragraphs
og_title: Convert HTML to Markdown in Python – full extraction guide
schemas:
- author: GroupDocs
  dateModified: '2026-08-03'
  description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  headline: Convert HTML to Markdown Python – extract links & paragraphs
  type: TechArticle
- description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  name: Convert HTML to Markdown Python – extract links & paragraphs
  steps:
  - name: Load the HTML document you want to convert
    text: '```python from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions,
      Converter'
  - name: Create a feature set that includes only the elements you need
    text: '```python # Instantiate the feature collection. selected_features = MarkdownSaveOptions.Features()'
  - name: Attach the feature set to the Markdown save options
    text: '```python md_options = MarkdownSaveOptions() md_options.features = selected_features
      ```'
  - name: Perform the conversion and save the result as a Markdown file
    text: '```python output_path = "YOUR_DIRECTORY/links_and_paragraphs.md" Converter.convert_html(html_doc,
      md_options, output_path) print(f"Conversion complete. Markdown saved to {output_path}")
      ```'
  type: HowTo
tags:
- HTML conversion
- Markdown
- Python
title: Convert HTML to Markdown Python – extract links & paragraphs
url: /python/general/convert-html-to-markdown-python-extract-links-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to Markdown Python – extract links & paragraphs

If you need to **convert HTML to Markdown**, this tutorial shows you a practical way to do it in Python while selectively **extracting links from HTML** and **extracting paragraphs from HTML**. You’ll see a complete, runnable example that saves the filtered content as a clean Markdown file.

Converting HTML to Markdown is a common step when you want lightweight, version‑controlled documentation, static‑site content, or simply a plain‑text representation of a web page. By the end of this guide you will have a script that:

1. Loads an HTML document from disk.  
2. Configures a feature set that keeps only links and paragraph elements.  
3. Performs the conversion using the GroupDocs Conversion SDK for Python.  
4. Writes the result to a `.md` file.

## Prerequisites

Before you start, make sure you have:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | The SDK targets modern Python versions. |
| `groupdocs-conversion` package | Provides `HTMLDocument`, `MarkdownSaveOptions`, and `Converter` classes used in the example. |
| An HTML file to test (e.g., `sample.html`) | The source you will convert. |

Install the SDK with pip:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** Use a virtual environment (`python -m venv .venv`) to keep dependencies isolated.

## Convert HTML to Markdown with Python

The core of the conversion lives in a few straightforward steps. Each step is explained below, and the full script appears at the end of the article.

### Step 1: Load the HTML document you want to convert

```python
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, Converter

# Replace YOUR_DIRECTORY with the path that contains your HTML file.
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*Why this step?*  
`HTMLDocument` parses the source file and builds an internal DOM representation that the converter can work with. Without loading the document first, the SDK has nothing to process.

### Step 2: Create a feature set that includes only the elements you need

```python
# Instantiate the feature collection.
selected_features = MarkdownSaveOptions.Features()

# Keep only hyperlinks.
selected_features.add(MarkdownSaveOptions.Features.LINK)

# Keep only paragraph tags.
selected_features.add(MarkdownSaveOptions.Features.PARAGRAPH)
```

*Why we add these features*  
`MarkdownSaveOptions.Features` acts as a filter. By adding `LINK` and `PARAGRAPH` we tell the converter to **extract links from HTML** and **extract paragraphs from HTML**, ignoring images, tables, scripts, and other markup that you may not need in the final Markdown.

### Step 3: Attach the feature set to the Markdown save options

```python
md_options = MarkdownSaveOptions()
md_options.features = selected_features
```

*Why this step?*  
`MarkdownSaveOptions` holds all conversion preferences. Assigning the previously built `selected_features` ensures the conversion respects our filter configuration.

### Step 4: Perform the conversion and save the result as a Markdown file

```python
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert_html(html_doc, md_options, output_path)
print(f"Conversion complete. Markdown saved to {output_path}")
```

*Why we call `convert_html`*  
`Converter.convert_html` is the SDK’s entry point for HTML‑to‑Markdown transformations. It reads the `HTMLDocument`, applies `md_options`, and writes the filtered output to `output_path`.

#### Expected output

The resulting `links_and_paragraphs.md` will contain only Markdown representations of hyperlinks and paragraph text, for example:

```markdown
[Visit the homepage](https://example.com)

This is the first paragraph of the article, describing the main topic.

Another paragraph with more details.
```

All other HTML elements such as `<img>`, `<table>`, or `<script>` are omitted, keeping the file lightweight and easy to edit.

## Extract links from HTML (optional deeper dive)

If your goal is **only to extract links from HTML** while discarding everything else, you can simplify the feature set:

```python
link_only_features = MarkdownSaveOptions.Features()
link_only_features.add(MarkdownSaveOptions.Features.LINK)

md_options.features = link_only_features
```

Running the conversion with this configuration produces a Markdown file where each link appears on its own line, e.g.:

```markdown


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}