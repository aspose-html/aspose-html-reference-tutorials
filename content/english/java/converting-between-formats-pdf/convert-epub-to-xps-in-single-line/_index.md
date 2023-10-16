---
title: Convert EPUB File to XPS in a Single Line
linktitle: Convert EPUB File to XPS in a Single Line
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 17
url: /java/converting-between-formats-pdf/convert-epub-to-xps-in-single-line/
---

## Complete Source Code
```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Call the ConvertEPUB method to convert the EPUB to XPS.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    new com.aspose.html.saving.XpsSaveOptions(),
                    Resources.output("output.xps")
            );
        }
```
