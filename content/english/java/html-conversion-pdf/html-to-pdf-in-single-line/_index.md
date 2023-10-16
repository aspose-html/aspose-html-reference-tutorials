---
title: HTML to PDF in a Single Line
linktitle: HTML to PDF in a Single Line
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/html-conversion-pdf/html-to-pdf-in-single-line/
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
