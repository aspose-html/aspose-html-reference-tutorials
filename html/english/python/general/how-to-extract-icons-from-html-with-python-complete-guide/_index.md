---
category: general
date: 2026-07-02
description: How to extract icons from an HTML file using Python. Learn to read HTML
  file python, parse HTML document, and extract href attribute to get favicon URLs.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: en
og_description: How to extract icons from an HTML page using Python. This tutorial
  shows you how to read HTML file python, parse the document, and pull out favicon
  URLs.
og_title: How to Extract Icons from HTML – Python Guide
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: How to Extract Icons from HTML with Python – Complete Guide
url: /python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Extract Icons from HTML with Python – Complete Guide

Ever wondered **how to extract icons** from a web page without opening a browser? Maybe you’re building a site‑catalog, a SEO audit tool, or just curious about the tiny favicons that appear in tabs. The good news is you can do it in a few lines of Python—no Selenium, no headless Chrome, just a plain‑text HTML file.

In this tutorial we’ll walk through reading an HTML file python, parsing the HTML document, and finally **extracting the href attribute** from `<link rel="icon">` tags to get those favicon URLs. By the end you’ll have a reusable snippet that works on any static HTML you throw at it, and you’ll also see how to handle edge cases like relative paths or multiple icon declarations.

## What You’ll Learn

- Load a local HTML file with Python (read html file python)  
- Use a lightweight parser to **parse html document** safely  
- Locate `<link>` elements that declare an icon  
- **Extract href attribute** values and turn them into absolute URLs  
- Collect and print all discovered **favicon URLs**  

No external services required—just the standard library and the popular **BeautifulSoup** package.

---

![Screenshot showing Python script extracting icons – how to extract icons](https://example.com/images/extract-icons-python.png "how to extract icons")

*Image alt text: "how to extract icons using a Python script"*

## Prerequisites

- Python 3.8+ installed  
- `beautifulsoup4` library (`pip install beautifulsoup4`)  
- A local HTML file you want to scan (e.g., `sample.html`)  

If you already have those, let’s jump in.

## Step 1: Read HTML File Python – Load the Document

First things first: we need to open the file and feed its contents to a parser. Using `with open(..., "r", encoding="utf‑8")` guarantees the file is closed automatically, and the UTF‑8 encoding handles most modern pages.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Why this matters:** Opening the file with the correct encoding prevents mysterious `�` characters that could break the parser later. Using `Path` from the standard library also makes the code cross‑platform.

## Step 2: Parse HTML Document – Find All Icon Links

Now we hand the raw HTML to **BeautifulSoup**, which builds a navigable tree. We’ll look for every `<link>` tag whose `rel` attribute contains the word `icon`. Note that `rel` may be a space‑separated list (`rel="shortcut icon"`), so we need a flexible check.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Why this step is crucial:** A naïve `soup.find_all("link", rel="icon")` would miss variations like `rel="shortcut icon"` or `rel="apple-touch-icon"`. Our helper `is_icon_link` covers those cases, making the extraction robust.

## Step 3: Extract href Attribute – Pull the URLs

With the relevant tags collected, we now pull the `href` attribute from each. Some pages might omit `href` (rare, but possible), so we guard against `None`. Additionally, favicons are often specified with relative URLs, so we’ll resolve them against the page’s base URL if you know it. For a local file we’ll just keep the path as‑is.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Why we strip whitespace:** HTML authors sometimes accidentally add spaces around URLs, which would break a subsequent request. Trimming ensures we get clean strings.

## Step 4: Extract Favicon URLs – Output the Results

Finally, we print (or return) the list of discovered URLs. In a real‑world script you might write them to a CSV, download the icons, or feed them into another service. Here’s a simple loop that shows the result on the console.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Handling Edge Cases

- **Multiple rel values:** Our `is_icon_link` check already catches `rel="shortcut icon"` and `rel="apple-touch-icon"`.  
- **Relative paths:** If you later need absolute URLs, use `urllib.parse.urljoin(base_url, href)`.  
- **Missing href:** The guard `if href:` skips malformed tags, avoiding `NoneType` errors.  
- **Duplicate entries:** You can `icon_urls = list(dict.fromkeys(icon_urls))` to deduplicate.

---

## Full Script – One‑Stop Solution

Putting it all together, here’s the complete, ready‑to‑run program. Save it as `extract_icons.py` and point `html_path` at any file you like.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Expected output** (assuming `sample.html` contains two icons):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Run it with `python extract_icons.py` and you’ll see the URLs printed to the console.

---

## Frequently Asked Questions

**Q: What if the HTML uses `<meta>` tags for icons?**  
A: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link` to also check for `meta` with `itemprop="image"` and pull its `content` attribute.

**Q: Can I fetch the icons automatically?**  
A: Yes—just feed each URL into `requests.get(url, stream=True)` and write the content to a file. Remember to handle relative URLs with `urljoin`.

**Q: Does this work on remote pages?**  
A: Absolutely. Replace the file‑reading step with `requests.get(page_url).text` and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and rate limits.

---

## Wrap‑Up

We’ve covered **how to extract icons** from any static HTML using Python, from reading the file to printing out each favicon URL. The core ideas—reading the file, parsing the document, locating the right tags, and pulling the `href` attribute—are reusable patterns you’ll encounter in many web‑scraping tasks.

Next steps? Try expanding the script to:

- Resolve relative URLs against the page’s base URL  
- Download each icon and save it locally  
- Support additional icon formats (`rel="mask-icon"` for Safari)  

Feel free to experiment, and if you run into quirks, drop a comment below. Happy parsing!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}