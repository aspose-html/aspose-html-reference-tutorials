---
title: Render SVG Doc as PNG in .NET with Aspose.HTML
linktitle: Render SVG Doc as PNG in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 15
url: /net/rendering-html-documents/render-svg-doc-as-png-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            string dataDir = RunExamples.GetDataDir_Data();
            using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", @"c:\work\"))
            {
                using (SvgRenderer renderer = new SvgRenderer())
                using (ImageDevice device = new ImageDevice(dataDir + @"document_out.png"))
                {
                    renderer.Render(device, document);
                }
            }
            // ExEnd:1
        }
```
