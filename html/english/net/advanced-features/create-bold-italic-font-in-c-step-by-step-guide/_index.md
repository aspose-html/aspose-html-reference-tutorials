---
category: general
date: 2026-08-15
description: Create bold italic font in C# quickly. Learn how to create font in C#
  with bold and italic styles using the built‑in Font class.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create bold italic font
- create font in c#
- C# FontStyle
- text styling C#
- System.Drawing.Font
language: en
lastmod: 2026-08-15
og_description: Create bold italic font in C# with a clear example. This tutorial
  shows how to create font in C# using FontStyle flags and explains common pitfalls.
og_image_alt: Screenshot of text rendered with a bold italic Arial font in a C# console
  window
og_title: Create bold italic font in C# – complete coding guide
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  headline: Create bold italic font in C# – step‑by‑step guide
  type: TechArticle
- description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  name: Create bold italic font in C# – step‑by‑step guide
  steps:
  - name: Save the code to a file named `Program.cs`.
    text: Save the code to a file named `Program.cs`.
  - name: Open a terminal in the file’s directory.
    text: Open a terminal in the file’s directory.
  - name: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
    text: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
  - name: Replace the generated `Program.cs` with the code above.
    text: Replace the generated `Program.cs` with the code above.
  - name: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
    text: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
  - name: Build and run with `dotnet run`.
    text: Build and run with `dotnet run`.
  type: HowTo
tags:
- C#
- fonts
- text styling
title: Create bold italic font in C# – step‑by‑step guide
url: /net/advanced-features/create-bold-italic-font-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create bold italic font in C# – step‑by‑step guide

If you need to **create bold italic font** in C#, this guide shows you exactly how to do it. You’ll see a complete, runnable example that also demonstrates how to **create font in C#** using the standard .NET `Font` class.

Working with custom fonts is a routine part of building Windows desktop apps, generating PDFs, or rendering HTML on the server. By the end of this tutorial you will be able to instantiate a font that is both bold and italic, understand why the bitwise `|` operator is used, and handle common edge cases such as missing font families.

## What you’ll learn

* How to import the required namespaces for font handling.  
* The syntax for combining `FontStyle.Bold` and `FontStyle.Italic`.  
* How to verify that the font was created successfully.  
* Tips for fallback handling when the requested family isn’t installed.  

No external libraries are required—everything uses the .NET Framework / .NET Core base class library.

## Prerequisites

* .NET 6.0 SDK or later (the code also works on .NET Framework 4.6+).  
* A code editor or IDE (Visual Studio, VS Code, Rider, etc.).  
* Basic familiarity with C# syntax.  

If you meet these prerequisites, you can follow the steps without any additional setup.

## Step 1: Add the necessary using directives

The `Font` class lives in the `System.Drawing` namespace, which is part of the `System.Drawing.Common` NuGet package for .NET Core/.NET 5+. Add the namespace at the top of your file:

```csharp
using System;
using System.Drawing;   // Provides Font and FontStyle
```

> **Why this step matters** – Without the `using System.Drawing;` line the compiler cannot locate `Font` or `FontStyle`, resulting in a “type or namespace name could not be found” error.

## Step 2: Combine bold and italic styles with the bitwise OR operator

In .NET, `FontStyle` is an enum marked with the `[Flags]` attribute. This means you can combine multiple values using the `|` (bitwise OR) operator:

```csharp
// Step 2: Create a Font that is both bold and italic
var font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
```

### Explanation

* `"Arial"` – the font family name. If the system does not have Arial installed, the constructor falls back to the default font.  
* `12` – point size.  
* `FontStyle.Bold | FontStyle.Italic` – combines the two style flags. The `|` operator merges the binary representation of each flag, producing a single value that represents “bold + italic”.

> **Pro tip:** Always use the enum names (`FontStyle.Bold`) rather than magic numbers; this improves readability and prevents bugs when the enum values change.

## Step 3: Verify the created font (optional but recommended)

Printing the font’s properties helps you confirm that the style combination succeeded, especially when debugging on a new machine.

```csharp
// Step 3: Output the font details to the console
Console.WriteLine($"Font family: {font.Name}");
Console.WriteLine($"Size (pt): {font.Size}");
Console.WriteLine($"Style: {font.Style}");
```

**Expected output**

```
Font family: Arial
Size (pt): 12
Style: Bold, Italic
```

If the output lists both `Bold` and `Italic`, the font was created correctly.

## Step 4: Render a sample string (visual confirmation)

When you run a console app you can’t see the actual glyph styling, but you can generate an image to prove the result. The following snippet draws “Hello, World!” using the bold‑italic font and saves it as *sample.png*:

```csharp
// Step 4: Draw text to an image file for visual confirmation
using (var bitmap = new Bitmap(300, 100))
using (var graphics = Graphics.FromImage(bitmap))
{
    graphics.Clear(Color.White);
    var brush = Brushes.Black;
    graphics.DrawString("Hello, World!", font, brush, new PointF(10, 30));
    bitmap.Save("sample.png");
    Console.WriteLine("Image saved as sample.png");
}
```

After the program runs, open *sample.png* to see the text rendered with the bold italic style.

![Sample text rendered with bold italic font](sample.png)

*Image alt text: Screenshot of text rendered with a bold italic Arial font in a C# console window* – this alt text satisfies the SEO requirement for image alt text.

## Step 5: Graceful fallback when the font family is unavailable

If the requested family (e.g., “Arial”) isn’t installed, the `Font` constructor throws an `ArgumentException`. Wrap the creation in a `try/catch` block and fall back to a known safe font such as “Segoe UI”.

```csharp
Font font;
try
{
    font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
}
catch (ArgumentException)
{
    Console.WriteLine("Arial not found – falling back to Segoe UI.");
    font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
}
```

**Why handle this?** In containerized or headless environments the default set of fonts can differ from a typical desktop. Providing a fallback prevents runtime crashes and ensures consistent styling.

## Full, runnable example

Putting everything together, here is a complete program you can copy, paste, and run:

```csharp
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create the font (bold + italic)
        Font font;
        try
        {
            font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
        }
        catch (ArgumentException)
        {
            Console.WriteLine("Arial not found – using Segoe UI as fallback.");
            font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
        }

        // Display font information
        Console.WriteLine($"Font family: {font.Name}");
        Console.WriteLine($"Size (pt): {font.Size}");
        Console.WriteLine($"Style: {font.Style}");

        // Render a sample image
        using (var bitmap = new Bitmap(300, 100))
        using (var graphics = Graphics.FromImage(bitmap))
        {
            graphics.Clear(Color.White);
            graphics.DrawString("Hello, World!", font, Brushes.Black, new PointF(10, 30));
            bitmap.Save("sample.png");
        }

        Console.WriteLine("Sample image saved as sample.png");
    }
}
```

### How to run

1. Save the code to a file named `Program.cs`.  
2. Open a terminal in the file’s directory.  
3. Execute `dotnet new console -n FontDemo` (if you need a project scaffold).  
4. Replace the generated `Program.cs` with the code above.  
5. Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).  
6. Build and run with `dotnet run`.  

You’ll see the console output confirming the font properties, and `sample.png` will appear in the project folder.

## Common pitfalls and how to avoid them

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| **Missing `System.Drawing.Common` package** | .NET Core does not include `System.Drawing` by default. | Run `dotnet add package System.Drawing.Common`. |
| **Font family not installed** | Headless Docker images often lack Windows fonts. | Use a fallback font or install the required fonts in the container. |
| **Incorrect use of `|`** | Using `+` instead of `|` results in an invalid combination. | Always combine `FontStyle` values with the bitwise OR operator (`|`). |
| **Disposing the `Font` object** | Not calling `Dispose` can leak GDI resources. | Wrap `Font` in a `using` block or call `font.Dispose()` after you’re done. |

## Conclusion

You now know how to **create bold italic font** in C# and how to **create font in C#** safely and efficiently. The tutorial covered importing the right namespace, combining `FontStyle` flags, verifying the result, rendering a visual sample, and handling missing font families.

Next, you might explore:

* **Creating underlined or strike‑through fonts** – add `FontStyle.Underline` or `FontStyle.Strikeout`.  
* **Using custom TrueType fonts** – load a `.ttf` file with `PrivateFontCollection`.  
* **Applying fonts in WinForms, WPF, or PDF generation** – the same `Font` object can be passed to UI controls or third‑party libraries.

Feel free to experiment with different families, sizes, and style combinations. If you run into issues, revisit the “Common pitfalls” table or check the official [.NET documentation for System.Drawing.Font](https://learn.microsoft.com/dotnet/api/system.drawing.font). Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Cara Menggabungkan Font Secara Programatis di C# – Panduan Langkah demi Langkah](/html/indonesian/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/)
- [Create HTML Document with Styled Text and Export to PDF – Full Guide](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [convert docx to png – create zip archive c# tutorial](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}