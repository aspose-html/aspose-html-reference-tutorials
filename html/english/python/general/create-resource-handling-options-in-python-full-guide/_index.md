---
category: general
date: 2026-07-21
description: Create resource handling options in Python and learn how to set max handling
  depth for HTML parsing. Follow this step‑by‑step tutorial for reliable resource
  management.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: en
lastmod: 2026-07-21
og_description: Create resource handling options in Python and instantly see how to
  set max handling depth for safe HTML document loading. Master the technique in minutes.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Create Resource handling options in Python – Complete Step‑by‑Step Guide
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Create Resource handling options in Python – Full Guide
url: /python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Resource handling options in Python – Full Guide

Ever wondered how to **create resource handling options** for a massive HTML page without blowing up your memory? You're not the only one. When you feed a gigantic document into a parser, nested resources like frames, iframes, or linked CSS can quickly spiral out of control.  

The good news? You can tell the parser to stop after a certain number of nested levels. In this tutorial we'll show you **how to set max handling depth** and keep your application responsive. Ready? Let’s dive in.

## What You’ll Learn

- Why limiting nesting depth matters for performance and security.  
- The exact code you need to **create resource handling options** using the `ResourceHandlingOptions` class.  
- How to configure `max_handling_depth` so the parser stops after three levels.  
- Tips for handling edge cases, such as documents with circular references or missing resources.  

No prior experience with the library is required—just a working Python 3 installation and a basic understanding of file I/O.

## Prerequisites

- Python 3.8+ (the library works on all recent versions).  
- The `htmlparser` package that provides `HTMLDocument` and `ResourceHandlingOptions`.  
- A sample HTML file (`big_page.html`) placed in a folder you can reference.  

If you haven’t installed the package yet, run:

```bash
pip install htmlparser
```

Now that the groundwork is out of the way, let’s get to the meat of the matter.

## Create Resource handling options – Step 1

First thing’s first: you need an instance of `ResourceHandlingOptions`. Think of it as a toolbox where you can set the limits and policies the parser should obey.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Why this matters:**  
When the parser encounters an `<iframe>` inside another `<iframe>`, it normally follows the chain forever. By capping the depth at `3`, you prevent runaway recursion that could otherwise exhaust RAM or cause a stack overflow.  

> **Pro tip:** If you’re parsing untrusted content (e.g., user‑uploaded HTML), consider lowering the depth to `1` or `2` to mitigate potential attacks.

## Load the HTML Document – Step 2

With your options object ready, pass it to `HTMLDocument`. The constructor will respect the `max_handling_depth` you just set.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**What’s happening under the hood?**  
`HTMLDocument` reads the file, builds a DOM tree, and then walks through every external resource (stylesheets, scripts, images). Whenever it hits a nested resource, it checks `resource_options.max_handling_depth`. If the limit is reached, the parser logs a warning and skips further nesting.  

That means you get a fully usable DOM for the first three layers, and the rest is safely ignored.

## Verify the Configuration – Step 3

It’s always a good idea to confirm that your settings took effect. The `resource_options` object exposes its current state, so you can print it out or assert it in a test.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

If the assertion passes, you can be confident that the parser will obey the limit throughout the rest of the run.

## Handling Edge Cases

### Circular References

Some legacy sites embed an iframe that points back to the original page, creating a loop. With `max_handling_depth` set, the loop is automatically broken after the third iteration. However, you might still see a warning in the logs. To silence noisy logs, adjust the logger level:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Missing Resources

If a nested resource fails to load (404 or network timeout), the parser throws an exception by default. Wrap the loading call in a `try/except` block to keep your application alive:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Adjusting Depth Dynamically

Sometimes you need different depths for different parts of your pipeline. Because `resource_options` is a mutable object, you can change `max_handling_depth` on the fly:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Just remember to reset the value before re‑using the same options instance in another thread.

## Full Working Example

Below is a complete script you can copy‑paste, adjust the file paths, and run immediately.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**Expected output (when files exist and are well‑formed):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

If a file cannot be read, you’ll see an error message instead of a crash.

![Create resource handling options in Python](/images/resource-options.png){alt="Create resource handling options in Python"}

## Recap – Why This Approach Rocks

- **Safety first:** Limiting nesting depth prevents runaway recursion and memory bloat.  
- **Flexibility:** You can change `max_handling_depth` at runtime to suit different scenarios.  
- **Simplicity:** A handful of lines of code let you **create resource handling options** and immediately apply them.  

In short, you now have a robust pattern for controlling how deeply your parser follows external resources.

## What’s Next?

- Explore the `ResourceHandlingOptions` class further—there are flags for caching, timeout handling, and MIME‑type filtering.  
- Combine depth limiting with a custom `UserAgent` string to avoid being blocked by aggressive servers.  
- If you’re working with asynchronous I/O, look into the `aiohtmlparser` variant that respects the same options but works with `asyncio`.  

Feel free to experiment: try setting the depth to `0` and watch the parser ignore every external reference. It’s a handy shortcut when you only need the raw HTML markup.

Got questions or a tricky page that still trips you up? Drop a comment below, and I’ll gladly help you fine‑tune the settings. Happy parsing!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create sandbox for HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}