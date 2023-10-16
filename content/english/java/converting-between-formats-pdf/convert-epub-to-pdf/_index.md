---
title: Convert EPUB File to PDF
linktitle: Convert EPUB File to PDF
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/converting-between-formats-pdf/convert-epub-to-pdf/
---

## Complete Source Code
```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of PdfSaveOptions.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```
