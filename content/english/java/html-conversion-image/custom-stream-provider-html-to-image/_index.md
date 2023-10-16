---
title: Custom Stream Provider for HTML to Image
linktitle: Custom Stream Provider for HTML to Image
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 15
url: /java/html-conversion-image/custom-stream-provider-html-to-image/
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
