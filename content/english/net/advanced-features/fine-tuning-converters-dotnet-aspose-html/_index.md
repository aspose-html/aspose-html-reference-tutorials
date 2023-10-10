---
title: Fine-Tuning Converters in .NET with Aspose.HTML
linktitle: Fine-Tuning Converters in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: Learn how to convert HTML to PDF, XPS, and images with Aspose.HTML for .NET. Step-by-step tutorial with code examples and FAQs.
type: docs
weight: 16
url: /net/advanced-features/fine-tuning-converters-dotnet-aspose-html/
---

## Introduction

Aspose.HTML for .NET is a powerful library that allows developers to manipulate and convert HTML documents in various formats. Whether you need to convert HTML to PDF, XPS, or images, or perform other HTML-related tasks, Aspose.HTML provides a robust set of tools to help you get the job done.

In this tutorial, we will explore some essential features of Aspose.HTML for .NET and provide step-by-step explanations for each example. By the end of this tutorial, you will have a solid understanding of how to use Aspose.HTML for .NET in your .NET applications.

## Prerequisites

Before we dive into the examples, make sure you have the following prerequisites in place:

- Aspose.HTML for .NET: You should have the Aspose.HTML for .NET library installed. You can download it from the [download link](https://releases.aspose.com/html/net/).

- Temporary License (Optional): If you don't have a valid license, you can obtain a temporary license from [here](https://purchase.aspose.com/temporary-license/).

Now, let's explore some common use cases with Aspose.HTML for .NET.

## Import Namespaces

In your C# code, start by importing the necessary namespaces:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Convert HTML to PDF

### Step 1: Prepare HTML Code

```csharp
var code = @"<span>Hello World!!</span>";
```

### Step 2: Initialize HTML Document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Step 3: Create PDF Device and Specify Output File

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Step 4: Render HTML to PDF

```csharp
document.RenderTo(device);
```

This example converts an HTML snippet into a PDF document. You can customize the HTML code and output file as needed.

## Set Custom Page Size

### Step 1: Prepare HTML Code

```csharp
var code = @"<span>Hello World!!</span>";
```

### Step 2: Initialize HTML Document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Step 3: Create PDF Rendering Options

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Step 4: Create PDF Device and Specify Options and Output File

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Step 5: Render HTML to PDF

```csharp
document.RenderTo(device);
```

This example demonstrates how to set a custom page size for the resulting PDF document.

## Adjust Resolution

### Step 1: Prepare HTML Code and Save to File

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Step 2: Initialize HTML Document

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Step 3: Create PDF Rendering Options for Low-Resolution

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Step 4: Create PDF Device and Specify Options and Output File for Low-Resolution

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Step 5: Render HTML to PDF for Low-Resolution

```csharp
document.RenderTo(device);
```

### Step 6: Create PDF Rendering Options for High-Resolution

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Step 7: Create PDF Device and Specify Options and Output File for High-Resolution

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Step 8: Render HTML to PDF for High-Resolution

```csharp
document.RenderTo(device);
```

This example illustrates how to adjust the resolution when rendering HTML to PDF, considering both low and high-resolution screens.

## Specify Background Color

### Step 1: Prepare HTML Code and Save to File

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Step 2: Initialize HTML Document

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Step 3: Initialize PDF Rendering Options with Background Color

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Step 4: Create PDF Device and Specify Options and Output File

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Step 5: Render HTML to PDF

```csharp
document.RenderTo(device);
```

This example demonstrates how to specify a background color when converting HTML to PDF.

## Set Left and Right Page Sizes

### Step 1: Prepare HTML Code

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Step 2: Initialize HTML Document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Step 3: Create PDF Rendering Options with Left and Right Page Sizes

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Step 4: Create PDF Device and Specify Options and Output File

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Step 5: Render HTML to PDF

```csharp
document.RenderTo(device);
```

This example shows how to set different page sizes for the left and right pages when converting HTML to PDF.

## Adjust Page Size to Content

### Step 1: Prepare HTML Code

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Step 2: Initialize HTML Document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Step 3: Create PDF Rendering Options

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Step 4: Create PDF Device and Specify Options and Output File

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Step 5: Render HTML to PDF

```csharp
document.RenderTo(device);
```

This example demonstrates how to adjust the page size to the widest content when converting HTML to PDF.

## Specify PDF Permissions

### Step 1: Prepare HTML Code

```csharp
var code = @"<div>Hello World!!</div>";
```

### Step 2: Initialize HTML Document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Step 3: Create PDF Rendering Options with Permissions

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Step 4: Create PDF Device and Specify Options and Output File

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Step 5: Render HTML to PDF

```csharp
document.RenderTo(device);
```

This example demonstrates how to specify permissions and encryption when converting HTML to a protected PDF.

## Specify Image-Specific Options

### Step 1: Prepare HTML Code

```csharp
var code = @"<div>Hello World!!</div>";
```

### Step 2: Initialize HTML Document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Step 3: Create Image Rendering Options

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Step 4: Create Image Device and Specify Options and Output File

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Step 5: Render HTML to Image

```csharp
document.RenderTo(device);
```

This example demonstrates how to convert HTML to an image with specific rendering options, such as format, resolution, and smoothing mode.

## Specify XPS Rendering Options

### Step 1: Prepare HTML Code

```csharp
var code = @"<span>Hello World!!</span>";
```

### Step 2: Initialize HTML Document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Step 3: Create XPS Rendering Options with Page Size

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Step 4: Create XPS Device and Specify Options and Output File

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Step 5: Render HTML to XPS

```csharp
document.RenderTo(device);
```

This example shows how to convert HTML to XPS with custom page size and rendering options.

## Combine Multiple HTML Documents into PDF

### Step 1: Prepare HTML Code for Multiple Documents

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Step 2: Create HTML Documents to Merge

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Step 3: Initialize HTML Renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Step 4: Create PDF Device for Merged Output

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Step 5: Merge HTML Documents into PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

This example demonstrates how to combine multiple HTML documents into a single PDF file using Aspose.HTML for .NET.

## Set Rendering Timeout

### Step 1: Prepare HTML Code with JavaScript

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Step 2: Initialize HTML Document

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Step 3: Initialize HTML Renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Step 4: Create PDF Device and Set Rendering Timeout

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Step 5: Render HTML to PDF with Timeout

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

This example demonstrates how to set a rendering timeout when converting HTML to PDF, which can be useful when dealing with dynamic content or long-running scripts.

## Conclusion

Aspose.HTML for .NET is a versatile library that empowers developers to work with HTML documents efficiently. In this tutorial, we covered various examples, from basic HTML to PDF conversions to more advanced features like custom page sizes, resolutions, and permissions. By following these examples, you can harness the full potential of Aspose.HTML for .NET in your .NET applications.

If you have any questions or need further assistance, don't hesitate to visit the [Aspose.HTML Forum](https://forum.aspose.com/) for support and guidance.

## FAQ's

### Q1. What is Aspose.HTML for .NET?
   
A1: Aspose.HTML for .NET is a .NET library that enables developers to manipulate and convert HTML documents programmatically. It offers a wide range of features for working with HTML content, including HTML to PDF, XPS, and image conversion, as well as advanced rendering options.

### Q2. Where can I download Aspose.HTML for .NET?

A2: You can download Aspose.HTML for .NET from the [download link](https://releases.aspose.com/html/net/).

### Q3. Do I need a license to use Aspose.HTML for .NET?

A3: While you can use Aspose.HTML for .NET without a license, it's recommended to obtain a license for production use to unlock all the features and remove any watermarks or limitations.

### Q4. How can I protect my PDF files generated with Aspose.HTML for .NET?

A4: You can specify PDF permissions and encryption settings when rendering HTML to PDF using Aspose.HTML for .NET. This allows you to control who can access and modify the resulting PDF files.

### Q5. Can I convert HTML to other formats like XPS or images?

A5: Yes, Aspose.HTML for .NET supports converting HTML to various formats, including PDF, XPS, and images (e.g., JPEG). You can customize the conversion settings to meet your specific requirements.
