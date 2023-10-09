---
title: Convert HTML to JPEG in .NET with Aspose.HTML
linktitle: Convert HTML to JPEG in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 17
url: /net/html-extensions-and-conversions/convert-html-to-jpeg-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            // The path to the documents directory
            string dataDir = "Your Data Directory";
            // Source HTML document  
            HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html");
            // Initialize ImageSaveOptions 
            ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
            // Output file path 
            string outputFile = dataDir + "HTMLtoJPEG_Output.jpeg";
            // Convert HTML to JPEG
            Converter.ConvertHTML(htmlDocument, options, outputFile);
            // ExEnd:1           
        }
```
