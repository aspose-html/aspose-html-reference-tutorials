---
category: general
date: 2026-09-26
description: Convert HTML to Markdown with Python, extracting links from HTML and
  saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: en
lastmod: 2026-09-26
og_description: Convert HTML to Markdown with Python, extracting links from HTML and
  saving HTML as Markdown. Follow this complete guide.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: Convert HTML to Markdown in Python – extract links and paragraphs
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: Convert HTML to Markdown in Python – extract links and paragraphs easily
url: /python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert HTML to Markdown in Python – extract links and paragraphs easily

If you need to **convert HTML to Markdown** while keeping only the useful parts, this guide shows you how to do it with just a few lines of Python. Whether you are scraping blog posts, archiving documentation, or cleaning up email bodies, you’ll learn a reliable way to extract links from HTML and save HTML as Markdown.

The tutorial covers everything from installing the required package to handling edge cases such as empty `<a>` tags or nested paragraphs. By the end you’ll have a ready‑to‑run script that **converts HTML to Markdown**, extracts links from HTML, and even extracts paragraphs from HTML when you need them.

---

## Prerequisites

Before you start, make sure you have:

* Python 3.8 or newer installed  
* Access to the `groupdocs-conversion` Python package (the library that provides `HTMLDocument`, `MarkdownSaveOptions`, and `Converter`)  
* A local HTML file you want to process (e.g., `article.html`)

You can install the library with pip:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** Use a virtual environment (`python -m venv venv`) to keep dependencies isolated.

---

## Step 1: Load the source HTML document

The first operation is to create an `HTMLDocument` object that points to your source file. This object abstracts the raw HTML and gives the converter a clean entry point.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Why this matters:* Loading the document this way lets the library parse the DOM once, so subsequent operations (like extracting links or paragraphs) are fast and memory‑efficient.

---

## Step 2: Create Markdown save options and select the features you need

`MarkdownSaveOptions` lets you decide which HTML elements survive the conversion. The `features` flag uses a bitwise OR to combine options.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Why this matters:* By specifying `LINKS` and `PARAGRAPHS` you **extract links from HTML** and **extract paragraphs from HTML** while discarding everything else (styles, scripts, images). If you later need only links, replace `MarkdownFeatures.PARAGRAPHS` with `0` (or omit it).

---

## Step 3: Convert the HTML to Markdown using the configured options

Now call the static `convert_html` method, passing the source document, the destination path, and the options you just built.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Why this matters:* The conversion runs in a single pass, applying the feature filter you defined. The resulting file (`article_links.md`) contains only Markdown‑formatted links and paragraphs, which is exactly what you need when you want to **save HTML as Markdown** for downstream processing.

---

## Full script – everything together

Below is a complete, runnable script that you can copy‑paste into a file named `html_to_md.py`. Adjust the paths to match your environment.

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### Expected output

Running the script generates a file similar to the following (the exact content depends on the source HTML):

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Only the link text and the paragraph text appear; all other HTML elements are stripped away.

---

## Extract only links or only paragraphs (advanced variations)

Sometimes you need **how to convert HTML** into a Markdown file that contains just one type of element.

### 1. Extract only links

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Extract only paragraphs

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Both variations reuse the same `convert_html` call, so you don’t have to write separate conversion logic.

---

## Handling edge cases

| Situation                               | Recommended fix |
|----------------------------------------|-----------------|
| HTML file contains empty `<a>` tags    | The converter automatically skips empty links. If you see stray `[]()` entries, set `md_options.removeEmptyLinks = True`. |
| Nested paragraphs (`<p>` inside `<div>`) | The library flattens nested paragraphs, preserving the text order. No extra code needed. |
| Non‑ASCII characters in link titles    | Ensure your Python file is saved with UTF‑8 encoding and open the output file with `encoding="utf-8"` if you read it later. |
| Very large HTML files (≥ 50 MB)        | Process the file in chunks using `HTMLDocument(stream=io.BytesIO(...))` to avoid loading the entire file into memory. |

---

## Frequently asked questions

**Q: Does this work with HTML fragments (no `<html>` root tag)?**  
A: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats the fragment as the document body.

**Q: Can I keep images as Markdown image syntax?**  
A: Add `MarkdownFeatures.IMAGES` to the `features` flag:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**Q: How do I convert many files in a directory?**  
A: Wrap `convert_html_to_markdown` in a loop that walks the directory with `os.listdir` or `pathlib.Path.rglob("*.html")`.

---

## Conclusion

You now know how to **convert HTML to Markdown** in Python while selectively **extracting links from HTML** and **extracting paragraphs from HTML**. The script demonstrates the standard approach—load the document, configure `MarkdownSaveOptions`, and run `Converter.convert_html`. With a few tweaks you can also **save HTML as Markdown** containing only links, only paragraphs, or a full faithful representation.

Next, you might explore:

* Adding `MarkdownFeatures.HEADINGS` to preserve section titles.  
* Using the resulting Markdown as input for static site generators like MkDocs or Hugo.  
* Automating bulk conversions for an entire documentation repository.

Happy converting!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [How to Set Offset When Converting HTML to Markdown in Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}