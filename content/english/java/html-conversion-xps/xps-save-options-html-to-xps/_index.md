---
title: XPS Save Options for HTML to XPS
linktitle: XPS Save Options for HTML to XPS
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/html-conversion-xps/xps-save-options-html-to-xps/
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
