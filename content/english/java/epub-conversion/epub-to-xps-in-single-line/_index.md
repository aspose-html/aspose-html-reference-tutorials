---
title: EPUB to XPS in a Single Line
linktitle: EPUB to XPS in a Single Line
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 25
url: /java/epub-conversion/epub-to-xps-in-single-line/
---

## Complete Source Code
```java
        //@START
        // Source EPUB document
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Initialize XpsSaveOptions
            com.aspose.html.saving.XpsSaveOptions options = new com.aspose.html.saving.XpsSaveOptions();
            options.setBackgroundColor(com.aspose.html.drawing.Color.getCyan());
            // Output file path
            String outputFile = Resources.output("EPUBtoXPS_Output.xps");
            // Convert EPUB to XPS
            com.aspose.html.converters.Converter.convertEPUB(fileInputStream, options, outputFile);
        }
        //@END
```
