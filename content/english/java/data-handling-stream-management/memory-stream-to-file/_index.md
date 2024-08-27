---
title: Convert Memory Stream to File using Aspose.HTML for Java
linktitle: Convert Memory Stream to File using Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 10
url: /java/data-handling-stream-management/memory-stream-to-file/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

public class Advanced_MemoryStreamToFile {
    public static void main(String [] args) throws java.io.IOException {
        // START_SNIPPET Advanced_MemoryStreamToFile
        MemoryStreamProvider streamProvider = new MemoryStreamProvider();

        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("<span>Hello World!!</span>");

        com.aspose.html.converters.Converter.convertHTML(document, new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg), streamProvider.lStream);

        // Get access to the memory stream that contains the result data
        java.io.InputStream memory = streamProvider.lStream.get(0);
        memory.reset();

        java.io.FileOutputStream fs = new java.io.FileOutputStream("output.jpg");
        java.nio.file.Files.copy(memory, new java.io.File("output.jpg").toPath());
        // END_SNIPPET
    }
}

```
