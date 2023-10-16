---
title: HTML to Image in a Single Line
linktitle: HTML to Image in a Single Line
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 17
url: /java/html-conversion-image/html-to-image-in-single-line/
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
