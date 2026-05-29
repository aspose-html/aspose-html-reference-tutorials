---
category: general
date: 2026-05-28
description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
  and extract href attributes with an XPath contains example.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: en
og_description: 'How to parse HTML in Python: learn to load an HTML file, use CSS
  selectors, and get href attributes with an XPath contains example.'
og_title: How to Parse HTML in Python – Step‑by‑Step
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: How to Parse HTML in Python – Complete Guide
url: /python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Parse HTML in Python – Complete Guide

Ever wondered **how to parse HTML** in a Python script without pulling in a heavyweight browser? You're not alone. Most of us just need to **load HTML file**, scrape a few headlines, and maybe pull a download link or two. In this tutorial I’ll show you exactly that—using a tiny library, a CSS selector, and an XPath contains example to **get href attribute** values.

We’ll walk through the whole process, from reading a local HTML document to printing the data you care about. No fluff, just a practical, runnable example you can drop into your own project today.

## What You’ll Learn

- How to **load an HTML file** with a lightweight parser.
- How to **use CSS selector** syntax to fetch elements like article headlines.
- How to craft an **XPath contains example** that filters links.
- How to safely **get href attribute** values from the matched nodes.
- Tips for handling malformed markup and extending the script.

You only need Python 3.8+ and the `lxml` and `cssselect` packages—both installable with a single `pip` command.

---

## Step 1: Load the HTML File

Before anything else, you need the HTML content in memory. The `lxml.html` module provides a convenient `fromstring` helper, but when you have a file on disk the `parse` function is even cleaner.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Why this matters:** Loading the file once keeps memory usage low and gives you a single `root` object that supports both CSS selectors and XPath queries. If the file is missing or unreadable, `html.parse` will raise a clear `OSError`, which you can catch later.

### Pro tip
If you’re dealing with a string rather than a file, swap `html.parse` for `html.fromstring(your_html_string)`.

---

## Step 2: Use CSS Selector to Get Headlines

CSS selectors are concise and familiar to anyone who’s written a stylesheet. Let’s grab every `<h2>` inside an `<article>`—perfect for news headlines.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Expected output** (assuming the sample HTML contains two articles):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Why CSS?** It’s readable, fast, and works out‑of‑the‑box with `lxml`. The `cssselect` method translates the selector into an XPath expression under the hood, giving you the best of both worlds.

---

## Step 3: XPath Contains Example – Find “download” Links

Sometimes you need more granular control than CSS offers. XPath’s `contains()` function shines when you want to match a substring inside an attribute, like all links that point to a download.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Sample output**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Why XPath contains?** It lets you filter directly on attribute values without extra Python loops. This is the classic **xpath contains example** you often see in tutorials, but here it’s paired with a real‑world use case.

---

## Step 4: Wrap It All Into a Reusable Function

Hard‑coding paths and prints is fine for a quick test, but production code likes functions. Below is a compact helper that returns both headlines and download links.

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

You can now call the function and pretty‑print the results:

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

Running the script yields the same output as before, but now it’s neatly packaged for reuse.

---

## Step 5: Handling Edge Cases and Common Pitfalls

1. **Missing `href` attribute** – XPath will still return the `<a>` node even if `href` is absent. Guard against `None`:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **Relative vs. absolute URLs** – If your links are relative, you may want to resolve them against the base URL:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **Malformed HTML** – `lxml` is forgiving, but extremely broken markup can cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except` block to log and skip problematic files.

4. **Performance with large files** – For multi‑megabyte pages, consider streaming with `iterparse` instead of loading the whole DOM into memory.

---

## Visual Overview (optional)

![How to parse HTML flow diagram showing load file → CSS selector → XPath contains → get href attribute](how-to-parse-html-flow.png "How to parse HTML flow diagram")

*Alt text includes the primary keyword to satisfy SEO.*

---

## Conclusion

We’ve covered **how to parse HTML** in Python from start to finish: loading an HTML file, using a CSS selector to pull article headlines, crafting an XPath contains example to locate download links, and finally **getting href attribute** values safely. The reusable `parse_news_html` function demonstrates a clean, maintainable approach you can adapt to any scraping task.

Ready for the next challenge? Try extending the script to:

- Parse tables with `//table//tr` XPath queries.
- Extract image `src` attributes using another **xpath contains example**.
- Switch to asynchronous fetching with `aiohttp` for live web pages.

Happy parsing, and remember—once you master these basics, the rest of HTML scraping becomes a piece of cake. If you hit any snags, drop a comment below—let’s troubleshoot together!


## Related Tutorials

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}