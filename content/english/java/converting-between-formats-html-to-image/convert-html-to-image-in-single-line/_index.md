---
title: Convert HTML to Image in a Single Line
linktitle: Convert HTML to Image in a Single Line
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 17
url: /java/converting-between-formats-html-to-image/convert-html-to-image-in-single-line/
---

## Complete Source Code
```java
        // Invoke the ConvertHTML method to convert the HTML code to image.
        com.aspose.html.converters.Converter.convertHTML(
                "<span>Hello</span> <span>World!!</span>",
                ".",
                new com.aspose.html.saving.ImageSaveOptions(
                        com.aspose.html.rendering.image.ImageFormat.Jpeg
                ),
                Resources.output("output.jpg")
        );
```
