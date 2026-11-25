---
category: general
date: 2026-09-07
description: Convert HTML to markdown quickly using Python and GitLab‑flavoured markdown.
  Learn to extract links from HTML and save a markdown file in one script.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- gitlab flavored markdown
- how to convert html
- html to markdown file
language: en
lastmod: 2026-09-07
og_description: Convert HTML to markdown with GitLab‑flavoured formatting. This tutorial
  shows how to extract links from HTML and produce a markdown file using Python.
og_image_alt: Screenshot of Python code that converts HTML to markdown
og_title: Convert HTML to markdown with GitLab flavor – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: Convert HTML to markdown quickly using Python and GitLab‑flavoured
    markdown. Learn to extract links from HTML and save a markdown file in one script.
  headline: How to convert HTML to markdown with GitLab flavor
  type: TechArticle
- description: Convert HTML to markdown quickly using Python and GitLab‑flavoured
    markdown. Learn to extract links from HTML and save a markdown file in one script.
  name: How to convert HTML to markdown with GitLab flavor
  steps:
  - name: Load the HTML source document
    text: '```python from aspose.html import HTMLDocument'
  - name: Configure GitLab‑flavoured markdown options
    text: '```python from aspose.html import MarkdownSaveOptions'
  - name: Perform the conversion and save the markdown file
    text: '```python from aspose.html import Converter'
  - name: Full script for quick copy‑paste
    text: '```python # convert_html_to_markdown.py """ How to convert HTML to markdown
      (GitLab flavor) and extract links from HTML. """'
  - name: Conclusion
    text: You now know how to **convert HTML to markdown**, extract links from HTML,
      and generate a **GitLab‑flavoured markdown** file using a concise Python script.
      The approach is reliable, works with any valid HTML source, and gives you fine‑grained
      control over which elements are exported. Feel free to ad
  type: HowTo
tags:
- HTML conversion
- Markdown
- Python
- Aspose.HTML
title: How to convert HTML to markdown with GitLab flavor
url: /python/general/how-to-convert-html-to-markdown-with-gitlab-flavor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to convert HTML to markdown with GitLab flavor

If you need to **convert HTML to markdown**, this guide walks you through a complete Python solution using the Aspose.HTML library. We'll also show **how to extract links from HTML** and generate a **GitLab‑flavoured markdown** file in a single pass.

You’ll learn:

* The exact code required to read an HTML document, configure conversion options, and write a markdown file.  
* Why the GitLab markdown formatter matters when you store documentation in GitLab repositories.  
* Common pitfalls—such as handling relative URLs or missing `<p>` tags—and how to avoid them.

By the end of this tutorial you can run a one‑liner script that produces an **html to markdown file** containing only the links and paragraphs you care about.

## Prerequisites

Before you start, make sure you have:

| Requirement | Reason |
|-------------|--------|
| Python ≥ 3.8 | Required for the Aspose.HTML Python package. |
| `aspose.html` package | Provides `HTMLDocument`, `MarkdownSaveOptions`, and `Converter`. Install with `pip install aspose-html`. |
| An HTML source file (e.g., `article.html`) | The file you want to convert. |
| Write permission to the output directory | The script will create `article.md`. |

> **Pro tip:** Use a virtual environment (`python -m venv venv`) to keep dependencies isolated.

## Install the Aspose.HTML Python package

```bash
pip install aspose-html
```

The package bundles the native binaries for Windows, macOS, and Linux, so no additional system libraries are needed.

## Convert HTML to markdown with Aspose.HTML

### Step 1: Load the HTML source document

```python
from aspose.html import HTMLDocument

# Replace YOUR_DIRECTORY with the path where article.html lives
html_path = "YOUR_DIRECTORY/article.html"
html_doc = HTMLDocument(html_path)

# Verify that the document loaded correctly
print(f"Loaded HTML title: {html_doc.title}")
```

*Why this step matters:* `HTMLDocument` parses the entire DOM, giving you access to every element—including the `<a>` tags we’ll later extract.

### Step 2: Configure GitLab‑flavoured markdown options

```python
from aspose.html import MarkdownSaveOptions

md_options = MarkdownSaveOptions()
# Choose the GitLab‑flavoured markdown formatter
md_options.formatter = MarkdownSaveOptions.Formatter.GIT

# Export only the features we need:
#   • LINKS – converts <a href=""> into markdown links
#   • PARAGRAPH – keeps <p> content as separate paragraphs
md_options.features = (
    MarkdownSaveOptions.Feature.LINK |
    MarkdownSaveOptions.Feature.PARAGRAPH
)

# Optional: preserve original line breaks (helps with diff tools)
md_options.use_original_line_breaks = True
```

*Why this step matters:* The **gitlab flavored markdown** formatter respects GitLab’s extended syntax (e.g., tables, task lists). By limiting `features` to `LINK` and `PARAGRAPH`, we **extract links from HTML** while discarding other elements like images or scripts.

### Step 3: Perform the conversion and save the markdown file

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/article.md"
Converter.convert(html_doc, output_path, md_options)

print(f"Markdown file created at: {output_path}")
```

When the script finishes, `article.md` contains only markdown‑formatted links and paragraphs, ready to be committed to a GitLab repository.

### Full script for quick copy‑paste

```python
# convert_html_to_markdown.py
"""
How to convert HTML to markdown (GitLab flavor) and extract links from HTML.
"""

from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def convert_html_to_md(html_path: str, md_path: str) -> None:
    """Convert an HTML file to a GitLab‑flavoured markdown file."""
    # Load the source HTML
    html_doc = HTMLDocument(html_path)

    # Set up conversion options
    md_options = MarkdownSaveOptions()
    md_options.formatter = MarkdownSaveOptions.Formatter.GIT
    md_options.features = (
        MarkdownSaveOptions.Feature.LINK |
        MarkdownSaveOptions.Feature.PARAGRAPH
    )
    md_options.use_original_line_breaks = True

    # Convert and save
    Converter.convert(html_doc, md_path, md_options)

if __name__ == "__main__":
    # Adjust these paths to your environment
    src_html = "YOUR_DIRECTORY/article.html"
    dst_md = "YOUR_DIRECTORY/article.md"

    convert_html_to_md(src_html, dst_md)
    print("Conversion complete.")
```

#### Expected output

Assuming `article.html` contains:

```html
<h1>Welcome</h1>
<p>This is a sample paragraph.</p>
<p>Visit <a href="https://example.com">our site</a> for more info.</p>
```

The generated `article.md` will be:

```markdown
Welcome

This is a sample paragraph.

Visit [our site](https://example.com) for more info.
```

Only the paragraph text and the link survive—exactly what the **extract links from HTML** option promises.

## Handling common edge cases

| Scenario | What to watch for | Suggested fix |
|----------|-------------------|---------------|
| Relative URLs (`href="/path/page.html"`) | GitLab markdown renders them relative to the repository root, which may break external links. | Prepend the base URL before conversion: `md_options.base_uri = "https://mydomain.com"` |
| Empty `<a>` tags (`<a href=""></a>`) | Results in `[]()` which looks odd in markdown. | Filter out empty links after conversion using a simple regex: `re.sub(r'\[.*?\]\(\s*\)', '', markdown_text)` |
| Non‑ASCII characters in URLs | Some markdown parsers escape them incorrectly. | Encode URLs with `urllib.parse.quote` before feeding them to the converter. |
| Large HTML files (>10 MB) | Memory consumption spikes because `HTMLDocument` loads the whole DOM. | Use streaming APIs (`HTMLDocument.load_from_stream`) if available, or split the source into sections. |

## Verify the conversion

You can quickly verify that the markdown file contains only the desired features:

```python
import pathlib

md_file = pathlib.Path(dst_md)
assert md_file.read_text().strip() != "", "Markdown file is empty!"
print("Markdown preview:")
print(md_file.read_text().splitlines()[:10])  # Show first 10 lines
```

If the assertion fails, double‑check that `md_options.features` includes `LINK` and `PARAGRAPH`.

## Next steps and related topics

* **Export additional features** – add `MarkdownSaveOptions.Feature.IMAGE` to include `<img>` tags.  
* **Convert to other markdown flavors** – switch `md_options.formatter` to `MarkdownSaveOptions.Formatter.COMMONMARK` for generic markdown.  
* **Batch processing** – loop over a directory of HTML files to produce a set of markdown documents.  
* **Integrate with CI/CD** – run the script in a GitLab pipeline to automatically keep documentation in sync.

---

### Conclusion

You now know how to **convert HTML to markdown**, extract links from HTML, and generate a **GitLab‑flavoured markdown** file using a concise Python script. The approach is reliable, works with any valid HTML source, and gives you fine‑grained control over which elements are exported. Feel free to adapt the script for batch conversions, custom formatting, or integration into your documentation workflow.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert markdown to html – Java guide with PDF output](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}