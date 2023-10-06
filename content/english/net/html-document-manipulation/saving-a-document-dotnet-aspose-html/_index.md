---
title: Saving a Document in .NET with Aspose.HTML
linktitle: Saving a Document in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 16
url: /net/html-document-manipulation/saving-a-document-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void HTMLToFile()
        {
            // Initialize an empty HTML Document.
            using (var document = new Aspose.Html.HTMLDocument())
            {
                // Create a text element and add it to the document
                var text = document.CreateTextNode("Hello World!");
                document.Body.AppendChild(text);
                // Save the HTML to the file on disk.
                document.Save("document.html");
            }
        }
        public static void HTMLWithoutLinkedFile()
        {
            // Prepare a simple HTML file with a linked document.
            System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                                         "<a href='linked.html'>linked file</a>");
            // Prepare a simple linked HTML file
            System.IO.File.WriteAllText("linked.html", "<p>Hello linked file!</p>");
            // Load 'document.html' into memory
            using (var document = new Aspose.Html.HTMLDocument("document.html"))
            {
                // Create Save Options instance
                var options = new Aspose.Html.Saving.HTMLSaveOptions();
                // The following line with value '0' cut off all other linked HTML-files while saving this instance.
                // If you remove this line or change value to the '1', the 'linked.html' file will be saved as well to the output folder.
                options.ResourceHandlingOptions.MaxHandlingDepth = 1;
                // Save the document
                document.Save(@".\html-to-file-example\document.html", options);
            }
        }
        public static void HTMLToMHTML()
        {
            // Prepare a simple HTML file with a linked document.
            System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                                         "<a href='linked.html'>linked file</a>");
            // Prepare a simple linked HTML file
            System.IO.File.WriteAllText("linked.html", "<p>Hello linked file!</p>");
            // Load 'document.html' into memory
            using (var document = new Aspose.Html.HTMLDocument("document.html"))
            {
                // Save the document
                document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
            }
        }
        public static void HTMLToMarkdown()
        {
            // Prepare an HTML code
            var html_code = "<H2>Hello World!</H2>";
            // Initialize document from the string variable
            using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
            {
                // Save the document as a Markdown file.
                document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
            }
        }
        public static void SVGToFile()
        {
            // Prepare an SVG code
            var code = @"
                <svg xmlns='http://www.w3.org/2000/svg' height='80' width='300'>
                    <g fill='none'>
                        <path stroke='red' d='M5 20 l215 0' />
                        <path stroke='black' d='M5 40 l215 0' />
                        <path stroke='blue' d='M5 60 l215 0' />
                    </g>
                </svg>";
            // Initialize a SVG instance from the content string
            using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
            {
                // Save the SVG file to the disk
                document.Save("document.svg");
            }
        }
```
