---
title: Memory Stream Provider in .NET with Aspose.HTML
linktitle: Memory Stream Provider in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 12
url: /net/advanced-features/memory-stream-provider-dotnet-aspose-html/
---

## Complete Source Code
```csharp
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
