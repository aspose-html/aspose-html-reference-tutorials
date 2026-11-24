---
category: general
date: 2026-11-24
description: Convert HTML to Markdown in Python using GitLab‑flavored options and
  extract links easily.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- save html as markdown
- html to markdown conversion
- extract links to markdown
language: en
lastmod: 2026-11-24
og_description: Convert HTML to Markdown in Python using GitLab‑flavored options,
  save html as markdown, and extract links to markdown with a complete example.
og_image_alt: Screenshot of a Python script converting HTML to GitLab‑flavored Markdown
og_title: Convert HTML to Markdown with GitLab‑flavored output – Python guide
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Convert HTML to Markdown in Python using GitLab‑flavored options and
    extract links easily.
  headline: How to convert HTML to Markdown with GitLab‑flavored output in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Conversion
- GitLab
title: How to convert HTML to Markdown with GitLab‑flavored output in Python
url: /python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to convert HTML to Markdown with GitLab‑flavored output in Python

If you need to **convert HTML to Markdown**, this guide shows a complete, ready‑to‑run solution. You’ll see how to save html as markdown using GitLab‑flavored formatting and how to extract links to markdown without leaving the code.

The approach works with the Aspose.HTML for Python library, which provides a single‑line conversion API and fine‑grained control over the Markdown flavor. By the end of the tutorial you’ll have a script that produces clean GitLab‑flavored markdown files and a list of extracted links.

## Prerequisites

Before you start, ensure you have:

* Python 3.8 or later installed.
* Access to `pip` for package installation.
* A local HTML file (e.g., `article.html`) you want to convert.
* Basic familiarity with running Python scripts from the command line.

No additional tools are required; the library handles parsing, conversion, and link extraction internally.

## Install the Aspose.HTML for Python library

The conversion API lives in the `aspose.html` package. Install it with `pip`:

```bash
pip install aspose-html
```

The package bundles the `HTMLDocument`, `MarkdownSaveOptions`, and `Converter` classes used later in the script. Installation completes in seconds and does not require a separate runtime.

## Load the HTML document

Creating an `HTMLDocument` object loads the source file into memory. The constructor accepts a file path or a URL.

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert.
doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

The `doc` instance now represents the full DOM tree, enabling the converter to read every element, including links and paragraph tags.

## Configure GitLab‑flavored Markdown options

GitLab‑flavored markdown differs from standard CommonMark in how it treats links and paragraphs. The `MarkdownSaveOptions` class lets you specify the formatter and the feature set you need.

```python
from aspose.html import MarkdownSaveOptions

# Configure options for GitLab‑flavored output.
#   formatter="GIT"  -> GitLab markdown
#   features=["Link", "Paragraph"] -> keep only links and paragraphs.
opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])
```

Setting `features` to `["Link", "Paragraph"]` ensures the conversion focuses on link extraction while preserving paragraph structure, which is ideal for documentation or changelog generation.

## Run the conversion and save as Markdown

With the document loaded and options configured, invoke the static `Converter.convert` method. It writes the result directly to the target file.

```python
from aspose.html import Converter

# Perform the conversion and write the markdown file.
Converter.convert(doc, "YOUR_DIRECTORY/article.md", opts)
```

After execution, `article.md` contains GitLab‑flavored markdown that mirrors the original HTML’s links and paragraphs.

## Verify the output and extract links to markdown

Open the generated file to confirm the conversion. You should see link syntax (`[text](url)`) and paragraph breaks that match the source.

```python
# Quick verification: read and print the first 10 lines.
with open("YOUR_DIRECTORY/article.md", "r", encoding="utf-8") as f:
    for i, line in enumerate(f):
        if i >= 10:
            break
        print(line.rstrip())
```

If you need the raw list of URLs for further processing, you can extract them from the `HTMLDocument` before conversion:

```python
# Extract all anchor href attributes.
links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
print("Extracted links:", links)
```

This step demonstrates **extract links to markdown** using the same DOM you already have, avoiding a second parse.

## Complete script

Putting everything together yields a single, self‑contained script you can drop into any project:

```python
# convert_html_to_gitlab_md.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def convert_html_to_markdown(src_path: str, dst_path: str) -> list:
    """
    Convert an HTML file to GitLab‑flavored Markdown and return a list of extracted links.

    Args:
        src_path: Path to the source HTML file.
        dst_path: Path where the Markdown file will be saved.

    Returns:
        A list of URLs found in the HTML document.
    """
    # Load the HTML document.
    doc = HTMLDocument(src_path)

    # Configure GitLab‑flavored Markdown options (links and paragraphs only).
    opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])

    # Convert and save as Markdown.
    Converter.convert(doc, dst_path, opts)

    # Extract links for additional processing.
    links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
    return links

if __name__ == "__main__":
    source = "YOUR_DIRECTORY/article.html"
    target = "YOUR_DIRECTORY/article.md"
    extracted_links = convert_html_to_markdown(source, target)

    print(f"Conversion complete. Markdown saved to {target}")
    print("Extracted links:", extracted_links)
```

Running the script:

```bash
python convert_html_to_gitlab_md.py
```

produces `article.md` with GitLab‑flavored markdown and prints the list of extracted URLs.

## Common variations and edge cases

| Scenario                              | Adjustment                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| **Full HTML (images, tables, etc.)** | Add `"Image"` or `"Table"` to `features` to keep those elements.           |
| **Different Markdown flavor**        | Change `formatter="GIT"` to `"COMMONMARK"` or `"GFM"` for other platforms. |
| **Large files (> 50 MB)**             | Use streaming APIs (`HTMLDocument.open`) to avoid loading the whole file. |
| **Unicode characters**                | Ensure the source file is UTF‑8 encoded; the library preserves encoding.   |

These variations let you reuse the same pattern for **save html as markdown** in many contexts.

## Pro tips

* **Reuse options:** Create a single `MarkdownSaveOptions` instance and pass it around if you convert multiple files in a batch job.
* **Validate links:** After extracting, run a simple `requests.head(url)` check to flag broken URLs.
* **Version lock:** Pin the Aspose.HTML version (`aspose-html==23.10`) to avoid unexpected API changes.

## Conclusion

You now know how to **convert HTML to markdown** using a GitLab‑flavored formatter, save html as markdown, and **extract links to markdown** with a concise Python script. The solution works out‑of‑the‑box, handles typical edge cases, and can be extended for other Markdown flavors or additional HTML features.

### Next steps

* Explore the `features` list to include images, tables, or code blocks.
* Integrate this script into a CI pipeline to automatically generate documentation from HTML sources.
* Combine the extracted links with a link‑checking service to maintain healthy references.

Feel free to adapt the script for your own workflows, and share your results with the community!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Convert HTML to Markdown Python – extract links & paragraphs](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [How to convert HTML to Markdown with GitLab‑flavored markdown in Python](/html/english/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-markdow/)
- [convert html to markdown python – save markdown file with python](/html/english/python/general/convert-html-to-markdown-python-save-markdown-file-with-pyth/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}