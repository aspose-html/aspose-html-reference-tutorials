---
title: Convert EPUB to PDF in a Single Line
linktitle: Convert EPUB to PDF in a Single Line
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/converting-between-formats-pdf/convert-epub-to-pdf-in-single-line/
---

## Complete Source Code
```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    new com.aspose.html.saving.PdfSaveOptions(),
                    Resources.output("output.pdf")
            );
        }
```
