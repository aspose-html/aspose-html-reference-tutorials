---
title: Converting EPUB to GIF
linktitle: Converting EPUB to GIF
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 11
url: /java/converting-between-epub-and-image-formats/convert-epub-to-gif/
---

## Complete Source Code
```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Initialize ImageSaveOptions
            com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Gif);
            // Call the ConvertEPUB method to convert the EPUB file to GIF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.gif")
            );
        }
```
