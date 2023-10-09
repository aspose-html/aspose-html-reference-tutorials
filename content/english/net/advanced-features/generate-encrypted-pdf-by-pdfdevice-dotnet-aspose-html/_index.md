---
title: Generate Encrypted PDF by PdfDevice in .NET with Aspose.HTML
linktitle: Generate Encrypted PDF by PdfDevice in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 15
url: /net/advanced-features/generate-encrypted-pdf-by-pdfdevice-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            string dataDir = "Your Data Directory";
            using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
            {
                var options = new PdfRenderingOptions()
                {
                    PageSetup =
                    {
                        AnyPage = new Page(new Size(500, 500), new Margin(50, 50, 50, 50))
                    },
                    Encryption = new PdfEncryptionInfo("user", "p@wd", PdfPermissions.PrintDocument, PdfEncryptionAlgorithm.RC4_128)
                };
                using (PdfDevice device = new PdfDevice(options, dataDir + @"document_out.pdf"))
                {
                    document.RenderTo(device);
                }
            }
            // ExEnd:1
        }
```
