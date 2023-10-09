---
title: Convert HTML to MHTML in .NET with Aspose.HTML
linktitle: Convert HTML to MHTML in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 19
url: /net/html-extensions-and-conversions/convert-html-to-mhtml-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            // The path to the documents directory
            string dataDir = "Your Data Directory";
            // Source HTML Document 
            HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html");
            // Initialize MHTMLSaveOptions
            MHTMLSaveOptions options = new MHTMLSaveOptions();
            // Set the resource handling rules
            options.ResourceHandlingOptions.MaxHandlingDepth = 1;
            // Output file path 
            string outputPDF = dataDir + "HTMLtoMHTML_Output.mht";
            // Convert HTML to MHTML
            Converter.ConvertHTML(htmlDocument, options, outputPDF);
            // ExEnd:1          
        }
```
