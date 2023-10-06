---
title: Load HTML Using a Remote Server in .NET with Aspose.HTML
linktitle: Load HTML Using a Remote Server in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 12
url: /net/html-document-manipulation/load-html-using-remote-server-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:LoadHtmlUsingRemoteServer
            Aspose.Html.HTMLDocument document = new Aspose.Html.HTMLDocument(new Aspose.Html.Url(@"https://www.w3.org/TR/html5/"));
            // Read children nodes and get length information
            if (document.Body.ChildNodes.Length == 0)
                Console.WriteLine("No ChildNodes found...");
            // Print Document URI to console. As per information above, it has to be https://www.w3.org/TR/html5/
            Console.WriteLine("Print Document URI = " + document.DocumentURI);
            // Print domain name for remote HTML
            Console.WriteLine("Domain Name = " + document.Domain);
            // ExEnd:LoadHtmlUsingRemoteServer           
        }
```
