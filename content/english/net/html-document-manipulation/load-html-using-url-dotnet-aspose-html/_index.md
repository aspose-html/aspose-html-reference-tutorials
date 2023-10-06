---
title: Load HTML Using URL in .NET with Aspose.HTML
linktitle: Load HTML Using URL in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 13
url: /net/html-document-manipulation/load-html-using-url-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:LoadHtmlUsingURL
            String InputHtml = "http://aspose.com/";
            // Load HTML file using Url instance
            Aspose.Html.HTMLDocument document = new Aspose.Html.HTMLDocument(new Aspose.Html.Url(InputHtml));
            // Print inner HTML of file to console
            Console.WriteLine(document.Body.InnerHTML);
            // ExEnd:LoadHtmlUsingURL           
        }
```
