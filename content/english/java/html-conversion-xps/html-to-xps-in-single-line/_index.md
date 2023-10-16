---
title: HTML to XPS in a Single Line
linktitle: HTML to XPS in a Single Line
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/html-conversion-xps/html-to-xps-in-single-line/
---

## Complete Source Code
```java
        // Source HTML document
        com.aspose.html.HTMLDocument htmlDocument = new com.aspose.html.HTMLDocument(Resources.input("input.html"));
        // Initialize XpsSaveOptions
        com.aspose.html.saving.XpsSaveOptions options = new com.aspose.html.saving.XpsSaveOptions();
        options.setBackgroundColor(com.aspose.html.drawing.Color.getCyan());
        // Output file path
        String outputFile = Resources.output("output.html.to.xps");
        // Convert HTML to XPS
        com.aspose.html.converters.Converter.convertHTML(htmlDocument, options, outputFile);
```
