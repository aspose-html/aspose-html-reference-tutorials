---
title: Render MHTML as XPS in .NET with Aspose.HTML
linktitle: Render MHTML as XPS in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 13
url: /net/rendering-html-documents/render-mhtml-as-xps-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            string dataDir = "Your Data Directory";
            using (var fs = File.OpenRead(dataDir + "document.mht"))
            using (var device = new Aspose.Html.Rendering.Xps.XpsDevice(dataDir + "document_out.xps"))
            using (var renderer = new Aspose.Html.Rendering.MhtmlRenderer())
            {
                renderer.Render(device, fs);
            }
            // ExEnd:1
        }
```
