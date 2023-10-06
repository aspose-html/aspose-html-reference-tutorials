---
title: Rendering Timeout in .NET with Aspose.HTML
linktitle: Rendering Timeout in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 12
url: /net/rendering-html-documents/rendering-timeout-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:RenderingTimeout
            // The path to the documents directory.
            string dataDir = RunExamples.GetDataDir_Data();
            // Create an instance of the HTML document
            using (var document = new Aspose.Html.HTMLDocument())
            {
                // Async loading of the external html file
                document.Navigate(dataDir + "input.html");
                // Create a renderer and output device 
                using (HtmlRenderer renderer = new HtmlRenderer())
                using (ImageDevice device = new ImageDevice(dataDir + @"document.png"))
                {
                    // Delay rendering for 5 seconds
                    // Note: document will be rendered into device if there are no scripts or any internal tasks to execute
                    renderer.Render(device, TimeSpan.FromSeconds(5), document);
                }
            }
            // ExEnd:RenderingTimeout
        }
        public static void IndefiniteTimeout()
        {
            // ExStart:IndefiniteTimeout
            // The path to the documents directory.
            string dataDir = RunExamples.GetDataDir_Data();
            // Create an instance of the HTML document
            using (var document = new Aspose.Html.HTMLDocument())
            {
                // Async loading of the external html file
                document.Navigate( dataDir + "input.html");
                // Create a renderer and output device 
                using (HtmlRenderer renderer = new HtmlRenderer())
                using (ImageDevice device = new ImageDevice(dataDir + @"document.png"))
                {
                    // Delay the rendering indefinitely until there are no scripts or any other internal tasks to execute
                    renderer.Render(device, -1, document);
                }
            }
            // ExEnd:IndefiniteTimeout
        }
```
