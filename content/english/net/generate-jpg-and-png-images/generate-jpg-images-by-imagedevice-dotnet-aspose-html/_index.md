---
title: Generate JPG Images by ImageDevice in .NET with Aspose.HTML
linktitle: Generate JPG Images by ImageDevice in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 10
url: /net/generate-jpg-and-png-images/generate-jpg-images-by-imagedevice-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            string dataDir = RunExamples.GetDataDir_Data();
            using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
            {
                // Initialize rendering optionss and set jpeg as output format
                var options = new ImageRenderingOptions(ImageFormat.Jpeg);
                // Set the size and margin property for all pages.
                options.PageSetup.AnyPage = new Page(new Size(500, 500), new Margin(50, 50, 50, 50));
                //  If the document has an element which size is bigger than predefined by user page size output pages will be will be adjusted.
                options.PageSetup.AdjustToWidestPage = true;
                using (ImageDevice device = new ImageDevice(options, dataDir + @"document_out.jpg"))
                {
                    document.RenderTo(device);
                }
            }
            // ExEnd:1
        }
```
