---
title: Convert HTML to MHTML
linktitle: Convert HTML to MHTML
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/converting-between-formats-html-to-markdown/convert-html-to-mhtml/
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
            // Initialize MHTMLSaveOptions
            com.aspose.html.saving.MHTMLSaveOptions options = new com.aspose.html.saving.MHTMLSaveOptions();
            // Convert HTML to MHT
            com.aspose.html.converters.Converter.convertHTML(
                    document,
                    options,
                    Resources.output("output.mht")
            );
        } finally {
            if (document != null) {
                document.dispose();
            }
        }
```
