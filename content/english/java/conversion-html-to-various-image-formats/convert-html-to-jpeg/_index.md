---
title: Converting HTML to JPEG
linktitle: Converting HTML to JPEG
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/conversion-html-to-various-image-formats/convert-html-to-jpeg/
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
