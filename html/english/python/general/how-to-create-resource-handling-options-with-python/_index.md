---
category: general
date: 2026-10-15
description: Learn how to create resource handling options and how to set max handling
  depth for Markdown saving in Python. Follow a step‑by‑step guide.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: en
lastmod: 2026-10-15
og_description: Create resource handling options in Python to control nested resource
  processing. This tutorial shows how to set max handling depth for reliable Markdown
  exports.
og_image_alt: Screenshot showing Python code to create resource handling options and
  set max handling depth
og_title: Create resource handling options – Python guide
schemas:
- author: Aspose
  dateModified: '2026-10-15'
  description: Learn how to create resource handling options and how to set max handling
    depth for Markdown saving in Python. Follow a step‑by‑step guide.
  headline: How to create resource handling options with Python
  type: TechArticle
tags:
- resource handling
- Markdown
- Python
- options
title: How to create resource handling options with Python
url: /python/general/how-to-create-resource-handling-options-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create resource handling options with Python

If you need to **create resource handling options** for a Markdown export, this guide gives you a complete solution. You’ll see exactly **how to set max handling depth** so that nested resources stop processing after the desired level.

Resource handling is essential when you generate Markdown from complex documents that contain images, embedded files, or other linked assets. Uncontrolled recursion can lead to performance issues or out‑of‑memory errors. By configuring the handling depth, you keep the process predictable and efficient.

In this tutorial you will:

* Initialize a `ResourceHandlingOptions` object.
* Configure the maximum handling depth.
* Attach the options to a `MarkdownSaveOptions` instance.
* Run a full example that you can copy into your project.

No external libraries beyond the standard SDK are required, and the code works with the latest version of the Python package as of October 2026.

## Prerequisites

Before you start, make sure you have:

* Python 3.9 or newer installed.
* The SDK that provides `ResourceHandlingOptions` and `MarkdownSaveOptions` (for example, `groupdocs-viewer` or a similar package). Install it with:

```bash
pip install groupdocs-viewer
```

* Basic familiarity with Python classes and object attributes.

## Step 1: Create resource handling options

The first step is to **create resource handling options**. This object acts as a container for all resource‑related settings.

```python
from groupdocs.viewer import ResourceHandlingOptions, MarkdownSaveOptions

# Step 1: Instantiate the options object
resource_options = ResourceHandlingOptions()
```

`ResourceHandlingOptions` does not apply any limits by default, which means the viewer will follow every linked resource it encounters. Initializing the object gives you a clean slate to apply precise controls.

## Step 2: How to set max handling depth

Now you’ll learn **how to set max handling depth**. The property `max_handling_depth` defines the number of nested levels the exporter will process before stopping.

```python
# Step 2: Limit the handling depth to five levels
resource_options.max_handling_depth = 5
```

Why limit the depth? Imagine a Markdown document that references another Markdown file, which in turn references a third file, and so on. Without a depth limit, the exporter could recurse indefinitely, consuming memory and CPU. Setting `max_handling_depth` to `5` tells the engine to stop after five nested resources, which is a safe default for most projects.

### Edge case: unlimited depth

If you deliberately want unlimited recursion (rare in production), set the value to `None`:

```python
resource_options.max_handling_depth = None  # No limit
```

Be aware that unlimited depth can cause performance degradation on very large document trees.

## Step 3: Attach the options to MarkdownSaveOptions

After configuring the resource handling, you must attach the options to a `MarkdownSaveOptions` instance. This tells the exporter to use the settings when saving.

```python
# Step 3: Create MarkdownSaveOptions and attach the resource handling config
markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

`MarkdownSaveOptions` aggregates all export‑related settings. By assigning `resource_options` to its `resource_handling_options` attribute, you ensure that the depth limit is enforced during the conversion.

## Step 4: Run a complete conversion (optional demo)

The following snippet demonstrates a full conversion from a sample document to Markdown using the options you just built. Adjust the file paths to match your environment.

```python
from groupdocs.viewer import Viewer

# Path to the source document (e.g., a DOCX with embedded images)
source_path = "sample.docx"
# Path where the Markdown output will be saved
output_path = "output.md"

# Initialize the viewer with the source file
viewer = Viewer(source_path)

# Perform the conversion using the configured options
viewer.save(output_path, markdown_options)

print(f"Conversion complete. Markdown saved to {output_path}")
```

**Expected output**

```
Conversion complete. Markdown saved to output.md
```

After running the script, open `output.md`. You will see that images and other resources are referenced up to five levels deep; any deeper links are omitted, preventing runaway recursion.

## Pro tip: verify the handling depth at runtime

If you need to confirm that the depth limit is applied, you can inspect the generated Markdown for missing resource references or enable verbose logging in the SDK:

```python
viewer.set_logging(True)  # Enable detailed logs
```

The log will show messages like:

```
[INFO] Resource handling stopped at depth 5 for file 'nested_image.png'
```

## Common questions

**What if my document has fewer than five nested resources?**  
The exporter will process all available resources because the depth limit is higher than the actual depth. No resources are truncated.

**Can I set a different limit for different file types?**  
Yes. Create separate `ResourceHandlingOptions` objects for each export format and assign them to the corresponding `SaveOptions` instance.

**Does the depth limit affect only images?**  
No. The limit applies to *all* resources that the exporter can follow, including embedded files, hyperlinks, and nested Markdown includes.

## Conclusion

You now know how to **create resource handling options** and **set max handling depth** for reliable Markdown exports in Python. By limiting recursion, you protect your application from excessive memory usage while still preserving the necessary content hierarchy.

Next steps you might explore:

* Adjust other `ResourceHandlingOptions` properties such as `extract_images` or `preserve_links`.
* Combine resource handling with custom naming conventions for extracted files.
* Experiment with different depth values to find the sweet spot for your specific document sets.

Feel free to adapt the code snippets to your own workflow and share your findings with the community. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Zip HTML in C# – Custom Resource Handler Tutorial](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-custom-resource-handler-tutorial/)
- [How to create custom schema handler with Aspose.HTML for Java](/html/english/java/custom-schema-message-handling/custom-schema-message-handler/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}