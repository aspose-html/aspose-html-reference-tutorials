---
title: Convert HTML to XPS in .NET with Aspose.HTML
linktitle: Convert HTML to XPS in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 22
url: /net/html-extensions-and-conversions/convert-html-to-xps-dotnet-aspose-html/
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
            // Initialize XpsSaveOptions 
            XpsSaveOptions options = new XpsSaveOptions
            {
                BackgroundColor = System.Drawing.Color.Cyan
            };
            // Output file path 
            string outputFile = dataDir + "input.xps";
            // Convert HTML to XPS
            Converter.ConvertHTML(htmlDocument, options, outputFile);
            // ExEnd:1         
        }
```
