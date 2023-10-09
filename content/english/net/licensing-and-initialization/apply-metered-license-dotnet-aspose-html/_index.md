---
title: Apply Metered License in .NET with Aspose.HTML
linktitle: Apply Metered License in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 10
url: /net/licensing-and-initialization/apply-metered-license-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:ApplyMeteredLicense
            // The path to the documents directory
            string dataDir = "Your Data Directory";
            // set metered public and private keys
            Aspose.Html.Metered metered = new Aspose.Html.Metered();
            // Access the setMeteredKey property and pass public and private keys as parameters
            metered.SetMeteredKey("*****", "*****");
            // Load the document from disk.
            HTMLDocument document = new HTMLDocument(dataDir + "input.html");
            // Print inner HTML of file to console
            Console.WriteLine(document.Body.InnerHTML);
            // ExEnd:ApplyMeteredLicense 
        }
```
