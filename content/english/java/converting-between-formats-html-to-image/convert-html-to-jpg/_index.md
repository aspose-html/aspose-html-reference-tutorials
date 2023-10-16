---
title: Convert HTML to JPG Image
linktitle: Convert HTML to JPG Image
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/converting-between-formats-html-to-image/convert-html-to-jpg/
---

## Complete Source Code
```java
        // Prepare an HTML code and save it to the file.
        String code = "<span>Hello</span> <span>World!!</span>";
        try (java.io.FileWriter fileWriter = new java.io.FileWriter(Resources.output("document.html"))) {
            fileWriter.write(code);
        }
        // Initialize an HTML document from the html file
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(Resources.output("document.html"));
        try {
            // Initialize ImageSaveOptions
            com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg);
            // Convert HTML to JPG
            com.aspose.html.converters.Converter.convertHTML(document, options, Resources.output("output.jpg"));
        } finally {
            if (document != null) {
                document.dispose();
            }
        }
```
