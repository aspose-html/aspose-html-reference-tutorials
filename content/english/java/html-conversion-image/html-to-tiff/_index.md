---
title: HTML to TIFF Image Conversion
linktitle: HTML to TIFF Image Conversion
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 14
url: /java/html-conversion-image/html-to-tiff/
---

## Complete Source Code
```java
        // Source HTML document
        com.aspose.html.HTMLDocument htmlDocument = new com.aspose.html.HTMLDocument(Resources.input("input.html"));
        // Initialize ImageSaveOptions
        com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Tiff);
        // Output file path
        String outputFile = Resources.output("HTMLtoPNG_Output.tif");
        // Convert HTML to TIFF
        com.aspose.html.converters.Converter.convertHTML(htmlDocument, options, outputFile);
```
