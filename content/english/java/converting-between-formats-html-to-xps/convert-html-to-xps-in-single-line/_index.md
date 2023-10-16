---
title: Convert HTML to XPS in a Single Line
linktitle: Convert HTML to XPS in a Single Line
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/converting-between-formats-html-to-xps/convert-html-to-xps-in-single-line/
---

## Complete Source Code
```java
        // Invoke the ConvertHTML method to convert the HTML to XPS.
        com.aspose.html.converters.Converter.convertHTML(
                "<span>Hello World!!</span>",
                ".",
                new com.aspose.html.saving.XpsSaveOptions(),
                Resources.output("output.xps")
        );
```
