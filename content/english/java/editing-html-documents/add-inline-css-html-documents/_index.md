---
title: Add Inline CSS to HTML Documents in Aspose.HTML for Java
linktitle: Add Inline CSS to HTML Documents in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 14
url: /java/editing-html-documents/add-inline-css-html-documents/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

public class WorkingWithHTMLDocuments_EditDocuments_InlineCSS {
    public static void main(String [] args) throws java.io.IOException {
        // START_SNIPPET WorkingWithHTMLDocuments_EditDocuments_InlineCSS
        // Create an instance of an HTML document with specified content
        String content = "<p> Inline CSS </p>";
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(content, ".");

        // Find the paragraph element to set a style attribute
        com.aspose.html.HTMLElement paragraph = (com.aspose.html.HTMLElement) document.getElementsByTagName("p").get_Item(0);

        // Set the style attribute
        paragraph.setAttribute("style", "font-size: 250%; font-family: verdana; color: #cd66aa");

        // Save the HTML document to a file
        document.save("edit-inline-css.html");

        // Create the instance of the PDF output device and render the document into this device
        com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice("edit-inline-css.pdf");
        document.renderTo(device);
        // END_SNIPPET
    }
}

```
