---
title: PDF Save Options for HTML to PDF
linktitle: PDF Save Options for HTML to PDF
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/html-conversion-pdf/pdf-save-options-html-to-pdf/
---

## Complete Source Code
```java
        // Source HTML document
        com.aspose.html.HTMLDocument htmlDocument = new com.aspose.html.HTMLDocument(Resources.input("input.html"));
        // Initialize PdfSaveOptions
        com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
        options.setJpegQuality(100);
        // Output file path
        String outputPDF = Resources.output("HTMLtoPDF_Output.pdf");
        // Convert HTML to PDF
        com.aspose.html.converters.Converter.convertHTML(htmlDocument, options, outputPDF);
```
