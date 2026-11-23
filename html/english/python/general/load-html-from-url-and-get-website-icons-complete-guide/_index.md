---
category: general
date: 2026-06-10
description: Load HTML from URL to get website icons quickly. Learn how to extract
  favicons, fetch website favicon URLs, and handle edge cases in Python.
draft: false
keywords:
- load html from url
- get website icons
- how to extract favicons
- extract favicon urls
- fetch website favicon urls
language: en
og_description: Load HTML from URL to extract favicons and fetch website favicon URLs.
  A step‑by‑step Python tutorial for developers.
og_title: Load HTML from URL and Get Website Icons – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML from URL to get website icons quickly. Learn how to extract
    favicons, fetch website favicon URLs, and handle edge cases in Python.
  headline: Load HTML from URL and Get Website Icons – Complete Guide
  type: TechArticle
tags:
- web scraping
- favicon extraction
- python
- html parsing
title: Load HTML from URL and Get Website Icons – Complete Guide
url: /python/general/load-html-from-url-and-get-website-icons-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Load HTML from URL and Get Website Icons – Complete Guide

Ever needed to **load HTML from URL** just to pull a site’s tiny logo? You’re not alone. Whether you’re building a bookmark manager, a SEO dashboard, or just a personal hobby project, getting website icons is a small but essential piece of the puzzle.

In this tutorial we’ll show you **how to extract favicons** using plain Python—no heavy Selenium, no browser magic. By the end you’ll be able to **fetch website favicon URLs**, handle relative paths, and even grab multiple icons if a site provides them. Ready? Let’s dive in.

## Why Load HTML from URL in the First Place?

Loading the raw HTML of a page gives you direct access to the `<link>` tags that browsers use to locate favicons. Those tags usually look like:

```html
<link rel="icon" href="/favicon.ico">
<link rel="apple-touch-icon" href="https://example.com/apple-touch-icon.png">
```

If you can pull that markup, you can programmatically read the `href` attribute and download the image yourself. It’s faster than scraping screenshots, and it works for any site that follows the standard conventions.

## Step 1 – Load the HTML Document from a URL

The first thing we need is a way to fetch the page source. The most popular choice in Python is the **requests** library because it’s simple, reliable, and handles redirects out of the box.

```python
import requests

def fetch_html(url: str) -> str:
    """
    Retrieve the raw HTML from the given URL.
    Raises an exception if the request fails.
    """
    response = requests.get(url, timeout=10)
    response.raise_for_status()          # Fail fast on HTTP errors
    return response.text
```

> **Pro tip:** If you’re working behind a corporate proxy, pass `proxies=` to `requests.get`. Also, setting a short timeout prevents your script from hanging on dead sites.

Now we can call `fetch_html("https://example.com")` and get a string containing the page’s markup. This is the core of **load HTML from URL**—the rest of the pipeline works with that string.

## Step 2 – Get Website Icons

Once we have the HTML, the next step is to locate every `<link>` element whose `rel` attribute mentions “icon”. The built‑in `html.parser` module can do the job, but **BeautifulSoup** makes the code far more readable.

```python
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def extract_icon_links(html: str, base_url: str) -> list[str]:
    """
    Parse the HTML and return a list of absolute URLs pointing to icons.
    Handles relative hrefs by joining them with the page’s base URL.
    """
    soup = BeautifulSoup(html, "html.parser")
    icons = []

    # Look for any <link> tag where rel contains "icon"
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            # Convert relative URLs to absolute ones
            absolute_url = urljoin(base_url, href)
            icons.append(absolute_url)

    return icons
```

Notice how we use `urljoin` to turn `"/favicon.ico"` into `"https://example.com/favicon.ico"`—that’s a common edge case when **get website icons**. Some sites even serve different icons for different devices, so you might end up with a handful of URLs. No problem; we just collect them all.

## Step 3 – Extract Favicon URLs and Display Them

Putting the pieces together is straightforward. We’ll fetch the HTML, run the extractor, and print the resulting list. The final script looks like this:

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def extract_icon_links(html: str, base_url: str) -> list[str]:
    soup = BeautifulSoup(html, "html.parser")
    icons = []
    for link in soup.find_all("link", rel=lambda r: r and "icon" in r.lower()):
        href = link.get("href")
        if href:
            icons.append(urljoin(base_url, href))
    return icons

def main():
    target = "https://example.com"
    html = fetch_html(target)
    icon_urls = extract_icon_links(html, target)
    print("Found icon URLs:", icon_urls)

if __name__ == "__main__":
    main()
```

### Expected Output

Running the script against a site that provides a standard favicon might give you:

```
Found icon URLs: ['https://example.com/favicon.ico']
```

If the site supplies multiple icons (Apple touch icon, shortcut icon, etc.), you’ll see a longer list:

```
Found icon URLs: [
    'https://example.com/favicon.ico',
    'https://example.com/apple-touch-icon.png',
    'https://example.com/favicon-32x32.png'
]
```

That’s the entire **extract favicon urls** workflow—compact, dependency‑light, and ready to be dropped into any project.

## Handling Common Pitfalls

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Relative `href` without a `<base>` tag** | `urljoin` assumes the page URL as the base, which works for most cases. | If a `<base href="...">` tag exists, read it first and pass that as `base_url`. |
| **Missing `rel="icon"`** | Some sites use `rel="shortcut icon"` or custom values. | Extend the lambda: `rel=lambda r: r and ("icon" in r.lower() or "shortcut" in r.lower())`. |
| **Redirects to a different domain** | The favicon may live on a CDN. | `urljoin` will correctly resolve the new domain because it uses the final request URL (`response.url`). |
| **Broken links (404)** | The HTML points to a file that no longer exists. | After extracting URLs, you can verify each with a HEAD request before using them. |
| **Multiple `<link>` tags with the same icon** | Duplicate entries inflate the list. | Use `set(icon_urls)` to deduplicate before returning. |

## Going Further – Fetch Website Favicon URLs in Bulk

If you need to **fetch website favicon URLs** for a list of domains, wrap the `main` logic in a loop:

```python
domains = ["https://example.com", "https://python.org", "https://github.com"]
for site in domains:
    try:
        icons = extract_icon_links(fetch_html(site), site)
        print(site, "->", icons)
    except Exception as e:
        print(site, "error:", e)
```

This pattern scales nicely, and you can add caching (e.g., with `functools.lru_cache`) to avoid hammering the same site repeatedly.

## Visual Overview

![Load HTML from URL diagram](load-html-url.png)

*Alt text: Load HTML from URL diagram showing fetch → parse → extract steps.*

The image above condenses the three‑step process: **load HTML from URL**, **get website icons**, and **extract favicon URLs**. It’s handy when you need to explain the flow to a teammate.

## Conclusion

We’ve walked through a complete, production‑ready solution for how to **load HTML from URL** and **get website icons** using only Python’s requests and BeautifulSoup libraries. By extracting the `href` attributes of `<link rel="icon">` tags, you can **extract favicon URLs**, handle relative paths, and even retrieve multiple icon formats—all in a few dozen lines of code.

What’s next? Try downloading the icons to a local folder, generate a CSV of domain‑to‑favicon mappings, or plug this logic into a Flask API that serves favicons on demand. The possibilities for **fetch website favicon URLs** are endless, and the core technique stays the same.

Got questions about edge cases, or want to share a clever tweak? Drop a comment below—happy icon hunting!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Load HTML Documents from Stream with Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Handle Document Load Events in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}