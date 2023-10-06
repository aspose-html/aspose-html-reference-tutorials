---
title: Manipulating Canvas in .NET with Aspose.HTML
linktitle: Manipulating Canvas in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 10
url: /net/canvas-and-image-manipulation/manipulating-canvas-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:ManipulateCanvas
            // The path to the documents directory.
            string dataDir = RunExamples.GetDataDir_Data();
            // Create an empty document
            using (HTMLDocument document = new HTMLDocument())
            {
                // Create a Canvas element
                var canvas = (HTMLCanvasElement)document.CreateElement("canvas");
                // Set the canvas size
                canvas.Width = 300;
                canvas.Height = 150;
                // Append created element to the document
                document.Body.AppendChild(canvas);
                // Initialize a canvas 2D context
                var context = (ICanvasRenderingContext2D)canvas.GetContext("2d");
                // Prepare a gradient brush
                var gradient = context.CreateLinearGradient(0, 0, canvas.Width, 0);
                gradient.AddColorStop(0, "magenta");
                gradient.AddColorStop(0.5, "blue");
                gradient.AddColorStop(1.0, "red");
                // Set the previously prepared brush to the fill and stroke properties
                context.FillStyle = gradient;
                context.StrokeStyle = gradient;
                // Fill a rectange
                context.FillRect(0, 95, 300, 20);
                // Write a text
                context.FillText("Hello World!", 10, 90, 500);
                // Create an instance of HTML renderer and XPS output device
                using (var renderer = new HtmlRenderer())
                using (var device = new XpsDevice(dataDir + "canvas.xps"))
                {
                    //  Render the document to the specified device
                    renderer.Render(device, document);
                }
            }
            // ExEnd:ManipulateCanvas
        }
```
