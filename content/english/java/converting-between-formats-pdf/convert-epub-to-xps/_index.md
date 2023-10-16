---
title: Convert EPUB File to XPS
linktitle: Convert EPUB File to XPS
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 14
url: /java/converting-between-formats-pdf/convert-epub-to-xps/
---

## Complete Source Code
```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of XpsSaveOptions.
            com.aspose.html.saving.XpsSaveOptions options = new com.aspose.html.saving.XpsSaveOptions();
            // Call the ConvertEPUB method to convert the EPUB to XPS.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.xps")
            );
        }
```
