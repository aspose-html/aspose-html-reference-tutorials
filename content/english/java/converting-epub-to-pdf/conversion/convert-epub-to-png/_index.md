---
title: Converting EPUB to PNG
linktitle: Converting EPUB to PNG
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/converting-epub-to-pdf//conversion/convert-epub-to-png/
---

## Complete Source Code
```java
        // Opens an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Initialize ImageSaveOptions
            com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Png);
            // Call the ConvertEPUB method to convert the EPUB file to PNG.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.png")
            );
        }
```
