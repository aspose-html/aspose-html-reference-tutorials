---
title: Merge HTML with XML in .NET with Aspose.HTML
linktitle: Merge HTML with XML in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 18
url: /net/html-document-manipulation/merge-html-with-xml-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            // The path to the documents directory
            string dataDir = "Your Data Directory";
            // HTML template document 
            HTMLDocument templateHtml = new HTMLDocument(dataDir + "HTMLTemplateforXML.html");
            //XML data for merging 
            TemplateData data = new TemplateData(dataDir + "XMLTemplate.xml");
            //Output file path 
            string templateOutput = dataDir + "HTMLTemplate_Output.html";
            //Merge HTML tempate with XML data
            Converter.ConvertTemplate(templateHtml, data, new TemplateLoadOptions(), templateOutput);
            // ExEnd:1
        }
```
