---
title: Convert SVG to PDF in .NET with Aspose.HTML
linktitle: Convert SVG to PDF in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 12
url: /net/canvas-and-image-manipulation/convert-svg-to-pdf-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            // The path to the documents directory
            string dataDir = RunExamples.GetDataDir_Data();
            // Source SVG document  
            SVGDocument svgDocument = new SVGDocument(dataDir + "input.svg");
            // Initialize pdfSaveOptions 
            PdfSaveOptions options = new PdfSaveOptions()
            {
                JpegQuality = 100
            };
            // Output file path 
            string outputFile = dataDir + "SVGtoPDF_Output.pdf";
            // Convert SVG to PDF 
            Converter.ConvertSVG(svgDocument, options, outputFile);
            // ExEnd:1
        }
```
