---
title: Create HTML Documents from String in Aspose.HTML for Java
linktitle: Create HTML Documents from String in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 15
url: /java/creating-managing-html-documents/create-html-documents-from-string/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

public class WorkingWithHTMLDocuments_CreateDocuments_LoadFromString {
    public static void main(String [] args) throws java.io.IOException {
        // START_SNIPPET WorkingWithHTMLDocuments_CreateDocuments_LoadFromString
        // Prepare HTML code
        String html_code = "<p>Hello World!</p>";

        // Initialize a document from the string variable
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(html_code, ".");

        // Save the document to a disk
        document.save("create-from-string.html");
        // END_SNIPPET
    }
}

```
