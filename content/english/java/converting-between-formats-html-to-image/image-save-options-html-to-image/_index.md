---
title: Specify Image Save Options for HTML to Image
linktitle: Specify Image Save Options for HTML to Image
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 16
url: /java/converting-between-formats-html-to-image/image-save-options-html-to-image/
---

## Complete Source Code
```java
        // Prepare an HTML code and save it to the file
        String code = "<span>Hello</span> <span>World!!</span>";
        try (java.io.FileWriter fileWriter = new java.io.FileWriter(Resources.output("document.html"))) {
            fileWriter.write(code);
        }
        // Set up the page-size 3000x1000 pixels and change the background color to green
        com.aspose.html.saving.ImageSaveOptions options = new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg);
        com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
        com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
        anyPage.setSize(
                new com.aspose.html.drawing.Size(
                        com.aspose.html.drawing.Length.fromPixels(3000),
                        com.aspose.html.drawing.Length.fromPixels(1000)
                )
        );
        pageSetup.setAnyPage(anyPage);
        options.setPageSetup(pageSetup);
        options.setBackgroundColor(com.aspose.html.drawing.Color.getGreen());
        // Call the ConvertHTML to convert 'document.html' into jpeg image
        com.aspose.html.converters.Converter.convertHTML(
                Resources.output("document.html"),
                options,
                Resources.output("output.jpg")
        );
```
