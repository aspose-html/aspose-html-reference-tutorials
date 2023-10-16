---
title: XPS Save Options for EPUB to XPS
linktitle: XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 24
url: /java/epub-conversion/xps-save-options-epub-to-xps/
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
