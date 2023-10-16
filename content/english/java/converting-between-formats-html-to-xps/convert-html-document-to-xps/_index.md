---
title: Convert HTML Document to XPS
linktitle: Convert HTML Document to XPS
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/converting-between-formats-html-to-xps/convert-html-document-to-xps/
---

## Complete Source Code
```java
        // Prepare an HTML code and save it to the file.
        String code = "<span>Hello World!!</span>";
        try (java.io.FileWriter fileWriter = new java.io.FileWriter(Resources.output("document.html"))) {
            fileWriter.write(code);
        }
        // Initialize an HTML document from the file
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(Resources.output("document.html"));
        try {
            // Initialize XpsSaveOptions
            com.aspose.html.saving.XpsSaveOptions options = new com.aspose.html.saving.XpsSaveOptions();
            // Convert HTML to XPS
            com.aspose.html.converters.Converter.convertHTML(
                    document,
                    options,
                    Resources.output("output.xps")
            );
        } finally {
            if (document != null) {
                document.dispose();
            }
        }
```
