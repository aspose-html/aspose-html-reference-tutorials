---
title: Convert EPUB to TIFF Image
linktitle: Convert EPUB to TIFF Image
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 14
url: /java/converting-between-formats-image/convert-epub-to-tiff/
---

## Complete Source Code
```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Initialize ImageSaveOptions
            com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Tiff);
            // Call the ConvertEPUB method to convert the EPUB file to TIFF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.tiff")
            );
        }
```
