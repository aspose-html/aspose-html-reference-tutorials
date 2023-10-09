---
title: Convert HTML to PDF in .NET with Aspose.HTML
linktitle: Convert HTML to PDF in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 10
url: /net/html-extensions-and-conversions/convert-html-to-pdf-dotnet-aspose-html/
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
            // Initialize PdfSaveOptions 
            PdfSaveOptions options = new PdfSaveOptions
            {
                JpegQuality = 100
            };
            // Output file path 
            string outputPDF = dataDir + "HTMLtoPDF_Output.pdf";
            // Convert HTML to PDF
            Converter.ConvertHTML(htmlDocument, options, outputPDF);
            // ExEnd:1
        }
```
