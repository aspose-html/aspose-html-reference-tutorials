---
category: general
date: 2026-04-06
description: Learn how to enable antialiasing, set image width and height, and save
  document as PNG in C# – a quick guide to export document to image.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: en
og_description: How to enable antialiasing when you export a document to an image.
  This guide shows you how to set image width, set image height, and save document
  as PNG.
og_title: How to Enable Antialiasing – Export Document to Image
tags:
- C#
- ImageRendering
- Antialiasing
title: How to Enable Antialiasing – Export Document to Image with C#
url: /net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Enable Antialiasing – Export Document to Image in C#

Ever wondered **how to enable antialiasing** while turning a document into a picture? Maybe you tried a quick `Save` call and the result looked jagged, especially on diagonal lines. The good news is you don’t need a graphics wizard—just a few lines of C# and the right options.

In this tutorial we’ll walk through setting the image width, setting the image height, and finally **save document as PNG** so you can **export document to image** with smooth edges. By the end you’ll have a ready‑to‑run snippet that produces a crisp 800 × 600 PNG with antialiasing turned on.

## Prerequisites

- .NET 6.0 or later (the code works on .NET Framework 4.7+ as well)  
- A reference to a rendering library that supports `ImageRenderingOptions` (e.g., Aspose.Words, Syncfusion, or any API exposing similar properties)  
- A basic understanding of C# syntax  

No heavy setup—just add the NuGet package and you’re good to go.

## Step 1: Install the Rendering Library

First, pull the package into your project. If you’re using Aspose.Words, run:

```bash
dotnet add package Aspose.Words
```

> **Pro tip:** Keep the library version up‑to‑date; the latest release (as of April 2026) adds performance tweaks for antialiasing.

## Step 2: Create the Document Object

Load or create the document you want to render. Here’s a minimal example that builds a one‑page document with a simple paragraph:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

The `Document` class is the entry point; everything you render comes from it. In real projects you’d probably load an existing .docx:

```csharp
// Document doc = new Document("input.docx");
```

## Step 3: Define Rendering Options (Width, Height, Antialiasing)

Now we answer the core question: **how to enable antialiasing**. The `ImageRenderingOptions` object lets you toggle smoothing and control dimensions.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Notice the comments: they explicitly mention **set image width**, **set image height**, and **UseAntialiasing**—the three knobs that matter most when you want a polished PNG.

### Why Antialiasing Matters

Without antialiasing, diagonal lines and curves appear stair‑stepped because the renderer treats each pixel as either on or off. Enabling it blends edge pixels, producing a visual softening that mimics what you’d see in a photo editor. The trade‑off is a tiny increase in processing time, but for most UI‑oriented exports it’s negligible.

## Step 4: Save Document as PNG (Export Document to Image)

With the options ready, we finally **save document as PNG**. The `Save` method takes the file path and the options we just configured.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

That’s it—your document is now an 800 × 600 PNG with antialiasing applied. If you open `output.png` you’ll see clean text, smooth lines, and no jagged artifacts.

### Verifying the Result

You can quickly check the file in any image viewer. Look for:

- Correct dimensions (800 × 600)  
- No visible stair‑step edges on the text or any shapes  
- A transparent background if your document didn’t contain a background color (most libraries default to white)

If the image looks jagged, double‑check that `UseAntialiasing = true` is not being overridden elsewhere.

## Step 5: Edge Cases & Variations

### Changing the Output Format

Want a JPEG instead of PNG? Just change the file extension and optionally adjust compression:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Exporting Multiple Pages

When the source document has several pages, the renderer creates separate image files per page by default. You can loop through pages:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Saving to a Stream (e.g., HTTP response)

If you’re building a web API, you might want to return the PNG directly:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Full Working Example

Below is the complete, copy‑paste‑ready program that incorporates every step discussed:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Running this program produces `output.png` in the executable’s folder. Open it, and you’ll see a smooth, 800 × 600 PNG—exactly what we set out to achieve.

## Common Questions & Troubleshooting

- **What if the image looks blurry?**  
  Blurriness can happen when you upscale a small source page. Keep the source page size close to the target dimensions, or increase the DPI via `imageOptions.Resolution` (e.g., `Resolution = 300`).

- **Does this work on .NET Framework?**  
  Yes. The same API exists in the classic framework; just reference the appropriate DLL.

- **Can I control background color?**  
  Absolutely. Set `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` before saving.

- **Is antialiasing hardware‑accelerated?**  
  Most libraries perform software antialiasing. If you need GPU acceleration, look for a rendering engine that explicitly supports it.

## Conclusion

We’ve covered **how to enable antialiasing** when you **export document to image**, walked through **set image width** and **set image height**, and showed you the exact steps to **save document as PNG**. The snippet above is ready for production, and you can now adapt it to JPEG, multi‑page PDFs, or even stream the image directly to a client.

Next, you might explore adding watermarks, adjusting DPI for print‑quality output, or integrating this logic into an ASP.NET Core endpoint. The same principles apply—just swap the file path for a response stream.

Happy coding, and enjoy those crisp, antialiased images! 

![Rendered PNG with antialiasing enabled](output.png "Rendered PNG with antialiasing enabled")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}