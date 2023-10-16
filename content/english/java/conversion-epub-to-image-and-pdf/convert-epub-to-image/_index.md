---
title: Converting EPUB to Image
linktitle: Converting EPUB to Image
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/conversion-epub-to-image-and-pdf/convert-epub-to-image/
---

## Complete Source Code
```java
        //@START
        // Source EPUB document
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Initialize ImageSaveOptions
            com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg);
            // Output file path
            String outputFile = Resources.output("EPUBtoImageOutput.jpeg");
            // Convert SVG to Image
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    outputFile
            );
        }
        //@END
```