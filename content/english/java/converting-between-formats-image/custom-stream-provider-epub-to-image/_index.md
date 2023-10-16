---
title: Specify Custom Stream Provider for EPUB to Image
linktitle: Specify Custom Stream Provider for EPUB to Image
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 15
url: /java/converting-between-formats-image/custom-stream-provider-epub-to-image/
---

## Complete Source Code
```java
// Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of MemoryStreamProvider
            try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
                // Convert EPUB to Image by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertEPUB(
                        fileInputStream,
                        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
                        streamProvider.lStream
                );
                // Get access to the memory streams that contain the resulted data
                int size = streamProvider.lStream.size();
                for (int i = 0; i < size; i++) {
                    java.io.InputStream inputStream = streamProvider.lStream.get(i);
                    // Flush the page to the output file
                    try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
                        byte[] buffer = new byte[inputStream.available()];
                        inputStream.read(buffer);
                        fileOutputStream.write(buffer);
                    }
                }
            }
        }
```
