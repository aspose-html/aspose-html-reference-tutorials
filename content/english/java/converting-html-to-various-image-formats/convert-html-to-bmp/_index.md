---
title: Converting HTML to BMP
linktitle: Converting HTML to BMP
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/converting-html-to-various-image-formats/convert-html-to-bmp/
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
            com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Bmp);
            // Convert HTML to BMP
            com.aspose.html.converters.Converter.convertHTML(document, options, Resources.output("output.bmp"));
        } finally {
            if (document != null) {
                document.dispose();
            }
        }
```
