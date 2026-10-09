---
category: general
date: 2026-10-09
description: convert html to markdown quickly with Python. Learn the full markdown
  conversion with git preset and other tips in this concise tutorial.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to convert html
- html to markdown python
- markdown conversion with git
language: en
lastmod: 2026-10-09
og_description: convert html to markdown using Python and the git‑flavoured preset.
  Follow this tutorial to get clean Markdown output in seconds.
og_image_alt: Screenshot of Python code converting an HTML file to a git‑flavoured
  Markdown file
og_title: Convert HTML to Markdown in Python – complete guide
schemas:
- author: GroupDocs
  dateModified: '2026-10-09'
  description: convert html to markdown quickly with Python. Learn the full markdown
    conversion with git preset and other tips in this concise tutorial.
  headline: How to convert HTML to Markdown in Python – step‑by‑step guide
  type: TechArticle
- description: convert html to markdown quickly with Python. Learn the full markdown
    conversion with git preset and other tips in this concise tutorial.
  name: How to convert HTML to Markdown in Python – step‑by‑step guide
  steps:
  - name: '**Source** – a string containing HTML.'
    text: '**Source** – a string containing HTML.'
  - name: '**Destination path** – where the markdown file will be written.'
    text: '**Destination path** – where the markdown file will be written.'
  - name: '**Options** – the `MarkdownSaveOptions` we configured earlier.'
    text: '**Options** – the `MarkdownSaveOptions` we configured earlier.'
  type: HowTo
tags:
- Python
- HTML
- Markdown
- Document conversion
title: How to convert HTML to Markdown in Python – step‑by‑step guide
url: /python/general/how-to-convert-html-to-markdown-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to convert HTML to markdown in Python – step‑by‑step guide

If you need to **convert HTML to markdown** quickly, this tutorial shows you a ready‑to‑run solution in Python. Whether you’re extracting blog content, migrating documentation, or building a static‑site generator, the example below demonstrates the most reliable way to perform the conversion while preserving Git‑flavoured markdown features.

You’ll also learn **how to convert HTML** with the `markdown conversion with git` preset, see common pitfalls, and get a complete, runnable script. No external web services are required—everything runs locally.

## What this guide covers

* Installing the required library (`groupdocs-conversion`).
* Setting up **MarkdownSaveOptions** for a Git‑flavoured output.
* Using **Converter.convert** to transform an HTML string or file.
* Handling images, tables, and code blocks during the conversion.
* Verifying the result and troubleshooting typical issues.

By the end of the guide you can confidently say you know **html to markdown python** conversion inside and out.

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | The library uses modern language features. |
| `pip` access | To install the conversion SDK. |
| Basic familiarity with Python functions | Needed to run the script and modify options. |

If you already have Python installed, you’re ready to move on.

## Step 1: Install the GroupDocs Conversion SDK

```bash
pip install groupdocs-conversion
```

The `groupdocs-conversion` package ships the `Converter` class and the `MarkdownSaveOptions` type you’ll use for **html to markdown python** conversion. The installation pulls all native dependencies, so no additional system packages are required.

> **Pro tip:** Use a virtual environment (`python -m venv .venv`) to keep the SDK isolated from other projects.

## Step 2: Import the required classes

```python
from groupdocs.conversion import Converter, MarkdownSaveOptions
```

`Converter` is the engine that reads the source document, while `MarkdownSaveOptions` lets you fine‑tune the output format. Importing them at the top of the file makes the script clear and reusable.

## Step 3: Prepare the Markdown save options

```python
# Step 1: Create Markdown save options
md_opts = MarkdownSaveOptions()

# Step 2: Enable the Git‑flavoured preset
md_opts.git = True
```

*Why enable the Git‑flavoured preset?*  
The Git preset (`md_opts.git = True`) produces markdown that matches the syntax used by GitHub, GitLab, and Bitbucket. It ensures fenced code blocks, tables, and task lists render correctly on those platforms.

If you don’t need Git‑specific features, you can omit the `git` line and receive plain CommonMark output.

## Step 4: Load your HTML source

You can provide HTML as a string, a file path, or a URL. Below we read a local `example.html` file:

```python
# Load HTML from a file (you can also use a string or request a remote page)
with open("example.html", "r", encoding="utf-8") as f:
    html_doc = f.read()
```

> **Common edge case:** If the HTML contains `<meta charset>` tags that differ from UTF‑8, open the file with the correct encoding to avoid garbled characters.

## Step 5: Perform the conversion

```python
# Step 3: Convert the HTML document to Markdown using the configured options
# The output file will be placed in the specified directory.
output_path = "output/git_style.md"
Converter.convert(html_doc, output_path, md_opts)
print(f"Conversion complete – Markdown saved to {output_path}")
```

`Converter.convert` accepts three arguments:

1. **Source** – a string containing HTML.
2. **Destination path** – where the markdown file will be written.
3. **Options** – the `MarkdownSaveOptions` we configured earlier.

Because we passed the Git preset, headings become `#`, tables use pipe syntax, and task lists appear as `- [ ]`.

### Verifying the result

Open `output/git_style.md` in any markdown viewer (e.g., VS Code, GitHub preview). You should see:

```markdown
# Sample Document

This is a paragraph extracted from the original HTML.

## Table Example

| Header 1 | Header 2 |
|----------|----------|
| Cell A   | Cell B   |

- [ ] Task item 1
- [x] Completed task
```

If the output looks empty or missing elements, double‑check that the HTML you passed is well‑formed. Malformed tags often cause the converter to skip sections.

## Handling images and external assets

By default, the SDK copies image URLs verbatim. To embed images as relative paths:

```python
md_opts.embed_images = True   # Embed images as base64 (optional)
md_opts.images_folder = "output/images"  # Directory for extracted images
```

Setting `embed_images` to `True` converts each `<img>` tag into a base64‑encoded data URI, making the markdown self‑contained. This is handy for documentation that must be portable.

## Converting multiple files in a batch

If you need to **convert html to markdown** for dozens of files, wrap the conversion in a loop:

```python
import pathlib

source_dir = pathlib.Path("html_sources")
output_dir = pathlib.Path("markdown_output")
output_dir.mkdir(exist_ok=True)

for html_path in source_dir.glob("*.html"):
    with html_path.open("r", encoding="utf-8") as f:
        html_content = f.read()
    md_file = output_dir / f"{html_path.stem}.md"
    Converter.convert(html_content, str(md_file), md_opts)
    print(f"Converted {html_path.name} → {md_file.name}")
```

This script respects the same **markdown conversion with git** settings for every file, guaranteeing consistent output across the whole project.

## Common pitfalls and how to avoid them

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| Missing tables | HTML tables are built with `<table>` tags that lack `<thead>` or `<tbody>` | Ensure the HTML includes proper table sections or pre‑process with BeautifulSoup to add them. |
| Code blocks appear as plain text | `<pre>` tags lack language class (e.g., `class="language-python"`) | Add a language identifier or set `md_opts.detect_code_language = True`. |
| Images appear broken in markdown preview | Relative paths are incorrect | Use `md_opts.images_folder` to control where images are saved, then adjust the markdown links accordingly. |
| Output file is empty | `html_doc` variable is `None` or empty | Verify that the file read operation succeeded and that the HTML source is not empty. |

## Full runnable example

Save the following script as `convert_html_to_md.py` and run `python convert_html_to_md.py`.

```python
# convert_html_to_md.py
"""
Complete example: convert an HTML file to Git‑flavoured Markdown using
GroupDocs Conversion SDK.
"""

from pathlib import Path
from groupdocs.conversion import Converter, MarkdownSaveOptions

def convert_html_to_markdown(html_path: Path, md_path: Path, git_preset: bool = True):
    # Load HTML content
    html_content = html_path.read_text(encoding="utf-8")

    # Configure Markdown options
    md_opts = MarkdownSaveOptions()
    md_opts.git = git_preset          # enable markdown conversion with git
    md_opts.embed_images = False      # change to True if you need embedded images
    md_opts.images_folder = str(md_path.parent / "images")

    # Perform conversion
    Converter.convert(html_content, str(md_path), md_opts)
    print(f"✅ {html_path.name} → {md_path.name}")

if __name__ == "__main__":
    # Paths – adjust to your environment
    source_html = Path("example.html")
    destination_md = Path("output/git_style.md")

    # Ensure output directory exists
    destination_md.parent.mkdir(parents=True, exist_ok=True)

    convert_html_to_markdown(source_html, destination_md)
```

**Expected output** (displayed in the console):

```
✅ example.html → git_style.md
Conversion complete – Markdown saved to output/git_style.md
```

Open `output/git_style.md` to verify that headings, tables, lists, and code blocks match the original HTML structure.

## Conclusion

You now have a solid, production‑ready method to **convert HTML to markdown** using Python. By configuring `MarkdownSaveOptions` with the `git` flag, the conversion respects Git‑flavoured markdown conventions, making the result ready for GitHub, GitLab, or any markdown‑aware CI pipeline.

Remember:

* Install `groupdocs-conversion` once and reuse it across projects.
* Use the Git preset (`md_opts.git = True`) for the most compatible markdown.
* Adjust image handling (`embed_images`, `images_folder`) to fit your deployment model.
* Batch‑process directories when you need to **html to markdown python** at scale.

Next, you might explore **how to convert html** into other formats such as PDF or DOCX, or integrate this script into a static‑site generator like MkDocs. Either way, the fundamentals covered here give you a reliable foundation for any markdown conversion task. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert markdown to html – Java guide with PDF output](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}