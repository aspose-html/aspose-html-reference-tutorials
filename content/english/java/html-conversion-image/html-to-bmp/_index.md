---
title: HTML to BMP Image Conversion
linktitle: HTML to BMP Image Conversion
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/html-conversion-image/html-to-bmp/
---

## Complete Source Code
```java
        //@START
        // Source HTML document
        com.aspose.html.HTMLDocument htmlDocument = new com.aspose.html.HTMLDocument(Resources.input("input.html"));
        // Initialize ImageSaveOptions
        com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Bmp);
        // Output file path
        String outputFile = Resources.output("HTMLtoBMP_Output.bmp");
        // Convert HTML to BMP
        com.aspose.html.converters.Converter.convertHTML(htmlDocument, options, outputFile);
        //@END
```
