---
title: Convert EPUB to XPS in .NET with Aspose.HTML
linktitle: Convert EPUB to XPS in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 13
url: /net/html-extensions-and-conversions/convert-epub-to-xps-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void WithASingleLine()
        {
            string dataDir = "Your Data Directory";
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Call the ConvertEPUB method to convert the EPUB to XPS.
                Aspose.Html.Converters.Converter.ConvertEPUB(stream, new Aspose.Html.Saving.XpsSaveOptions(), "output.xps");
            }
        }
        public static void ConvertEPUBFileToXPS()
        {
            string dataDir = "Your Data Directory";
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Create an instance of XpsSaveOptions.
                var options = new Aspose.Html.Saving.XpsSaveOptions();
                // Call the ConvertEPUB method to convert the EPUB to XPS.
                Aspose.Html.Converters.Converter.ConvertEPUB(stream, options, "output.xps");
            }
        }
        public static void SpecifyXpsSaveOptions()
        {
            string dataDir = "Your Data Directory";
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Create an instance of the XpsSaveOptions with a custom page-size and a background-color.
                var options = new Aspose.Html.Saving.XpsSaveOptions()
                {
                    PageSetup =
                    {
                        AnyPage = new Aspose.Html.Drawing.Page()
                        {
                            Size = new Aspose.Html.Drawing.Size(Aspose.Html.Drawing.Length.FromPixels(3000), Aspose.Html.Drawing.Length.FromPixels(1000))
                        }
                    },
                    BackgroundColor = System.Drawing.Color.AliceBlue,
                };
                // Call the ConvertEPUB method to convert the EPUB to XPS.
                Aspose.Html.Converters.Converter.ConvertEPUB(stream, options, "output.xps");
            }
        }
        public static void SpecifyCustomStreamProvider()
        {
            string dataDir = "Your Data Directory";
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Create an instance of MemoryStreamProvider
                using (var streamProvider = new MemoryStreamProvider())
                {
                    // Convert EPUB to XPS by using the MemoryStreamProvider
                    Aspose.Html.Converters.Converter.ConvertEPUB(stream, new Aspose.Html.Saving.XpsSaveOptions(), streamProvider);
                    // Get access to the memory stream that contains the resulted data
                    var memory = streamProvider.Streams.First();
                    memory.Seek(0, System.IO.SeekOrigin.Begin);
                    // Flush the result data to the output file
                    using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
                    {
                        memory.CopyTo(fs);
                    }
                }
            }
        }
        class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // List of MemoryStream objects created during the document rendering
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // This method is called when the only one output stream is required, for instance for XPS, PDF or TIFF formats.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // This method is called when the creation of multiple output streams are required. For instance during the rendering HTML to list of the image files (JPG, PNG, etc.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                //  Here You can release the stream filled with data and, for instance, flush it to the hard-drive
            }
            public void Dispose()
            {
                // Releasing resources
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
