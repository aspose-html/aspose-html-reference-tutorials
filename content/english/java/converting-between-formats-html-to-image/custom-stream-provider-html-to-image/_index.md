---
title: Specify Custom Stream Provider for HTML to Image
linktitle: Specify Custom Stream Provider for HTML to Image
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 15
url: /java/converting-between-formats-html-to-image/custom-stream-provider-html-to-image/
---

## Complete Source Code
```java
        // Create an instance of MemoryStreamProvider
        try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
            // Initialize an HTML document
            com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("<span>Hello</span> <span>World!!</span>", ".");
            try {
                // Convert HTML to Image by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertHTML(
                        document,
                        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
                        streamProvider.lStream
                );
                // Get access to the memory stream that contains the result data
                java.io.InputStream inputStream = streamProvider.lStream.stream().findFirst().get();
                // Flush the result data to the output file
                try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("output.jpg"))) {
                    byte[] buffer = new byte[inputStream.available()];
                    inputStream.read(buffer);
                    fileOutputStream.write(buffer);
                }
            } finally {
                if (document != null) {
                    document.dispose();
                }
            }
        }
```
