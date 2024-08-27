---
title: Create Empty HTML Documents in Aspose.HTML for Java
linktitle: Create Empty HTML Documents in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 11
url: /java/creating-managing-html-documents/create-empty-html-documents/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

public class WorkingWithHTMLDocuments_CreateDocuments_EmptyHTML {
    public static void main(String [] args) throws java.io.IOException {
        // START_SNIPPET WorkingWithHTMLDocuments_CreateDocuments_EmptyHTML
        // Initialize an empty HTML Document.
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument();
        try {
            // Save the document to disk.
            document.save("create-empty-document.html");
        } finally {
            if (document != null) {
                document.dispose();
            }
        }
        // END_SNIPPET
    }
}

```
