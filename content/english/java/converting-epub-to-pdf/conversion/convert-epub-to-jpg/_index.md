---
title: Converting EPUB to JPG
linktitle: Converting EPUB to JPG
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/converting-epub-to-pdf//conversion/convert-epub-to-jpg/
---

## Complete Source Code
```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Initialize ImageSaveOptions
            com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(
                    com.aspose.html.rendering.image.ImageFormat.Jpeg
            );
            // Call the ConvertEPUB method to convert the EPUB file to JPG.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.jpg")
            );
        }
```
