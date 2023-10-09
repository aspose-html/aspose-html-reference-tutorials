---
title: Generate XPS Documents by XpsDevice in .NET with Aspose.HTML
linktitle: Generate XPS Documents by XpsDevice in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 19
url: /net/html-document-manipulation/generate-xps-documents-by-xpsdevice-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            string dataDir = "Your Data Directory";
            using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
            {
                using (XpsDevice device = new XpsDevice(new XpsRenderingOptions()
                {
                    PageSetup =
                    {
                        AnyPage = new Page(new Size(500, 500), new Margin(50, 50, 50, 50))
                    }
                }, dataDir + @"document_out.xps"))
                {
                    document.RenderTo(device);
                }
            }
            // ExEnd:1
        }
```
