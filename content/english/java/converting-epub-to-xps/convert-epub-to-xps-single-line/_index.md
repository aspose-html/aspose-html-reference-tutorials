---
title: Converting EPUB to XPS with a Single Line of Code
linktitle: Converting EPUB to XPS with a Single Line of Code
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/converting-epub-to-xps/convert-epub-to-xps-single-line/
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
