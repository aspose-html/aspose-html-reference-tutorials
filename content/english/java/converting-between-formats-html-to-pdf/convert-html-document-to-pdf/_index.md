---
title: Convert HTML Document to PDF
linktitle: Convert HTML Document to PDF
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/converting-between-formats-html-to-pdf/convert-html-document-to-pdf/
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
            // Initialize PdfSaveOptions
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            // Convert HTML to PDF
            com.aspose.html.converters.Converter.convertHTML(
                    document,
                    options,
                    Resources.output("output.pdf")
            );
        } finally {
            if (document != null) {
                document.dispose();
            }
        }
```
