---
title: HTML to MHTML Conversion
linktitle: HTML to MHTML Conversion
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/html-conversion-markdown/html-to-mhtml/
---

## Complete Source Code
```java
        // Source HTML Document
        com.aspose.html.HTMLDocument htmlDocument = new com.aspose.html.HTMLDocument(Resources.input("input.html"));
        // Initialize MHTMLSaveOptions
        com.aspose.html.saving.MHTMLSaveOptions options = new com.aspose.html.saving.MHTMLSaveOptions();
        // Set the resource handling rules
        options.getResourceHandlingOptions().setMaxHandlingDepth(1);
        // Output file path
        String outputPDF = Resources.output("HTMLtoMHTML_Output.mht");
        // Convert HTML to MHTML
        com.aspose.html.converters.Converter.convertHTML(htmlDocument, options, outputPDF);
```
