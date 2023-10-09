---
title: Convert HTML to DOC and DOCX in .NET with Aspose.HTML
linktitle: Convert HTML to DOC and DOCX in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 15
url: /net/html-extensions-and-conversions/convert-html-to-doc-docx-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:HTMLtoDOCandDOCX
            // The path to the documents directory
            string dataDir = "Your Data Directory";
            // Source HTML document  
            HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html");
            DocSaveOptions options = new DocSaveOptions();
            options.DocumentFormat = Rendering.Doc.DocumentFormat.DOCX;
            Converter.ConvertHTML(htmlDocument, options, dataDir + "HTMLtoDOCX_out.docx");
            // ExEnd:HTMLtoDOCandDOCX
        }
```
