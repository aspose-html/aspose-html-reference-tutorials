---
title: Convert HTML to PDF in a Single Line
linktitle: Convert HTML to PDF in a Single Line
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/converting-between-formats-html-to-pdf/convert-html-to-pdf-in-single-line/
---

## Complete Source Code
```java
        // Invoke the ConvertHTML method to convert the HTML to PDF.
        com.aspose.html.converters.Converter.convertHTML(
                "<span>Hello World!!</span>",
                ".",
                new com.aspose.html.saving.PdfSaveOptions(),
                Resources.output("output.pdf")
        );
```
