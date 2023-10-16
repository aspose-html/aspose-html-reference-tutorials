---
title: Specify Custom Stream Provider for HTML to PDF
linktitle: Specify Custom Stream Provider for HTML to PDF
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 11
url: /java/converting-between-formats-html-to-pdf/custom-stream-provider-html-to-pdf/
---

## Complete Source Code
```java
        // Create an instance of MemoryStreamProvider
        try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
            // Initialize an HTML document
            com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("<span>Hello World!!</span>", ".");
            try {
                // Convert HTML to PDF by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertHTML(
                        document,
                        new com.aspose.html.saving.PdfSaveOptions(),
                        streamProvider.lStream
                );
                // Get access to the memory stream that contains the result data
                java.io.InputStream inputStream = streamProvider.lStream.stream().findFirst().get();
                // Flush the result data to the output file
                try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("output.pdf"))) {
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
