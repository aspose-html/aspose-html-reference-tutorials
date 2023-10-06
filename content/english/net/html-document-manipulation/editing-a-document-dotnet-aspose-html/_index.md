---
title: Editing a Document in .NET with Aspose.HTML
linktitle: Editing a Document in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 15
url: /net/html-document-manipulation/editing-a-document-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void UsingDOM()
        {
            // Create the instance of HTML Document
            using (var document = new Aspose.Html.HTMLDocument())
            {
                // Create the style element and assign the green color for all elements with class-name equals 'gr'.
                var style = document.CreateElement("style");
                style.TextContent = ".gr { color: green }";
                // Find the document header element and append style element to the header
                var head = document.GetElementsByTagName("head").First();
                head.AppendChild(style);
                // Create the paragraph element with class-name 'gr'.
                var p = (Aspose.Html.HTMLParagraphElement)document.CreateElement("p");
                p.ClassName = "gr";
                // Create the text node
                var text = document.CreateTextNode("Hello World!!");
                // Append the text node to the paragraph
                p.AppendChild(text);
                // Append the paragraph to the document body element
                document.Body.AppendChild(p);
                // Create the instance of the PDF output device and render the document into this device
                using (var device = new Aspose.Html.Rendering.Pdf.PdfDevice("output.pdf"))
                    document.RenderTo(device);
            }
        }
        public static void UsingInnerOuterHTML()
        {
            // Create an instance of HTML Document
            using (var document = new Aspose.Html.HTMLDocument())
            {
                // Write the content of the HTML document into the console output
                Console.WriteLine(document.DocumentElement.OuterHTML); // output: <html><head></head><body></body></html>
                // Set content of the body element
                document.Body.InnerHTML = "<p>Hello World!!</p>";
                // Write the content of the HTML document into the console output
                Console.WriteLine(document.DocumentElement.OuterHTML); // output: <html><head></head><body><p>Hello World!!</p></body></html>
            }
        }
        public static void EditCSS()
        {
            // Create an instance of HTML Document with specified content
            var content = "<style>p { color: red; }</style><p>Hello World!</p>";
            using (var document = new Aspose.Html.HTMLDocument(content, "."))
            {
                // Find the paragraph element to inspect the styles
                var paragraph = (Aspose.Html.HTMLElement)document.GetElementsByTagName("p").First();
                // Get the reference to the IViewCSS interface. 
                var view = (Aspose.Html.Dom.Css.IViewCSS)document.Context.Window;
                // Get the calculated style value for the paragraph node
                var declaration = view.GetComputedStyle(paragraph);
                // Read the "color" property value out of the style declaration object
                System.Console.WriteLine(declaration.Color); // rgb(255, 0, 0)
                // Set the green color to the paragraph
                paragraph.Style.Color = "green";
                // Create the instance of the PDF output device and render the document into this device
                using (var device = new Aspose.Html.Rendering.Pdf.PdfDevice("output.pdf"))
                    document.RenderTo(device);
            }
        }
```
