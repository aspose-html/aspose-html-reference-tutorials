---
title: Advanced File Loading for HTML Documents in Aspose.HTML for Java
linktitle: Advanced File Loading for HTML Documents in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 13
url: /java/creating-managing-html-documents/advanced-file-loading-html-documents/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

public class WorkingWithHTMLDocuments_CreateDocuments_LoadFromFile2 {
    public static void main(String [] args) throws java.io.IOException {
        // START_SNIPPET WorkingWithHTMLDocuments_CreateDocuments_LoadFromFile2
        // Prepare a path to a file
        String documentPath = "Sprite.html";

        // Initialize an HTML document from a file
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(documentPath);

        document.save("Sprite_out.html");
        // END_SNIPPET
    }
}

```
