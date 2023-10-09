---
title: Create Stream Provider in .NET with Aspose.HTML
linktitle: Create Stream Provider in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 11
url: /net/advanced-features/create-stream-provider-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            // The path to the documents directory
            string dataDir = "Your Data Directory";
            // Create a custom StreamProvider based on ICreateStreamProvider interface 
            using (MemoryStreamProvider streamProvider = new MemoryStreamProvider())
            {
                // Create a simple HTML document
                using (HTMLDocument document = new HTMLDocument())
                {
                    // Add your first 'hello world' to the document.
                    document.Body.AppendChild(document.CreateTextNode("Hello world!!!"));
                    // Convert HTML document to XPS by using the custom StreamProvider
                    Aspose.Html.Converters.Converter.ConvertHTML(document, new XpsSaveOptions(), streamProvider);
                    // Get access to the memory stream that contains the result data
                    var memory = streamProvider.Streams[0];
                    memory.Seek(0, SeekOrigin.Begin);
                    // Flush the result data to the output file
                    using (FileStream fs = File.Create(dataDir + "output.xps"))
                    {
                        memory.CopyTo(fs);
                    }
                }
            }
            // ExEnd:1
        }
    }
    public class MemoryStreamProvider : ICreateStreamProvider
    {
        // List of MemoryStream objects created during the document rendering
        public List<MemoryStream> Streams { get; } = new List<MemoryStream>();
        public Stream GetStream(string name, string extension)
        {
            // This method is called when the only one output stream is required, for instance for XPS, PDF or TIFF formats
            MemoryStream result = new MemoryStream();
            Streams.Add(result);
            return result;
        }
        public Stream GetStream(string name, string extension, int page)
        {
            // This method is called when the creation of multiple output streams are required. For instance during the rendering HTML to list of the image files (JPG, PNG, etc.)
            MemoryStream result = new MemoryStream();
            Streams.Add(result);
            return result;
        }
        public void ReleaseStream(Stream stream)
        {
            //  Here You can release the stream filled with data and, for instance, flush it to the hard-drive
        }
        public void Dispose()
        {
            // Releasing resources
            foreach (var stream in Streams)
                stream.Dispose();
        }
```
