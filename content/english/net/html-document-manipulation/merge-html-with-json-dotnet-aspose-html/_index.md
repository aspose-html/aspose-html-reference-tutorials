---
title: Merge HTML with Json in .NET with Aspose.HTML
linktitle: Merge HTML with Json in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 17
url: /net/html-document-manipulation/merge-html-with-json-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            // The path to the documents directory
            string dataDir = "Your Data Directory";
            // HTML template document 
            HTMLDocument templateHtml = new HTMLDocument(dataDir + "HTMLTemplateForJson.html");
            //XML data for merging 
            TemplateData data = new TemplateData(dataDir + "JsonTemplate.json");
            //Output file path 
            string templateOutput = dataDir + "MergeHTMLWithJson_Output.html";
            //Merge HTML tempate with XML data
            Converter.ConvertTemplate(templateHtml, data, new TemplateLoadOptions(), templateOutput);
            // ExEnd:1
        }
```
