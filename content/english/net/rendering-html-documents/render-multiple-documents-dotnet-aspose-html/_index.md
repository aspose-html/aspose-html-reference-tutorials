---
title: Render Multiple Documents in .NET with Aspose.HTML
linktitle: Render Multiple Documents in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 14
url: /net/rendering-html-documents/render-multiple-documents-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            string dataDir = RunExamples.GetDataDir_Data();
            using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
            using (var document2 = new Aspose.Html.HTMLDocument("<style>p { color: blue; }</style><p>my first paragraph</p>", @"c:\work\"))
            {
                using (HtmlRenderer renderer = new HtmlRenderer())
                using (XpsDevice device = new XpsDevice(dataDir + @"document_out.xps"))
                {
                    renderer.Render(device, document, document2);
                }
            }
            // ExEnd:1
        }
```
