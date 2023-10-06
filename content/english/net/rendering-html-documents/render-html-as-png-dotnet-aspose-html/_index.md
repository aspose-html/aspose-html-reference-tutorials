---
title: Render HTML as PNG in .NET with Aspose.HTML
linktitle: Render HTML as PNG in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 10
url: /net/rendering-html-documents/render-html-as-png-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            string dataDir = RunExamples.GetDataDir_Data();
            using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
            {
                using (HtmlRenderer renderer = new HtmlRenderer())
                using (ImageDevice device = new ImageDevice(dataDir + @"document_out.png"))
                {
                    renderer.Render(device, document);
                }
            }
            // ExEnd:1
        }
```
