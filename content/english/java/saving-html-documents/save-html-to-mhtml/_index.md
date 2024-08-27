---
title: Save HTML to MHTML in Aspose.HTML for Java
linktitle: Save HTML to MHTML in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/saving-html-documents/save-html-to-mhtml/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import java.io.IOException;

public class WorkingWithHTMLDocuments_SaveDocuments_SaveHTMLToMHTML {
    public static void main(String [] args) throws IOException {
        // START_SNIPPET WorkingWithHTMLDocuments_SaveDocuments_SaveHTMLToMHTML
        // Prepare an output path for a document saving
        String documentPath = "save-to-MTHML.mht";

        // Prepare a simple HTML file with a linked document
        java.nio.file.Files.write(java.nio.file.Paths.get("document.html"), "<p>Hello World!</p><a href='linked-file.html'>linked file</a>".getBytes());
        // Prepare a simple linked HTML file
        java.nio.file.Files.write(java.nio.file.Paths.get("linked-file.html"), "<p>Hello linked file!</p>".getBytes());

        // Load the "document.html" into memory
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html");

        // Save the document to MHTML format
        document.save(documentPath, com.aspose.html.saving.HTMLSaveFormat.MHTML);
        // END_SNIPPET
    }
}

```
