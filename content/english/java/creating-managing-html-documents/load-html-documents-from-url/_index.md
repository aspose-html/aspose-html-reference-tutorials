---
title: Load HTML Documents from URL in Aspose.HTML for Java
linktitle: Load HTML Documents from URL in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 16
url: /java/creating-managing-html-documents/load-html-documents-from-url/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

public class WorkingWithHTMLDocuments_CreateDocuments_LoadFromURL {
    public static void main(String [] args) throws java.io.IOException {
        // START_SNIPPET WorkingWithHTMLDocuments_CreateDocuments_LoadFromURL
        // Load a document from 'https://docs.aspose.com/html/net/creating-a-document/document.html' web page
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("https://docs.aspose.com/html/net/creating-a-document/document.html");

        System.out.println(document.getDocumentElement().getOuterHTML());
        // END_SNIPPET
    }
}

```
