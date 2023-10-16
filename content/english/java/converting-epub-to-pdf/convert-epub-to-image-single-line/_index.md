---
title: Converting EPUB to Image with a Single Line of Code
linktitle: Converting EPUB to Image with a Single Line of Code
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 17
url: /java/converting-epub-to-pdf/convert-epub-to-image-single-line/
---

## Complete Source Code
```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Call the ConvertEPUB method to convert the EPUB file to image.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
                    Resources.output("output.jpg")
            );
        }
```
