---
title: Creating a Document in .NET with Aspose.HTML
linktitle: Creating a Document in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 10
url: /net/working-with-html-documents/creating-a-document-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            CreateSVG();
            FromScratch();
            FromLocalFile();
            FromRemoteURL();
            FromRemoteURL1();
            FromHTML();
            FromStream();
        }
        private static void CreateSVG()
        {
            using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
            {
                // do some actions over the document here...
            }
        }
        private static void FromScratch()
        {
            using (var document = new Aspose.Html.HTMLDocument())
            {
                // do some actions over the document here...
            }
        }
        private static void FromLocalFile()
        {
            string dataDir = RunExamples.GetDataDir_Data();
            using (var document = new Aspose.Html.HTMLDocument(dataDir+"input.html"))
            {
                // do some actions over the document here...
            }
        }
        private static void FromRemoteURL()
        {
            using (var document = new Aspose.Html.HTMLDocument("http://your.site.com/"))
            {
                // do some actions over the document here...
            }
        }
        private static void FromRemoteURL1()
        {
            using (var document = new Aspose.Html.HTMLDocument(new Url("http://your.site.com/")))
            {
                // do some actions over the document here...
            }
        }
        private static void FromHTML()
        {
            using (var document = new Aspose.Html.HTMLDocument("<p>my first paragraph</p>", "."))
            {
                // do some actions over the document here...
            }
        }
        private static void FromStream()
        {
            using (MemoryStream mem = new MemoryStream())
            using (StreamWriter sw = new StreamWriter(mem))
            {
                sw.Write("<p>my first paragraph</p>");
                // It is important to set the position to the beginning, since HTMLDocument starts the reading exactly from the current position within the stream.
                sw.Flush();
                mem.Seek(0, SeekOrigin.Begin);
                using (var document = new Aspose.Html.HTMLDocument(mem, "about:blank"))
                {
                    // do some actions over the document here...
                }
            }
        }
```
