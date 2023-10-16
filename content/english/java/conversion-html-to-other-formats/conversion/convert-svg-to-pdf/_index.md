---
title: Converting SVG to PDF
linktitle: Converting SVG to PDF
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 15
url: /java/conversion-html-to-other-formats//conversion/convert-svg-to-pdf/
---

## Complete Source Code
```java
        // Source SVG document
        com.aspose.html.dom.svg.SVGDocument svgDocument = new com.aspose.html.dom.svg.SVGDocument(Resources.input("input.svg"));
        // Initialize pdfSaveOptions
        com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
        options.setJpegQuality(100);
        // Output file path
        String outputFile = Resources.output("SVGtoPDF_Output.pdf");
        // Convert SVG to PDF
        com.aspose.html.converters.Converter.convertSVG(svgDocument, options, outputFile);
```
