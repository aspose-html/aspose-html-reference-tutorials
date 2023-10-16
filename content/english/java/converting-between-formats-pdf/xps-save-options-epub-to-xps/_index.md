---
title: Specify XPS Save Options for EPUB to XPS
linktitle: Specify XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 16
url: /java/converting-between-formats-pdf/xps-save-options-epub-to-xps/
---

## Complete Source Code
```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the XpsSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.XpsSaveOptions options = new com.aspose.html.saving.XpsSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(
                    new com.aspose.html.drawing.Size(
                            com.aspose.html.drawing.Length.fromPixels(3000),
                            com.aspose.html.drawing.Length.fromPixels(1000)
                    )
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to XPS.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.xps")
            );
        }
```
