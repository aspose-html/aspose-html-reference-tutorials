---
title: Convert SVG to XPS in .NET with Aspose.HTML
linktitle: Convert SVG to XPS in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 13
url: /net/canvas-and-image-manipulation/convert-svg-to-xps-dotnet-aspose-html/
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
            // Initialize XpsSaveOptions 
            XpsSaveOptions options = new XpsSaveOptions()
            {
                BackgroundColor = System.Drawing.Color.Cyan
            };
            // Output file path 
            string outputFile = dataDir + "SVGtoXPS_Output.xps";
            // Convert SVG to XPS 
            Converter.ConvertSVG(svgDocument, options, outputFile);
            // ExEnd:1   
        }
```
