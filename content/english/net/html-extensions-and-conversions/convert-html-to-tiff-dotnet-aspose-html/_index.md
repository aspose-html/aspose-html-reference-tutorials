---
title: Convert HTML to TIFF in .NET with Aspose.HTML
linktitle: Convert HTML to TIFF in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 21
url: /net/html-extensions-and-conversions/convert-html-to-tiff-dotnet-aspose-html/
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
            ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Tiff);
            // Output file path 
            string outputFile = dataDir + "HTMLtoPNG_Output.tif";
            // Convert HTML to TIFF
            Converter.ConvertHTML(htmlDocument, options, outputFile);
            // ExEnd:1                    
        }
```
