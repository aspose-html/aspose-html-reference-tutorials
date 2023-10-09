---
title: Convert HTML to BMP in .NET with Aspose.HTML
linktitle: Convert HTML to BMP in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 14
url: /net/html-extensions-and-conversions/convert-html-to-bmp-dotnet-aspose-html/
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
            ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Bmp);
            // Output file path 
            string outputFile = dataDir + "HTMLtoBMP_Output.bmp";
            // Convert HTML to BMP
            Converter.ConvertHTML(htmlDocument, options, outputFile);
            // ExEnd:1           
        }
```
