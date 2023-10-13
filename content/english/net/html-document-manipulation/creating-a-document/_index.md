---
title: Creating a Document in .NET with Aspose.HTML
linktitle: Creating a Document in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: Unleash the Power of Aspose.HTML for .NET. Learn to Create, Manipulate, and Optimize HTML and SVG Documents with Ease. Explore Step-By-Step Examples and FAQs.
type: docs
weight: 14
url: /net/html-document-manipulation/creating-a-document/
---

In the ever-evolving world of web development, staying ahead of the curve is essential. Aspose.HTML for .NET provides developers with a robust toolkit to work with HTML documents. Whether you're starting from scratch, loading from a file, pulling from a URL, or handling SVG documents, this library offers the versatility you need.

In this step-by-step guide, we will delve into the fundamentals of using Aspose.HTML for .NET, ensuring you're well-equipped to wield this powerful tool in your web development projects. Before we dive into the details, let's go over the prerequisites and the necessary namespaces to kickstart your journey.

## Prerequisites

To successfully follow this tutorial and harness the power of Aspose.HTML for .NET, you'll need the following prerequisites:

- A Windows machine with .NET Framework or .NET Core installed.
- A code editor like Visual Studio.
- Basic knowledge of C# programming.

Now that you have your prerequisites in place, let's get started.

## Importing Namespaces

Before you start using Aspose.HTML for .NET, you need to import the necessary namespaces. These namespaces contain classes and methods that are vital for working with HTML documents. Below is a list of namespaces you should import:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

With these namespaces imported, you are now ready to dive into the step-by-step examples.

## Creating an HTML Document from Scratch

### Step 1: Initialize an Empty HTML Document

```csharp
// Initialize an empty HTML Document.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Create a text element and add it to the document
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Save the document to disk.
    document.Save("document.html");
}
```

In this example, we start by creating an empty HTML document and adding a "Hello World!" text to it. We then save the document to a file.

## Creating an HTML Document from a File

### Step 1: Prepare a 'document.html' file

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Step 2: Load from a 'document.html' file

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Write the document content to the output stream.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Here, we prepare a file with "Hello World!" content and then load it as an HTML document. We print the document's content to the console.

## Creating an HTML Document from a URL

### Step 1: Load a document from a web page

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Write the document content to the output stream.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

In this example, we load an HTML document directly from a web page and display its content.

## Creating an HTML Document from a String

### Step 1: Prepare an HTML code

```csharp
var html_code = "<p>Hello World!</p>";
```

### Step 2: Initialize document from the string variable

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Save the document to disk.
    document.Save("document.html");
}
```

Here, we create an HTML document from a string variable and save it to a file.

## Creating an HTML Document from a MemoryStream

### Step 1: Create a memory stream object

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Write the HTML Code into the memory object
    sw.Write("<p>Hello World!</p>");
    // Set the position to the beginning
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Initialize document from the memory stream
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Save the document to disk.
        document.Save("document.html");
    }
}
```

In this example, we create an HTML document from a memory stream and save it to a file.

## Working with SVG Documents

### Step 1: Initialize the SVG Document from a string

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Write the document content to the output stream.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Here, we create and display an SVG document from a string.

## Loading an HTML Document Asynchronously

### Step 1: Create the instance of HTML Document

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Step 2: Subscribe to the 'ReadyStateChange' event

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    // Check the value of 'ReadyState' property.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Step 3: Navigate asynchronously at the specified Uri

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

In this example, we load an HTML document asynchronously and handle the 'ReadyStateChange' event to display the content when loading is complete.

## Handling the 'OnLoad' Event

### Step 1: Create the instance of HTML Document

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Step 2: Subscribe to the 'OnLoad' event

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Step 3: Navigate asynchronously at the specified Uri

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

This example demonstrates loading an HTML document asynchronously and handling the 'OnLoad' event to display the content upon completion.

## In Conclusion

In the dynamic world of web development, having the right tools at your disposal is crucial. Aspose.HTML for .NET equips you with the means to create, manipulate, and process HTML and SVG documents efficiently. This comprehensive guide has walked you through the essentials, ensuring that you can harness the power of Aspose.HTML for .NET in your projects.

## FAQ's

### Q1: What is Aspose.HTML for .NET?

A1: Aspose.HTML for .NET is a powerful .NET library that enables developers to work with HTML and SVG documents. It provides a wide range of features, from creating documents from scratch to parsing and manipulating existing HTML and SVG files.

### Q2: Can I use Aspose.HTML for .NET with .NET Core?

A2: Yes, Aspose.HTML for .NET is compatible with both .NET Framework and .NET Core, making it a versatile choice for modern .NET applications.

### Q3: Is Aspose.HTML for .NET suitable for web scraping and parsing?

A3: Absolutely! Aspose.HTML for .NET is an excellent choice for web scraping and parsing tasks, thanks to its ability to load HTML documents from URLs and strings. You can extract data, perform analysis, and more.

### Q4: How can I access support for Aspose.HTML for .NET?

A4: If you encounter any issues or have questions while using Aspose.HTML for .NET, you can visit the [Aspose Forum](https://forum.aspose.com/) for support and assistance from the community and Aspose experts.

### A5: Where can I find detailed documentation and download options?

A5: For comprehensive documentation and access to download options, you can refer to the following links:

- [Documentation](https://reference.aspose.com/html/net/)
- [Download](https://releases.aspose.com/html/net/)
- [Buy](https://purchase.aspose.com/buy)
- [Free Trial](https://releases.aspose.com/)
- [Temporary License](https://purchase.aspose.com/temporary-license/)
