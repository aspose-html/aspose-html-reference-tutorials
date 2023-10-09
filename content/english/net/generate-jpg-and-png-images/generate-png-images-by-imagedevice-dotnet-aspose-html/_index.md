---
title: Generate PNG Images by ImageDevice in .NET with Aspose.HTML
linktitle: Generate PNG Images by ImageDevice in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 11
url: /net/generate-jpg-and-png-images/generate-png-images-by-imagedevice-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            string dataDir = "Your Data Directory";
            using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
            {
                using (ImageDevice device = new ImageDevice(dataDir + @"document_out.png"))
                {
                    document.RenderTo(device);
                }
            }
            // ExEnd:1
        }
```
