---
title: Use Extended Content Property in .NET with Aspose.HTML
linktitle: Use Extended Content Property in .NET with Aspose.HTML
second_title: Aspose.Slides .NET HTML manipulation API
description: 
type: docs
weight: 14
url: /net/advanced-features/use-extended-content-property-dotnet-aspose-html/
---

## Complete Source Code
```csharp
        public static void Run()
        {
            // ExStart:1
            string dataDir = RunExamples.GetDataDir_Data();
            //  Initialize configuration object and set up the page-margins for the document
            Configuration configuration = new Configuration();
            configuration.GetService<IUserAgentService>().UserStyleSheet = @"
                                                                            @page 
                                                                            {
                                                                                /* Page margins should be not empty in order to write content inside the margin-boxes */
                                                                                margin-top: 1cm;
                                                                                margin-left: 2cm;
                                                                                margin-right: 2cm;
                                                                                margin-bottom: 2cm;
                                                                                /* Page counter located at the bottom of the page */
                                                                                @bottom-right
                                                                                {
                                                                                    -aspose-content: ""Page "" currentPageNumber() "" of "" totalPagesNumber();
                                                                                    color: green;
                                                                                }
                                                                                /* Page title located at the top-center box */
                                                                                @top-center
                                                                                {
                                                                                    -aspose-content: ""Document's title"";
                                                                                    vertical-align: bottom;
                                                                                }    
                                                                            }";
            //  Initialize an empty document
            using (HTMLDocument document = new HTMLDocument(configuration))
            {
                //  Initialize an output device
                using (XpsDevice device = new XpsDevice(dataDir + "output_out.xps"))
                {
                    // Send the document to the output device
                    document.RenderTo(device);
                }
            }
            // ExEnd:1
        }
```
