---
title: Load HTML Documents from File in Aspose.HTML for Java
linktitle: Load HTML Documents from File in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/creating-managing-html-documents/load-html-documents-from-file/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

public class WorkingWithHTMLDocuments_CreateDocuments_LoadFromFile {
    public static void main(String [] args) throws java.io.IOException {
        // START_SNIPPET WorkingWithHTMLDocuments_CreateDocuments_LoadFromFile
        // Prepare a 'load-from-file.html' file.
        try (java.io.FileWriter fileWriter = new java.io.FileWriter("load-from-file.html")) {
            fileWriter.write("Hello World!");
        }

        // Load from a 'load-from-file.html' file.
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("load-from-file.html");
        // Write the document content to the output stream.
        System.out.println(document.getDocumentElement().getOuterHTML());
        // END_SNIPPET
    }
}

```
