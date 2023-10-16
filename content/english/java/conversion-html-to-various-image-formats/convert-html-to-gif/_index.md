---
title: Converting HTML to GIF
linktitle: Converting HTML to GIF
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 11
url: /java/conversion-html-to-various-image-formats/convert-html-to-gif/
---

## Complete Source Code
```java
        // Source HTML document
        com.aspose.html.HTMLDocument htmlDocument = new com.aspose.html.HTMLDocument(Resources.input("input.html"));
        // Initialize ImageSaveOptions
        com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Gif);
        // Output file path
        String outputFile = Resources.output("HTMLtoGIF_Output.gif");
        // Convert HTML to GIF
        com.aspose.html.converters.Converter.convertHTML(htmlDocument, options, outputFile);
```
