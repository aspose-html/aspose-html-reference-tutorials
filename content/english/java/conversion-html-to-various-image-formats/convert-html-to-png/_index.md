---
title: Converting HTML to PNG
linktitle: Converting HTML to PNG
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/conversion-html-to-various-image-formats/convert-html-to-png/
---

## Complete Source Code
```java
        // Source HTML document
        com.aspose.html.HTMLDocument htmlDocument = new com.aspose.html.HTMLDocument(Resources.input("input.html"));
        // Initialize ImageSaveOptions
        com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Png);
        // Output file path
        String outputFile = Resources.output("HTMLtoPNG_Output.png");
        // Convert HTML to PNG
        com.aspose.html.converters.Converter.convertHTML(htmlDocument, options, outputFile);
```
