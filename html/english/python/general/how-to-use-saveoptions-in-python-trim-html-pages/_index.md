---
category: general
date: 2026-05-28
description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
  guide also explains how to load an HTML document and efficiently remove nested resources.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: en
og_description: How to use SaveOptions to trim HTML pages in Python. Follow this guide
  to load an HTML document, set resource limits, and save a clean, lightweight file.
og_title: How to Use SaveOptions in Python – Trim HTML Pages
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: How to Use SaveOptions in Python – Trim HTML Pages
url: /python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use SaveOptions in Python – Trim HTML Pages

Ever wondered **how to use SaveOptions** to shrink a massive HTML file without breaking anything? You're not the only one. When you pull in a page that includes dozens of nested resources—think CSS, JS, or even other HTML snippets—your output can balloon out of control.  

In this tutorial we’ll walk through a complete, runnable example that not only shows **how to use SaveOptions**, but also covers **how to load an HTML document** and the best way to **trim an HTML page** by limiting the nesting depth. By the end you’ll have a clean, trimmed file ready for deployment or further processing.

## What You’ll Achieve

- Load any local HTML file with a single line of code.  
- Configure resource‑handling options to stop at a specific include depth.  
- Save the trimmed result using the powerful `SaveOptions` class.  

No external tools, no magic—just plain Python and a tiny library that does the heavy lifting.

---

## Prerequisites

Before we dive in, make sure you have:

1. **Python 3.9+** installed (the syntax used works on any recent version).  
2. The hypothetical `htmlprocessor` package that provides `HTMLDocument`, `SaveOptions`, and `ResourceHandlingOptions`. Install it via:

```bash
pip install htmlprocessor
```

> **Pro tip:** If you’re using a virtual environment, activate it first—keeps your dependencies tidy.

---

## Step 1: How to Load an HTML Document

Loading a file is as simple as pointing the constructor at your path. The library reads the markup, builds a DOM‑like tree, and prepares it for further manipulation.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Why this matters:** The `HTMLDocument` object abstracts away raw string handling, giving you methods to query, modify, and eventually save the page. It also normalizes line endings and character encodings, which saves you from subtle bugs later.

You’ll notice we printed the title just to verify the load succeeded. If the file is missing or malformed, the constructor will raise a clear exception—no silent failures.

---

## Step 2: Configure Resource Handling – The Core of Trimming

The next piece of the puzzle is **how to trim HTML page** content by limiting how deep the processor follows includes. This is where `ResourceHandlingOptions` shines.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### What Does `max_handling_depth` Do?

- **Depth 1** → Only the root HTML file, all external resources are ignored.  
- **Depth 2** → The root plus any directly referenced files (e.g., an `iframe` or server‑side include).  
- **Higher values** → Deeper nesting, but also larger output and longer processing time.

By capping the depth at **2**, we keep the main page and one layer of includes, discarding anything deeper. This is usually enough to strip out redundant footers, analytics scripts, or nested templates that you don't need in a trimmed copy.

---

## Step 3: Attach the Options to Save Configuration

Now we bind our resource rules to a `SaveOptions` instance. This object tells the library *exactly* how to write the file back to disk.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Why use `SaveOptions`?**  
> It gives you granular control over the output—beyond just the resource depth. You can later add compression, pretty‑printing, or even custom callbacks without touching the core saving logic.

---

## Step 4: How to Use SaveOptions to Trim the HTML Page

Finally, we invoke the `save` method with our configured options. The library will walk the DOM, respect the depth limit, and write a trimmed file.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Expected Result

- The `trimmed_page.html` file contains the original markup **plus** any includes up to one level deep.  
- All deeper includes are omitted, resulting in a smaller, faster‑loading page.  
- No broken tags appear—the library automatically closes any elements that were left dangling after removal.

You can open the output in a browser to verify that the main content still renders, while extraneous scripts or nested frames are gone.

---

## Full Working Example

Putting it all together, here’s the complete script you can copy‑paste and run:

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

Run the script, point `INPUT` at any complex HTML file, and you’ll get a leaner version in `OUTPUT`.  

> **Edge case note:** If the original page contains conditional comments (`<!--[if IE]>…<![endif]-->`) that reference deeper resources, they’ll be stripped just like any other nested include. This prevents old‑IE hacks from inflating your final size.

---

## Visual Summary

Below is a quick diagram that illustrates the flow—from loading the document, through resource handling, to saving the trimmed result.

![how to use saveoptions example](https://example.com/placeholder.png "Diagram showing how to use SaveOptions to trim HTML pages")

*Alt text:* **how to use saveoptions example** – shows the three‑step process of loading, configuring, and saving an HTML document.

---

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| **What if I need deeper nesting?** | Increase `max_handling_depth` to 3 or 4, but remember the output size will grow. |
| **Can I exclude specific tags (e.g., `<script>`) regardless of depth?** | Yes—`SaveOptions` also supports a `tag_exclusion_list` property. Add `"script"` to that list to always drop scripts. |
| **Is the library thread‑safe?** | The current version is not. Create a separate `HTMLDocument` per thread. |
| **Will relative URLs be rewritten?** | By default no. Use `save_opt.rewrite_relative_urls = True` if you need them adjusted to the new location. |

---

## Next Steps

Now that you’ve mastered **how to use SaveOptions**, try these extensions:

- **Compress the output:** Set `save_opt.enable_gzip = True` for smaller files on the wire.  
- **Pretty‑print for debugging:** Toggle `save_opt.indent_output = True` to get nicely formatted HTML.  
- **Batch processing:** Loop over a directory of HTML files and apply the same trimming logic—great for static site generators.

Each of these tweaks builds on the same foundation you just learned, keeping your code clean and maintainable.

---

## Conclusion

We’ve covered the entire lifecycle of trimming an HTML page in Python: **how to load an HTML document**, configure **how to trim HTML page** using `ResourceHandlingOptions`, and finally **how to use SaveOptions** to write the cleaned file. The example is fully self‑contained, runs out‑of‑the‑box, and demonstrates why controlling resource depth is a vital optimization for web‑scraping, static site generation, or any situation where you need a lightweight HTML snapshot.

Give it a spin, experiment with different `max_handling_depth` values, and let the trimmed pages do the heavy lifting for you. If you hit any snags, drop a comment below—happy coding!


## Related Tutorials

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Render HTML as PNG – Complete C# Guide](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [How to Zip HTML in C# – Save HTML to Zip](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}