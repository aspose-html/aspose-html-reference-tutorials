---
title: Manage Inner and Outer HTML Properties in Aspose.HTML for Java
linktitle: Manage Inner and Outer HTML Properties in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 15
url: /java/editing-html-documents/manage-inner-outer-html-properties/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

public class WorkingWithHTMLDocuments_EditDocuments_InnerOuterHTMLProperties {
    public static void main(String [] args) throws java.io.IOException {
        // START_SNIPPET WorkingWithHTMLDocuments_EditDocuments_InnerOuterHTMLProperties
        // Create an instance of an HTML document
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument();

        // Write the content of the HTML document into the console output
        System.out.println(document.getDocumentElement().getOuterHTML()); // output: <html><head></head><body></body></html>

        // Set the content of the body element
        document.getBody().setInnerHTML("<p>HTML is the standard markup language for Web pages.</p>");

        // Write the content of the HTML document into the console output
        System.out.println(document.getDocumentElement().getOuterHTML()); // output: <html><head></head><body><p>HTML is the standard markup language for Web pages.</p></body></html>
        // END_SNIPPET
    }
}

```
