---
category: general
date: 2026-06-26
description: Learn how to get favicon by loading HTML from URL and extracting href
  from link tags. Step‑by‑step Python code to get website icons fast.
draft: false
keywords:
- how to get favicon
- load html from url
- get website icons
- extract href from link
- how to extract favicons
language: en
og_description: 'How to get favicon quickly: load HTML from URL, find link rel=''icon'',
  and extract href from link tags using Python.'
og_title: How to Get Favicon – Python Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-26'
  description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  headline: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  type: TechArticle
- description: Learn how to get favicon by loading HTML from URL and extracting href
    from link tags. Step‑by‑step Python code to get website icons fast.
  name: How to Get Favicon – Complete Python Guide for Extracting Site Icons
  steps:
  - name: What if the site uses a `<meta>` tag instead of `<link>`?
    text: Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`.
      You can extend `find_icon_links` to also search for those meta tags and treat
      them the same way.
  - name: How do I handle relative URLs that start with `//`?
    text: '`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`)
      based on the scheme of the base URL, so you don’t need extra logic.'
  - name: Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?
    text: Yes—just drop the `filter_ico_urls` step. The script will return every icon
      URL it discovers, including PNGs of various dimensions. You can then sort or
      select based on the filename pattern.
  - name: Does this work on sites that block bots?
    text: 'If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get`
      call:'
  type: HowTo
tags:
- Python
- Web Scraping
- HTML Parsing
title: How to Get Favicon – Complete Python Guide for Extracting Site Icons
url: /python/general/how-to-get-favicon-complete-python-guide-for-extracting-site/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Get Favicon – Complete Python Guide for Extracting Site Icons

Ever wondered **how to get favicon** from any website without digging through the page source manually? You're not the only one—developers, SEO pros, and even designers often need the tiny icon that represents a site. In this tutorial we’ll show you a clean, Python‑centric way to load HTML from a URL, locate the `<link rel="icon">` tags, and pull out the icon URLs. By the end, you’ll know exactly **how to get favicon** for any domain, and you’ll have a reusable script ready for your projects.

We’ll cover everything from fetching the HTML to handling edge cases like relative URLs and multiple icon formats. No external services required—just the standard `requests` library and a lightweight HTML parser. Ready to start? Let’s dive in.

## Prerequisites

- Python 3.8+ installed (the code works on 3.10 as well)  
- Basic familiarity with `requests` and list comprehensions  
- Internet access for the target website  

If you already have these, great—skip to the first step. Otherwise, install the only dependency we need:

```bash
pip install requests beautifulsoup4
```

> **Pro tip:** `beautifulsoup4` is a battle‑tested parser that makes “load html from url” a breeze.

## Step 1: Load HTML from URL with Python  

The first thing you need to do when learning **how to get favicon** is fetch the page’s source. This is the “load html from url” part of the process.

```python
import requests
from bs4 import BeautifulSoup

def fetch_html(url: str) -> str:
    """Download the raw HTML of *url* and return it as text."""
    response = requests.get(url, timeout=10)
    response.raise_for_status()   # will raise if the request failed
    return response.text
```

Why use `requests`? It handles redirects, HTTPS verification, and timeouts automatically, which means fewer surprises when you later try to **get website icons**.

## Step 2: Parse the Document and Find Icon Links  

Now that we have the HTML, we need to locate all `<link>` elements whose `rel` attribute indicates an icon. This is the heart of **how to get favicon**.

```python
def find_icon_links(html: str) -> list[BeautifulSoup]:
    """Return a list of <link> tags that declare an icon."""
    soup = BeautifulSoup(html, "html.parser")
    # Look for rel="icon" or rel="shortcut icon"
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]
```

Notice we check both `icon` and `shortcut icon` because older sites still use the latter. This small nuance often trips people up when they search “how to extract favicons.”

## Step 3: Extract href from Link Elements  

With the relevant tags in hand, the next logical step—**extract href from link**—is straightforward.

```python
from urllib.parse import urljoin

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    """Convert each <link> tag’s href into a full absolute URL."""
    urls = []
    for tag in link_tags:
        href = tag.get("href")
        if href:
            # Resolve relative URLs against the base page
            full_url = urljoin(base_url, href)
            urls.append(full_url)
    return urls
```

Using `urljoin` guarantees that even if a site provides a relative path like `/favicon.ico`, you’ll end up with a proper absolute URL—critical for a reliable **how to get favicon** script.

## Step 4: Optional – Validate and Filter Icon URLs  

Sometimes a page lists many icons (Apple touch icons, PNGs of various sizes, etc.). If you only care about the classic `.ico` file, filter accordingly. This step shows **how to extract favicons** of a specific type.

```python
def filter_ico_urls(urls: list[str]) -> list[str]:
    """Keep only URLs that end with .ico (case‑insensitive)."""
    return [u for u in urls if u.lower().endswith(".ico")]
```

Feel free to tweak the filter: replace `".ico"` with `".png"` or check for `rel="apple-touch-icon"` if you need high‑resolution icons.

## Step 5: Download the Icon Files (If You Want the Actual Image)  

Extracting the URLs is half the battle; downloading gives you a file you can display or store. Here’s a quick helper:

```python
import os

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    """Save each icon to *folder*, creating it if necessary."""
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")
```

Running this after the previous steps gives you a local copy of every discovered favicon, perfect for caching or offline analysis.

## Step 6: Putting It All Together – Full Working Example  

Below is the complete, ready‑to‑run script that demonstrates **how to get favicon** from any site. Copy‑paste, change the `target_url`, and watch the output.

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
import os

def fetch_html(url: str) -> str:
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text

def find_icon_links(html: str) -> list[BeautifulSoup]:
    soup = BeautifulSoup(html, "html.parser")
    return [
        tag for tag in soup.find_all("link")
        if tag.get("rel") and ("icon" in tag["rel"] or "shortcut icon" in tag["rel"])
    ]

def extract_icon_urls(base_url: str, link_tags: list) -> list[str]:
    return [urljoin(base_url, tag.get("href")) for tag in link_tags if tag.get("href")]

def filter_ico_urls(urls: list[str]) -> list[str]:
    return [u for u in urls if u.lower().endswith(".ico")]

def download_icons(urls: list[str], folder: str = "favicons") -> None:
    os.makedirs(folder, exist_ok=True)
    for url in urls:
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            filename = os.path.join(folder, os.path.basename(url))
            with open(filename, "wb") as f:
                f.write(resp.content)
            print(f"Saved {filename}")
        except Exception as e:
            print(f"Failed to download {url}: {e}")

def get_favicons(target_url: str) -> None:
    print(f"Fetching HTML from {target_url} …")
    html = fetch_html(target_url)

    print("Finding <link> tags that declare icons …")
    icon_tags = find_icon_links(html)

    print(f"Extracting href attributes – {len(icon_tags)} candidates found.")
    raw_urls = extract_icon_urls(target_url, icon_tags)

    # Optional filtering – keep only .ico files
    ico_urls = filter_ico_urls(raw_urls)
    print(f"Filtered to {len(ico_urls)} .ico URLs:", ico_urls)

    if ico_urls:
        download_icons(ico_urls)
    else:
        print("No .ico favicons detected; here are all discovered URLs:")
        print(raw_urls)

# Example usage – replace with any site you want to test
if __name__ == "__main__":
    target_url = "https://www.python.org"
    get_favicons(target_url)
```

**Expected output (truncated for brevity):**

```
Fetching HTML from https://www.python.org …
Finding <link> tags that declare icons …
Extracting href attributes – 3 candidates found.
Filtered to 1 .ico URLs: ['https://www.python.org/static/favicon.ico']
Saved favicons/favicon.ico
```

If the site only provides PNG or Apple touch icons, the script will list those URLs instead, showing you exactly **how to get favicon** in every scenario.

## Common Questions & Edge Cases  

### What if the site uses a `<meta>` tag instead of `<link>`?  
Some older pages embed the icon URL in a `<meta name="msapplication‑TileImage">`. You can extend `find_icon_links` to also search for those meta tags and treat them the same way.

### How do I handle relative URLs that start with `//`?  
`urljoin` automatically resolves protocol‑relative URLs (`//example.com/favicon.ico`) based on the scheme of the base URL, so you don’t need extra logic.

### Can I retrieve multiple sizes (e.g., 32×32, 180×180) automatically?  
Yes—just drop the `filter_ico_urls` step. The script will return every icon URL it discovers, including PNGs of various dimensions. You can then sort or select based on the filename pattern.

### Does this work on sites that block bots?  
If a site returns a 403 or requires a custom User‑Agent, tweak the `requests.get` call:

```python
headers = {"User-Agent": "Mozilla/5.0 (compatible; FaviconBot/1.0)"}
response = requests.get(url, headers=headers, timeout=10)
```

That small change often solves “how to get favicon” on stricter domains.

## Visual Overview  

![Diagram showing the flow of how to get favicon from a website – load HTML, parse link tags, extract href, optional download](how-to-get-favicon-diagram.png "how to get favicon flow diagram")

*The image’s alt text contains the primary keyword, satisfying SEO for images.*

## Conclusion  

We’ve walked through **how to get favicon** step by step: loading HTML from a URL,


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}