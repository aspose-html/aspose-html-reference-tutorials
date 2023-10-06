---
title: Convert SVG to Image in .NET with Aspose.HTML
linktitle: Convert SVG to Image in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 11
url: /net/canvas-and-image-manipulation/convert-svg-to-image-dotnet-aspose-html/
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
            // Initialize ImageSaveOptions 
            ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
            // Output file path 
            string outputFile = dataDir + "SVGtoImage_Output.jpeg";
            // Convert SVG to Image
            Converter.ConvertSVG(svgDocument, options, outputFile);
            // ExEnd:1           
        }
```
