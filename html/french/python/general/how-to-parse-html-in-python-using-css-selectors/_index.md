---
category: general
date: 2026-10-21
description: Apprenez à analyser le HTML en Python, à charger un document HTML, à
  utiliser les sélecteurs CSS et à extraire rapidement les hyperliens du HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: fr
lastmod: 2026-10-21
og_description: Comment analyser le HTML en Python avec des sélecteurs CSS. Charger
  un document HTML, sélectionner les liens et extraire les hyperliens du HTML avec
  un code propre.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: Comment analyser le HTML en Python – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: Comment analyser le HTML en Python à l'aide de sélecteurs CSS
url: /fr/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to parse HTML in Python using CSS selectors

If you need to **how to parse html** in a Python script, this guide shows you exactly that. You’ll learn how to load an HTML document, how to use selector syntax to find elements, and how to extract hyperlinks from html without writing a custom parser.

Parsing HTML is a common task for web scrapers, data‑analysis pipelines, or automated testing. By the end of this tutorial you’ll have a reusable function that loads an HTML document, selects all `<a>` tags with a CSS selector, and returns a clean list of URLs.

## What you’ll need

- Python 3.8+ (the code works on any recent version)  
- The **lxml** library (`pip install lxml`) – provides fast HTML parsing and CSS selector support  
- An HTML file you want to analyse (e.g., `sample.html`)  

No additional tools are required; everything runs with the standard library and a single third‑party package.

## Step 1: How to parse HTML – load the document

The first step in any HTML workflow is to read the file into memory. Using **lxml.html** gives you a tree object that supports CSS selectors.

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**Why this matters:**  
`load_html` abstracts the file‑reading boilerplate and guarantees the document is parsed with a tolerant HTML parser. This is the safest way to **load html document python** without worrying about malformed markup.

## Step 2: How to use selector – find all link elements

Once the document is loaded, you can use a CSS selector to locate every `<a>` tag. The selector `"a"` matches all anchor elements, but you could refine it (e.g., `"a.external"` or `"nav a"`).

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**Why this matters:**  
The **how to use selector** approach lets you express complex queries in a single, readable string, avoiding manual tree traversal. It works for any CSS pattern supported by `lxml.cssselect`.

## Step 3: Extract hyperlinks from HTML and process them

Now that you have a list of `<a>` elements, you can pull the `href` attribute from each one. The helper below also normalises relative URLs against a base URL (if you provide one).

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**Expected output** (assuming `sample.html` contains three links):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**Why this matters:**  
`extract_hyperlinks` is the core of **extract hyperlinks from html**. It gracefully handles missing `href` attributes, resolves relative links, and returns a plain Python list that you can feed into further processing (e.g., requests, pandas, or a database).

## Full end‑to‑end example

Putting the three functions together gives you a single script that loads a file, selects all anchors, and prints each hyperlink.

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

Running `python parse_links.py` prints every hyperlink, fully resolved, to the console. This script demonstrates **how to parse html**, **how to use selector**, and **extract hyperlinks from html** in a single, reusable flow.

## Common variations and edge‑case handling

| Situation | What to change | Reason |
|-----------|----------------|--------|
| **Only absolute URLs needed** | Omit the `base_url` argument in `extract_hyperlinks` | Keeps relative URLs untouched |
| **You need the link text as well** | Return a tuple `(href, link.text_content())` from `extract_hyperlinks` | Allows you to store both URL and anchor text |
| **Large HTML files** | Use `lxml.etree.iterparse` with a CSS selector filter | Reduces memory usage by streaming |
| **Different selector** | Replace `"a"` with `"nav a[href]"` or `"div.content a.external"` | Targets a subset of links, useful for **how to use selector** in complex pages |

**Pro tip:** Always validate the extracted URLs before making network requests. A quick `urlparse` check can filter out malformed strings and protect your scraper from crashes.

## Conclusion

You now know **how to parse html** in Python, how to **load html document python**, how to **how to use selector** to target elements, and how to **extract hyperlinks from html** efficiently. The complete example above is ready to copy‑paste into your project, and you can adapt each function to suit more advanced use cases such as pagination, JavaScript‑generated content, or multi‑page crawling.

Next steps you might explore include:

- Using **requests‑html** or **Playwright** to fetch pages that require JavaScript execution.  
- Storing the extracted URLs in a CSV or SQLite database for later analysis.  
- Adding error handling for network timeouts and HTTP status codes.

Happy parsing, and feel free to experiment with different selectors to unlock the full power of CSS‑based HTML queries in Python!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to configure HTML resource handling in Python and load an HTML document](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [How to Parse HTML in Python – Complete Guide](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [How to Load HTML in Python – Step‑by‑Step Guide](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}