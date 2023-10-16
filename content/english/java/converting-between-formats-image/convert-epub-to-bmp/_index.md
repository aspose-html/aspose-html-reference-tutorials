---
title: Convert EPUB to BMP Image
linktitle: Convert EPUB to BMP Image
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/converting-between-formats-image/convert-epub-to-bmp/
---

## Complete Source Code
```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Initialize ImageSaveOptions
            com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Bmp);
            // Call the ConvertEPUB method to convert the EPUB file to BMP.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.bmp")
            );
        }
```
