---
title: HTML to JPG Image Conversion
linktitle: HTML to JPG Image Conversion
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/html-conversion-image/html-to-jpg/
---

## Complete Source Code
```java
        // Source HTML document
        com.aspose.html.HTMLDocument htmlDocument = new com.aspose.html.HTMLDocument(Resources.input("input.html"));
        // Initialize ImageSaveOptions
        com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg);
        // Output file path
        String outputFile = Resources.output("HTMLtoJPEG_Output.jpeg");
        // Convert HTML to JPEG
        com.aspose.html.converters.Converter.convertHTML(htmlDocument, options, outputFile);
```
