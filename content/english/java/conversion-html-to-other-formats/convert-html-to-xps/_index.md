---
title: Converting HTML to XPS
linktitle: Converting HTML to XPS
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/conversion-html-to-other-formats/convert-html-to-xps/
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
