---
category: general
date: 2026-05-31
description: Learn how to download icons using Python. We'll also cover how to extract
  favicon, read HTML document Python, and write binary file python in a single tutorial.
draft: false
keywords:
- how to download icons
- how to extract favicon
- write binary file python
- read html document python
- load html python
language: en
og_description: How to download icons using Python explained step‑by‑step. Learn to
  extract favicon, read HTML document Python, and write binary file python.
og_title: How to Download Icons with Python – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to download icons using Python. We'll also cover how to extract
    favicon, read HTML document Python, and write binary file python in a single tutorial.
  headline: How to Download Icons with Python – Complete Guide
  type: TechArticle
tags:
- python
- web-scraping
- favicon
- file-io
title: How to Download Icons with Python – Complete Guide
url: /python/general/how-to-download-icons-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Download Icons with Python – Complete Guide

Ever wondered **how to download icons** from a website without manually right‑clicking each one? You're not the only one. Whether you're building a brand‑audit tool or just want a local copy of every favicon you encounter, mastering this task saves you time and keystrokes.

In this tutorial we'll walk through **how to download icons** from an HTML file using plain‑vanilla Python. We'll also show you **how to extract favicon**, demonstrate **read html document python**, and explain **write binary file python** so you end up with a tidy folder of .ico files ready for any project.

---

## What You’ll Need

- Python 3.8+ (the standard library is enough)
- A local copy of the HTML page you want to scan (or a URL you can fetch)
- Basic familiarity with file I/O in Python  
- No external packages required, but `beautifulsoup4` can make things smoother if you prefer (optional)

Got those? Great—let's dive in.

![How to download icons example](https://example.com/placeholder.png "how to download icons example")

---

## Step 1: Load the HTML Document in Python  

First things first, we need to **load html python** style—read the file into memory so we can inspect its `<link>` tags. The simplest way is to open the file with the built‑in `open` function and read it as text.

```python
# Step 1: Load the HTML document
HTML_PATH = "YOUR_DIRECTORY/sample.html"

# Using the built‑in open() to read the file as a string
with open(HTML_PATH, "r", encoding="utf-8") as f:
    html_content = f.read()
```

*Why this step?*  
Reading the HTML gives us a raw string that we can parse. If you skip this and try to work with a path directly, the parser won't have anything to examine.

---

## Step 2: Parse the Document and Find Icon Links  

Now we need to **read html document python** style. While you could use regexes, a tiny HTML parser keeps things reliable. Python ships with `html.parser` which we can subclass for our purpose.

```python
from html.parser import HTMLParser

class IconLinkParser(HTMLParser):
    """Collects href attributes from <link rel='icon'> tags."""
    def __init__(self):
        super().__init__()
        self.icon_hrefs = []

    def handle_starttag(self, tag, attrs):
        if tag.lower() != "link":
            return
        attrs_dict = dict(attrs)
        # Look for rel="icon" (or rel="shortcut icon")
        rel = attrs_dict.get("rel", "").lower()
        if "icon" in rel:
            href = attrs_dict.get("href")
            if href:
                self.icon_hrefs.append(href)

# Instantiate and feed the HTML content
parser = IconLinkParser()
parser.feed(html_content)

# Now we have a list of all icon URLs
icon_hrefs = parser.icon_hrefs
print(f"Found {len(icon_hrefs)} icon link(s):", icon_hrefs)
```

**Explanation**  
- `handle_starttag` fires for every opening tag.  
- We filter for `<link>` elements whose `rel` attribute contains the word *icon*. This covers both `rel="icon"` and the older `rel="shortcut icon"`.  
- The `href` values are stored in `icon_hrefs`, ready for the next step.

---

## Step 3: Resolve Relative Paths (Optional but Helpful)

If the HTML uses relative URLs, we must turn them into absolute file system paths. This is where **load html python** knowledge meets `urllib.parse`.

```python
import os
from urllib.parse import urljoin

# Base directory where the HTML file lives
BASE_DIR = os.path.dirname(os.path.abspath(HTML_PATH))

def resolve_path(href):
    # If href already looks like an absolute path, return it unchanged
    if os.path.isabs(href):
        return href
    # Otherwise, join it with the base directory
    return os.path.normpath(os.path.join(BASE_DIR, href))

resolved_icon_paths = [resolve_path(h) for h in icon_hrefs]
print("Resolved paths:", resolved_icon_paths)
```

*Why bother?*  
When you later **write binary file python**, you need a real file path. Relative URLs like `images/favicon.ico` would otherwise cause a `FileNotFoundError`.

---

## Step 4: Write Each Icon to a Local Binary File  

Here’s the heart of **how to download icons**. We’ll loop over the resolved paths, read each icon as binary data, and write it out to a new file in a dedicated `icons/` folder.

```python
import shutil

OUTPUT_DIR = "YOUR_DIRECTORY/icons"
os.makedirs(OUTPUT_DIR, exist_ok=True)

for index, icon_path in enumerate(resolved_icon_paths):
    # Guard against missing files
    if not os.path.isfile(icon_path):
        print(f"⚠️  Icon file not found: {icon_path}")
        continue

    # Destination filename: icon_0.ico, icon_1.ico, …
    dest_path = os.path.join(OUTPUT_DIR, f"icon_{index}.ico")

    # **write binary file python** – copy the binary data
    with open(icon_path, "rb") as src_file, open(dest_path, "wb") as dst_file:
        shutil.copyfileobj(src_file, dst_file)

    print(f"✅ Saved {dest_path}")
```

**What’s happening?**  

- `os.makedirs(..., exist_ok=True)` ensures the output folder exists.  
- `shutil.copyfileobj` streams the bytes from source to destination, which is the most memory‑efficient way to **write binary file python**.  
- We name each file `icon_<index>.ico` to avoid collisions.

**Expected output**

```
Found 2 icon link(s): ['images/favicon.ico', 'icons/custom.ico']
Resolved paths: ['/path/to/YOUR_DIRECTORY/images/favicon.ico',
                '/path/to/YOUR_DIRECTORY/icons/custom.ico']
✅ Saved YOUR_DIRECTORY/icons/icon_0.ico
✅ Saved YOUR_DIRECTORY/icons/icon_1.ico
```

After the script finishes, you’ll have a clean collection of icon files ready for any downstream task.

---

## Step 5: Bonus – Download Icons Directly from a Remote URL  

If your HTML lives on the web instead of the local disk, replace the file‑reading part with a tiny `requests` call. This demonstrates **how to extract favicon** from any live page.

```python
import requests

REMOTE_URL = "https://example.com"

# Grab the HTML
response = requests.get(REMOTE_URL)
response.raise_for_status()
html_content = response.text

# Re‑run the parser (same as before) to get icon URLs
parser = IconLinkParser()
parser.feed(html_content)
icon_hrefs = parser.icon_hrefs

# Download each icon via HTTP
for index, href in enumerate(icon_hrefs):
    # Resolve relative URLs against the page URL
    icon_url = urljoin(REMOTE_URL, href)
    r = requests.get(icon_url, stream=True)
    r.raise_for_status()
    dest_path = os.path.join(OUTPUT_DIR, f"remote_icon_{index}.ico")
    with open(dest_path, "wb") as out_file:
        shutil.copyfileobj(r.raw, out_file)
    print(f"✅ Downloaded {icon_url} → {dest_path}")
```

**Why add this?**  
Many real‑world projects need to scrape favicons from live sites. This snippet shows you can extend the same **how to download icons** logic to the internet with just a couple of extra lines.

---

## Common Pitfalls & Pro Tips

- **Missing `rel="icon"`** – Some sites embed icons via `<meta>` tags or CSS. If you need those, expand the parser to look for `<meta name="msapplication‑TileImage">` or CSS `background-image` URLs.  
- **Non‑ICO formats** – Modern favicons often use `.png` or `.svg`. The code above works for any binary image; just adjust the file extension in `dest_path` if you care about preserving the original format.  
- **Permission errors** – When writing files, ensure your script runs with write permission to the target folder. Using `os.makedirs(..., exist_ok=True)` avoids “directory not found” crashes.  
- **Large HTML files** – For massive pages, consider streaming the file line‑by‑line instead of loading the entire string into memory. The built‑in `HTMLParser` can handle incremental feeds.  

---

## Conclusion

You've just learned **how to download icons** from an HTML document using pure Python. By **reading html document python**, parsing for `<link rel="icon">` tags, resolving any relative paths, and finally **write binary file python** to store each icon locally, you now have a reusable script that works for both local and remote pages.  

Next steps? Try extending the parser to capture Apple touch icons (`rel="apple-touch-icon"`), or integrate the script into a larger web‑crawling pipeline that gathers favicons for hundreds of domains. The fundamentals covered here—HTML parsing, path resolution, and binary file handling—are building blocks for many web‑automation tasks.

Got questions or want to share a cool use case? Drop a comment below, and happy icon hunting!


## What Should You Learn Next?

- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Convert HTML to JPEG Using Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}