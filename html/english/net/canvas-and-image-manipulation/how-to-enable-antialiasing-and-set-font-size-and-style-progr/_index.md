---
category: general
date: 2026-11-20
description: How to enable antialiasing in C# graphics and set font size, set font
  style programmatically with a complete, runnable example using ImageRenderingOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable antialiasing
- set font size
- set font style programmatically
- C# graphics rendering
- ImageRenderingOptions example
language: en
lastmod: 2026-11-20
og_description: How to enable antialiasing in C# graphics, set font size, and set
  font style programmatically using ImageRenderingOptions – complete code and explanation.
og_image_alt: Screenshot of antialiased text with custom font size and style generated
  by C# code showing how to enable antialiasing
og_title: How to enable antialiasing and set font size & style programmatically in
  C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: How to enable antialiasing in C# graphics and set font size, set font
    style programmatically with a complete, runnable example using ImageRenderingOptions.
  headline: How to enable antialiasing and set font size and style programmatically
    in C#
  type: TechArticle
tags:
- C#
- graphics
- antialiasing
- fonts
title: How to enable antialiasing and set font size and style programmatically in
  C#
url: /net/canvas-and-image-manipulation/how-to-enable-antialiasing-and-set-font-size-and-style-progr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to enable antialiasing and set font size and style programmatically in C#

How to enable antialiasing in C# graphics is a frequent requirement when you need smooth edges on shapes or text. This tutorial shows you how to enable antialiasing, set font size, and set font style programmatically using the **ImageRenderingOptions** class. By the end of the guide you will have a self‑contained console application that renders crisp, styled text into an image file.

You’ll learn how to configure the rendering pipeline, choose the right font family, adjust the font size, and apply bold or italic styles without leaving your code. The only prerequisite is a recent .NET SDK and the Aspose.Imaging NuGet package, which the example installs automatically.

## Prerequisites

- .NET 6.0 SDK or later (download from https://dotnet.microsoft.com/)
- Visual Studio 2022 or any editor that supports .NET projects
- **Aspose.Imaging** NuGet package (the library that provides `ImageRenderingOptions`)

You can add the package with the following command:

```bash
dotnet add package Aspose.Imaging
```

## How to enable antialiasing with ImageRenderingOptions

`ImageRenderingOptions` is the central object that controls how Aspose.Imaging draws graphics. Setting its `UseAntialiasing` property tells the rasterizer to smooth edges, which eliminates the jagged “staircase” effect that appears when antialiasing is off.

```csharp
// Step 1: Create a new ImageRenderingOptions instance
ImageRenderingOptions renderingOptions = new ImageRenderingOptions();

// Step 2: Enable antialiasing for smoother graphics
renderingOptions.UseAntialiasing = true;
```

Enabling antialiasing is essential for high‑quality UI elements, chart rendering, and any situation where visual fidelity matters.

## Set font size programmatically

The font size determines how large the glyphs appear in the final bitmap. You can change it by constructing a `Font` object with the desired point size. The example below sets the size to **24 pt**, which is a common size for readable headings.

```csharp
// Step 3: Choose a font family and size
Font font = new Font("Arial", 24); // 24‑point Arial
```

You can replace `24` with any integer or floating‑point value to meet your layout requirements. The `Font` class also accepts a `GraphicsUnit` parameter if you need pixel‑based sizing.

## Set font style programmatically

Applying bold, italic, or underline styles is a matter of passing a `WebFontStyle` flag when you create the `Font`. The `WebFontStyle` enum combines multiple styles using a bitwise OR operation.

```csharp
// Step 4: Apply bold and italic styles
font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);
```

If you only need a single style, use `WebFontStyle.Bold`, `WebFontStyle.Italic`, or `WebFontStyle.Underline`. This approach lets you **set font style programmatically** without hard‑coding separate font files.

## Full runnable example

Below is a complete console application that puts everything together:

```csharp
using System;
using Aspose.Imaging;
using Aspose.Imaging.Brushes;
using Aspose.Imaging.ImageOptions;
using Aspose.Imaging.Sources;
using Aspose.Imaging.FileFormats.Png;
using Aspose.Imaging.Graphics;
using Aspose.Imaging.Fonts;
using Aspose.Imaging.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Create rendering options and enable antialiasing
        ImageRenderingOptions renderingOptions = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            // Enable hinting for sharper text on low‑resolution images
            TextOptions = new TextOptions { UseHinting = true }
        };

        // 2️⃣ Define the font (size + style)
        Font font = new Font("Arial", 24, WebFontStyle.Bold | WebFontStyle.Italic);

        // 3️⃣ Prepare a bitmap with a white background
        int width = 800;
        int height = 200;
        using (var bitmap = new RasterImage(width, height, PixelFormat.Format24bppRgb))
        {
            bitmap.SaveOptions = new PngOptions { ColorType = PngColorType.Truecolor };
            bitmap.Fill(new SolidBrush(Color.White));

            // 4️⃣ Create a graphics object that respects our rendering options
            using (Graphics graphics = new Graphics(bitmap, renderingOptions))
            {
                // Position the text in the center of the image
                PointF location = new PointF(50, 80);
                graphics.DrawString("Antialiased Bold Italic Text", font, new SolidBrush(Color.Black), location);
            }

            // 5️⃣ Save the result
            string outputPath = "antialiased_text.png";
            bitmap.Save(outputPath);
            Console.WriteLine($"Image saved to {outputPath}");
        }
    }
}
```

### Explanation of each section

| Section | Why it matters |
|---------|----------------|
| **Rendering options** | Turning `UseAntialiasing` on guarantees smooth edges for both vector shapes and text. |
| **TextOptions.UseHinting** | Hinting improves legibility on low‑resolution outputs by adjusting glyph outlines. |
| **Font construction** | The `Font` constructor combines **set font size** and **set font style programmatically** in a single call. |
| **Graphics object** | Passing `renderingOptions` to `Graphics` ensures every drawing operation respects antialiasing and hinting. |
| **DrawString** | This method renders the text with the configured font, producing the final antialiased output. |
| **Saving** | The PNG format preserves the exact pixel data without additional compression artifacts. |

#### Expected output

Running the program creates **antialiased_text.png** that looks like this:

![Antialiased text example](https://example.com/antialiased_text.png "Antialiased text with custom font size and style – how to enable antialiasing")

The image shows crisp, bold‑italic Arial text rendered at 24 pt with smooth edges, confirming that **how to enable antialiasing** worked as intended.

## Common variations and edge cases

- **Different font families** – Replace `"Arial"` with any installed font name (e.g., `"Times New Roman"`). If the font isn’t available, Aspose.Imaging throws a `FontNotFoundException`.
- **Changing the font size** – Adjust the second argument of the `Font` constructor to any floating‑point value. Larger values increase readability but may require a larger bitmap.
- **Multiple styles** – Combine `WebFontStyle.Underline` with `Bold` and `Italic` using the `|` operator: `WebFontStyle.Bold | WebFontStyle.Underline`.
- **High‑DPI rendering** – For retina‑style output, increase the bitmap dimensions (e.g., 1600 × 400) while keeping the same font size; antialiasing will still produce smooth results.
- **Disabling antialiasing** – Set `renderingOptions.UseAntialiasing = false;` to compare the visual difference. The text will appear jagged, which is useful for debugging or performance testing.

## Pro tips

- **Cache the `Font` object** if you draw many strings in a loop; creating a new `Font` each iteration adds overhead.
- **Use `TextOptions.UseHinting` together with antialiasing** for the best trade‑off between sharpness and smoothness on low‑resolution images.
- **Validate the output file** by opening it in an image viewer that shows pixel‑level detail (e.g., Photoshop or GIMP). This helps you confirm that antialiasing truly took effect.

## Conclusion

You now know **how to enable antialiasing** in C# graphics, how to **set font size**, and how to **set font style programmatically** using `ImageRenderingOptions`. The complete example demonstrates a practical workflow that you can copy into your own projects, whether you are generating charts, creating UI thumbnails, or producing dynamic graphics for web services.

Next, you might explore **set font color programmatically**, add **gradient fills**, or render **vector shapes** with the same antialiasing settings. All of those topics build on the foundation covered here, so you’re well‑positioned to create high‑quality graphics entirely from code. Happy rendering!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Enable Antialiasing When Rendering HTML to PNG in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-when-rendering-html-to-png-in-c/)
- [How to enable antialiasing for HTML image rendering in C#](/html/english/net/rendering-html-documents/how-to-enable-antialiasing-for-html-image-rendering-in-c/)
- [How to Enable Antialiasing in Aspose HTML to PDF Conversion (C#)](/html/english/net/html-extensions-and-conversions/how-to-enable-antialiasing-in-aspose-html-to-pdf-conversion/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}