---
title: Custom Stream Provider for EPUB to PDF
linktitle: Custom Stream Provider for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 19
url: /java/epub-conversion/custom-stream-provider-epub-to-pdf/
---

## Complete Source Code
```java
        //@START
        // Source EPUB document
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Initialize pdfSaveOptions
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            options.setJpegQuality(100);
            // Output file path
            String outputFile = Resources.output("EPUBtoPDF_Output.pdf");
            // Convert EPUB to PDF
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    outputFile
            );
        }
        //@END
```
