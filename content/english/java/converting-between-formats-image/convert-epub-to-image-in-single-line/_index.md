---
title: Convert EPUB to Image in a Single Line
linktitle: Convert EPUB to Image in a Single Line
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 17
url: /java/converting-between-formats-image/convert-epub-to-image-in-single-line/
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
