---
category: general
date: 2026-11-27
description: Convert html to markdown using Python and generate markdown from html
  with GitLab‑flavored markdown support. Learn how to set markdown formatter and export
  html as markdown.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- export html as markdown
- generate markdown from html
- set markdown formatter
language: en
lastmod: 2026-11-27
og_description: Convert html to markdown with Python and GitLab‑flavored markdown.
  This guide shows how to set markdown formatter and export html as markdown in a
  few steps.
og_image_alt: Diagram illustrating how to convert html to markdown using a Python
  script
og_title: Convert html to markdown with GitLab‑flavored Markdown in Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Convert html to markdown using Python and generate markdown from html
    with GitLab‑flavored markdown support. Learn how to set markdown formatter and
    export html as markdown.
  headline: Convert html to markdown with GitLab‑flavored Markdown using Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
title: Convert html to markdown with GitLab‑flavored Markdown using Python
url: /python/general/convert-html-to-markdown-with-gitlab-flavored-markdown-using/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert html to markdown with GitLab‑flavored Markdown using Python

If you need to **convert html to markdown**, this guide shows a complete, ready‑to‑run solution. You’ll see how to **export html as markdown**, choose the **GitLab‑flavored markdown** format, and **set markdown formatter** options so the output matches your repository’s rendering rules.

In the following sections we’ll walk through every line of code, explain why each setting matters, and cover common variations such as keeping only links and paragraphs or switching to the default flavor. By the end you’ll be able to **generate markdown from html** in a single function call.

## Prerequisites

Before you start, make sure you have:

* Python 3.8+ installed  
* The `aspose.words` (or a similar library that provides `HTMLDocument`, `MarkdownSaveOptions`, and `Converter`) installed via `pip install aspose-words`  
* A small HTML file you want to convert, e.g., `sample.html` in a known directory  

No additional tools are required; the tutorial uses only the library’s built‑in conversion engine.

## Step 1: Load the HTML document you want to convert

The conversion pipeline begins by loading the source file into an `HTMLDocument` object. This object parses the HTML markup and prepares it for transformation.

```python
from aspose.words import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

# Load the HTML file you wish to convert
html_doc = HTMLDocument("YOUR_DIRECTORY/sample.html")
```

*Why this step matters*: `HTMLDocument` normalizes the HTML structure, resolves relative URLs, and creates a DOM that the markdown engine can traverse. Skipping this step would force the converter to read raw text, resulting in missing tags or broken links.

## Step 2: Create Markdown save options and configure the desired flavor and features

Here we **set markdown formatter** options. The `format` property selects the markdown flavor—`"GIT"` produces **GitLab‑flavored markdown**, while `"DEFAULT"` yields standard CommonMark.

```python
# Create a MarkdownSaveOptions instance
md_options = MarkdownSaveOptions()

# Set the formatter to GitLab‑flavored markdown
md_options.formatter = "GIT"  # alternatives: "DEFAULT", "MARKDOWN"

# Choose which markdown features to keep.
# In this example we keep only links and paragraphs.
md_options.features = (
    MarkdownFeatures.LINK |
    MarkdownFeatures.PARAGRAPH
)
```

*Why this matters*: Different platforms (GitHub, GitLab, Bitbucket) interpret markdown slightly differently. By **setting markdown formatter** to `"GIT"` you ensure that tables, task lists, and other GitLab‑specific syntax render correctly. The `features` flag lets you **export html as markdown** while stripping unwanted elements, which keeps the output clean for documentation or read‑me files.

## Step 3: Convert the HTML document to Markdown using the configured options

With the source loaded and the options prepared, invoke the static `convert` method. This single call performs the heavy lifting.

```python
# Perform the conversion and write the result to a .md file
Converter.convert(html_doc, md_options, "YOUR_DIRECTORY/sample.md")
```

*Why this matters*: The `Converter` class abstracts the entire transformation pipeline. It reads the DOM from `HTMLDocument`, applies the formatter you **set markdown formatter**, respects the selected `features`, and writes the final markdown file. The result is a clean, GitLab‑compatible `.md` file ready for version control.

## Expected output

Assuming `sample.html` contains a simple paragraph with a link:

```html
<p>Check out the <a href="https://example.com">example site</a> for more info.</p>
```

The generated `sample.md` will look like:

```markdown
Check out the [example site](https://example.com) for more info.
```

Because we limited the features to `LINK` and `PARAGRAPH`, any images, tables, or scripts from the original HTML are omitted. If you need a richer conversion, adjust `md_options.features` accordingly (e.g., add `MarkdownFeatures.IMAGE`).

## Step 4: Verify the conversion and handle edge cases

It’s good practice to read the output file back into Python and verify that the conversion succeeded, especially when processing many files in a batch.

```python
# Verify the markdown file exists and print its first lines
import pathlib

output_path = pathlib.Path("YOUR_DIRECTORY/sample.md")
if output_path.is_file():
    print("Conversion succeeded. First 3 lines:")
    print("\n".join(output_path.read_text().splitlines()[:3]))
else:
    raise FileNotFoundError("The markdown file was not created.")
```

**Common edge cases**

| Situation | How to address it |
|-----------|-------------------|
| **Relative image URLs** – they become broken in markdown | Use `md_options.features |= MarkdownFeatures.IMAGE` and then post‑process the markdown to rewrite image paths. |
| **Complex tables** – GitLab has limited table support | Keep the default formatter (`"DEFAULT"`) or manually adjust the table syntax after conversion. |
| **Unicode characters** – may appear as escaped sequences | Ensure your Python script opens files with `encoding="utf-8"` and set `md_options.encoding = "UTF-8"` if the library exposes it. |

## Pro tip: Batch conversion for an entire folder

If you need to **generate markdown from html** for dozens of files, wrap the three steps in a loop:

```python
import os

source_dir = "YOUR_DIRECTORY"
target_dir = "YOUR_DIRECTORY/markdown"

os.makedirs(target_dir, exist_ok=True)

for filename in os.listdir(source_dir):
    if filename.lower().endswith(".html"):
        html_path = os.path.join(source_dir, filename)
        md_path = os.path.join(target_dir, os.path.splitext(filename)[0] + ".md")

        html_doc = HTMLDocument(html_path)
        md_options = MarkdownSaveOptions()
        md_options.formatter = "GIT"
        md_options.features = MarkdownFeatures.LINK | MarkdownFeatures.PARAGRAPH

        Converter.convert(html_doc, md_options, md_path)
        print(f"Converted {filename} → {os.path.basename(md_path)}")
```

This script **exports html as markdown** for every `.html` file, preserving the GitLab flavor throughout the batch.

## Conclusion

You now have a full, production‑ready method to **convert html to markdown**, choose the **GitLab‑flavored markdown** output, and **set markdown formatter** options that match your project's needs. By following the steps above you can reliably **export html as markdown**, **generate markdown from html**, and adapt the pipeline for bulk processing or custom feature sets.

Next, consider exploring:

* Adding `MarkdownFeatures.IMAGE` to keep inline images when you **export html as markdown** for richer documentation.
* Switching the formatter to `"DEFAULT"` if you need a more generic markdown file.
* Integrating this conversion into a CI/CD pipeline so that every HTML report automatically becomes a Markdown artifact.

Happy coding, and enjoy the seamless transition from HTML to clean, GitLab‑ready markdown!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to convert HTML to Markdown with a custom formatter in Python](/html/english/python/general/how-to-convert-html-to-markdown-with-a-custom-formatter-in-p/)
- [How to convert HTML to markdown with images using Python](/html/english/python/general/how-to-convert-html-to-markdown-with-images-using-python/)
- [How to convert HTML to Markdown with Python – complete guide](/html/english/python/general/how-to-convert-html-to-markdown-with-python-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}