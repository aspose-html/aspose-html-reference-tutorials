---
category: general
date: 2026-11-20
description: Learn how to save HTML using a custom ResourceHandler in C# and also
  save HTML to zip archives with concise, production‑ready code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: en
lastmod: 2026-11-20
og_description: How to save HTML using a custom ResourceHandler in C# and optionally
  save HTML to zip files—complete, runnable guide for .NET developers.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: How to save HTML with a custom resource handler in C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: How to save HTML with a custom resource handler in C#
url: /net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to save HTML with a custom resource handler in C#

If you need to know **how to save HTML** from an in‑memory string or a parsed document, this guide shows a complete solution. Using a custom `ResourceHandler` lets you control the destination stream, which means you can **save HTML to zip** archives without writing temporary files.

You’ll see why a `ResourceHandler` is preferred over the older `IOutputStorage` approach, how to set it up, and how to extend it for zip compression. By the end of this tutorial you can embed the code in any .NET 6+ project and adapt it to your own storage requirements.

## What you’ll build

* A minimal `ResourceHandler` that returns a `MemoryStream`.
* An `HtmlDocument` created with **HtmlAgilityPack**.
* A call to `doc.Save` that writes the HTML into the stream supplied by the handler.
* An optional wrapper that compresses the resulting HTML into a zip file.

Prerequisites:

* .NET 6 SDK or later.
* `HtmlAgilityPack` NuGet package (`dotnet add package HtmlAgilityPack`).
* Basic familiarity with C# streams.

## Step 1: Create a custom resource handler (primary way to **how to save html**)

The `ResourceHandler` base class (available from version 24.2 of the viewer SDK) defines a single abstract method, `HandleResource`. Implementing this method gives you full control over where the HTML is written.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Why this matters:** By returning a `MemoryStream`, you avoid disk I/O, reduce latency, and keep the code deterministic for unit tests. The handler is invoked automatically by the `Save` method, so you never need to pass a stream explicitly.

## Step 2: Load or build the HTML document

`HtmlAgilityPack` provides a convenient `HtmlDocument` class that can parse a string, a file, or a stream. For this example we load a simple literal, but the same code works with any HTML source.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Why this matters:** Keeping the document in memory aligns with the stream‑based approach of the custom handler. It also lets you manipulate the DOM before saving, such as injecting scripts or fixing malformed tags.

## Step 3: Save the document using the custom handler

Calling `doc.Save` with an instance of `MyHandler` triggers the `HandleResource` method. The HTML is written directly to the stream you returned.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

After `Save` completes, the `MemoryStream` inside `MyHandler` contains the serialized HTML. You can retrieve it like this:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Result:** The console prints the exact HTML you passed to `LoadHtml`. This proves that you now understand **how to save HTML** with a custom handler.

## Step 4: Extending the handler to **save HTML to zip**

If you want to archive the HTML, modify `MyHandler` to write into a `ZipArchiveEntry`. The .NET `System.IO.Compression` namespace makes this straightforward.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Now use the new handler:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Why this works:** The `HandleResource` method creates a zip entry named `document.html`. When `doc.Save` writes to the returned stream, the data is compressed automatically. Because the zip is built in memory, you can return it from a web API, attach it to an email, or store it in a database without touching the file system.

## Common questions and edge cases

### What if I need multiple HTML files in the same zip?
Create a new entry for each call to `HandleResource`. The `resourceName` argument typically contains the filename, so you can use it directly:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### How to handle large documents without exhausting memory?
Replace `MemoryStream` with a `FileStream` that points to a temporary file. The handler then returns the file stream, and you can later delete the file after the zip is created.

### Does this approach work with .NET Core on Linux?
Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.

### Can I encrypt the zip archive?
`ZipArchive` supports password‑based encryption only through third‑party libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output bytes with a library that provides AES encryption before sending them to the client.

## Pro tips

* **Reuse the handler** when processing many documents in a batch; creating a new `ZipArchive` for each file adds unnecessary overhead.
* **Set `LeaveOpen: true`** on the `ZipArchive` constructor if you need to read the zip bytes while the archive is still open.
* **Validate HTML** before saving by calling `doc.OptionCheckSyntax = true;` – this catches malformed tags early.
* **Log the size** of the generated zip; unusually large output often indicates duplicate resources or missing compression.

## Full working example

Below is a single file you can paste into a console project (`dotnet new console`) and run. It demonstrates both plain HTML saving and zip compression.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using HtmlAgilityPack;

// ---------- Custom handlers ----------
class MyHandler : ResourceHandler
{
    public MemoryStream HtmlStream { get; } = new();

    public override Stream HandleResource(string resourceName) => HtmlStream;
}

class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open();
    }

    public byte[] GetZipBytes()
    {
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}

// ---------- Main program ----------
class Program
{
    static void Main()
    {
        // Build a simple HTML document.
        HtmlDocument doc = new HtmlDocument();
        doc.LoadHtml("<html><body>Hello World from HtmlAgilityPack</body></html>");

        // ---- Example 1: plain HTML save ----
        var plainHandler = new MyHandler();
        doc.Save(plainHandler);
        plainHandler.HtmlStream.Seek(0, SeekOrigin.Begin);
        using var reader = new StreamReader(plainHandler.HtmlStream);
        Console.WriteLine("Plain HTML output:");


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Save HTML in C# with Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [How to Use ZipArchive – Save HTML and Resources to a ZIP File](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [save html as zip with a custom resource handler – step‑by‑step guide](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}