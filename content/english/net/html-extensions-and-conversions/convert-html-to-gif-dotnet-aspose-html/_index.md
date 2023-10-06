---
title: Convert HTML to GIF in .NET with Aspose.HTML
linktitle: Convert HTML to GIF in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 16
url: /net/html-extensions-and-conversions/convert-html-to-gif-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            // The path to the documents directory
            string dataDir = RunExamples.GetDataDir_Data();
            // Source HTML document  
            HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html");
            // Initialize ImageSaveOptions 
            ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Gif);
            // Output file path 
            string outputFile = dataDir + "HTMLtoGIF_Output.gif";
            // Convert HTML to GIF
            Converter.ConvertHTML(htmlDocument, options, outputFile);
            // ExEnd:1           
        }
```
