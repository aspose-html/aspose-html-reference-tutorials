---
title: Convert EPUB to Image in .NET with Aspose.HTML
linktitle: Convert EPUB to Image in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 11
url: /net/html-extensions-and-conversions/convert-epub-to-image-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void WithASingleLine()
        {
            string dataDir = RunExamples.GetDataDir_Data();
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Call the ConvertEPUB method to convert the EPUB file to image.
                Aspose.Html.Converters.Converter.ConvertEPUB(stream, new Aspose.Html.Saving.ImageSaveOptions(Aspose.Html.Rendering.Image.ImageFormat.Jpeg), "output.jpg");
            }
        }
        public static void ConvertEPUBToJPG()
        {
            string dataDir = RunExamples.GetDataDir_Data();
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Initialize ImageSaveOptions 
                var options = new Aspose.Html.Saving.ImageSaveOptions(Aspose.Html.Rendering.Image.ImageFormat.Jpeg);
                // Call the ConvertEPUB method to convert the EPUB file to JPG.
                Aspose.Html.Converters.Converter.ConvertEPUB(stream, options, "output.jpg");
            }
        }
        public static void ConvertEPUBToPNG()
        {
            string dataDir = RunExamples.GetDataDir_Data();
            // Opens an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Initialize ImageSaveOptions 
                var options = new Aspose.Html.Saving.ImageSaveOptions(Aspose.Html.Rendering.Image.ImageFormat.Png);
                // Call the ConvertEPUB method to convert the EPUB file to PNG.
                Aspose.Html.Converters.Converter.ConvertEPUB(stream, options, "output.png");
            }
        }
        public static void ConvertEPUBToBMP()
        {
            string dataDir = RunExamples.GetDataDir_Data();
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Initialize ImageSaveOptions 
                var options = new Aspose.Html.Saving.ImageSaveOptions(Aspose.Html.Rendering.Image.ImageFormat.Bmp);
                // Call the ConvertEPUB method to convert the EPUB file to BMP.
                Aspose.Html.Converters.Converter.ConvertEPUB(stream, options, "output.bmp");
            }
        }
        public static void ConvertEPUBToGIF()
        {
            string dataDir = RunExamples.GetDataDir_Data();
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Initialize ImageSaveOptions 
                var options = new Aspose.Html.Saving.ImageSaveOptions(Aspose.Html.Rendering.Image.ImageFormat.Gif);
                // Call the ConvertEPUB method to convert the EPUB file to GIF.
                Aspose.Html.Converters.Converter.ConvertEPUB(stream, options, "output.gif");
            }
        }
        public static void ConvertEPUBToTIFF()
        {
            string dataDir = RunExamples.GetDataDir_Data();
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Initialize ImageSaveOptions 
                var options = new Aspose.Html.Saving.ImageSaveOptions(Aspose.Html.Rendering.Image.ImageFormat.Tiff);
                // Call the ConvertEPUB method to convert the EPUB file to TIFF.
                Aspose.Html.Converters.Converter.ConvertEPUB(stream, options, "output.tiff");
            }
        }
        public static void SpecifyImageSaveOptions()
        {
            string dataDir = RunExamples.GetDataDir_Data();
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Initailize the ImageSaveOptions with a custom page-size and a background-color.
                var options = new Aspose.Html.Saving.ImageSaveOptions(Aspose.Html.Rendering.Image.ImageFormat.Jpeg)
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
                // Call the ConvertEPUB method to convert the EPUB file to JPG.
                Aspose.Html.Converters.Converter.ConvertEPUB(stream, options, "output.jpg");
            }
        }
        public static void SpecifyCustomStreamProvider()
        {
            string dataDir = RunExamples.GetDataDir_Data();
            // Open an existing EPUB file for reading.
            using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
            {
                // Create an instance of MemoryStreamProvider
                using (var streamProvider = new MemoryStreamProvider())
                {
                    // Convert EPUB to Image by using the MemoryStreamProvider
                    Aspose.Html.Converters.Converter.ConvertEPUB(stream, new Aspose.Html.Saving.ImageSaveOptions(Aspose.Html.Rendering.Image.ImageFormat.Jpeg),
                        streamProvider);
                    // Get access to the memory streams that contain the resulted data
                    for (int i = 0; i < streamProvider.Streams.Count; i++)
                    {
                        var memory = streamProvider.Streams[i];
                        memory.Seek(0, System.IO.SeekOrigin.Begin);
                        // Flush the page to the output file
                        using (System.IO.FileStream fs = System.IO.File.Create($"page_{i + 1}.jpg"))
                        {
                            memory.CopyTo(fs);
                        }
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
