---
category: general
date: 2026-08-15
description: Create custom resource handler in C# to manage HTML resources like images
  and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: en
lastmod: 2026-08-15
og_description: Create custom resource handler in C# to control how HTML resources
  are streamed. This tutorial shows HTMLLoadOptions setup, memory stream handling,
  and loading HTMLDocument with custom logic.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Create custom resource handler in C# – full guide for HTML resource management
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Create custom resource handler in C# for HTML loading
url: /net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create custom resource handler in C# for HTML loading

If you need to **create custom resource handler** for HTML files, this guide shows you exactly how. You’ll learn to intercept images, CSS, and other assets while loading an HTML document, using `HTMLLoadOptions` and a memory‑based stream.

The tutorial covers everything required to implement a reusable handler, configure load options, and verify that resources are captured correctly. No external documentation is needed—just the code below and the explanations.

## Prerequisites

- .NET 6.0 or later
- Basic familiarity with C#
- A reference to the HTML processing library that provides `HTMLDocument`, `HtmlLoadOptions`, and `ResourceHandler` (e.g., GroupDocs.Viewer for .NET)

## Overview of the solution

We will:

1. **Create a custom resource handler** by subclassing `ResourceHandler`.
2. Configure `HTMLLoadOptions` to use the handler.
3. Load an HTML file with `HTMLDocument` while the handler supplies a stream for each resource.
4. (Optional) Store received resources to disk for verification.

Each step includes full source code and the reasoning behind it.

## Step 1: Define the custom resource handler class

Creating a custom handler means overriding `HandleResource` so the library can write resource bytes to a stream you control. Using a `MemoryStream` keeps the data in memory, which is ideal for testing or further processing.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Why this matters:**  
Overriding `HandleResource` gives you complete control over where resource data goes. If you later need to cache images, transform CSS, or log resource usage, you can replace the `MemoryStream` with any custom stream implementation.

## Step 2: Configure `HTMLLoadOptions` to use the handler

`HTMLLoadOptions` lets you plug the handler into the loading pipeline. Setting the `ResourceHandler` property tells the viewer to invoke `MyHandler` for every external asset.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Why this matters:**  
Without assigning `ResourceHandler`, the viewer would write resources to its default location (often a temporary folder). By specifying your own handler, you **create custom resource handler** behavior that aligns with your application’s storage strategy.

## Step 3: Load the HTML document with the configured options

Now load the HTML file. The viewer will call `MyHandler.HandleResource` for each resource it encounters.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

At this point the HTML content is parsed, and all external resources have been streamed into the memory buffers supplied by `MyHandler`.

## Step 4 (optional): Access the captured resources

If you need to inspect or persist the resources, you can modify `MyHandler` to store each `MemoryStream` in a dictionary keyed by the resource name.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

After loading, you can iterate over `handler.Resources` and write each to disk:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Why this matters:**  
Storing resources enables post‑processing such as image optimization, CSS minification, or archiving. It also provides a tangible verification that the **create custom resource handler** logic works as intended.

## Step 5: Clean up

Both `HTMLDocument` and any streams should be disposed to free unmanaged resources.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Full runnable example

Below is a self‑contained program that demonstrates all steps from class definition to resource extraction.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Expected output**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

The console lists each resource that the viewer streamed through your custom handler, confirming that the **create custom resource handler** workflow succeeded.

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| *What if a resource is large (e.g., high‑resolution image)?* | Replace `MemoryStream` with a `FileStream` pointing to a temporary folder. This prevents excessive memory consumption. |
| *Can I filter resources by type?* | Inside `HandleResource`, inspect `info.MimeType` or `info.Extension` and return `null` for unwanted types. Returning `null` tells the viewer to skip the resource. |
| *Is thread safety required?* | If the same handler instance is used across multiple concurrent loads, protect the `Resources` dictionary with a lock or use a concurrent collection. |
| *How do I support relative URLs?* | `ResourceInfo` contains the original URL; you can combine it with the base path of the HTML file to resolve relative references before storing. |

## Conclusion

You now know how to **create custom resource handler** in C# for HTML loading, configure `HTMLLoadOptions`, capture streamed assets, and clean up responsibly. This pattern gives you full control over resource management, enabling scenarios such as on‑the‑fly image processing, CSS rewriting, or secure storage.

Next, explore related topics like **HTMLDocument loading** with different rendering options, or extend the handler to **C# resource handler** implementations that write directly to cloud storage. Experiment with the handler’s `HandleResource` method to fit your project’s specific resource workflow.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Custom Resource Handler in C# – Convert HTML to ZIP Tutorial](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}