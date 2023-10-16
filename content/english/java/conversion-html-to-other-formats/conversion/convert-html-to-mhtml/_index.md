---
title: Converting HTML to MHTML
linktitle: Converting HTML to MHTML
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 11
url: /java/conversion-html-to-other-formats//conversion/convert-html-to-mhtml/
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
