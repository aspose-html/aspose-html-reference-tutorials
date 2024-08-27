---
title: Convert HTML to Markdown in Aspose.HTML for Java
linktitle: Convert HTML to Markdown in Aspose.HTML for Java
second_title: Java HTML Processing with Aspose.HTML
description: 
type: docs
weight: 12
url: /java/saving-html-documents/convert-html-to-markdown/
---

## Complete Source Code
```java
package com.aspose.html.documentation.examples;

import java.io.IOException;

public class WorkingWithHTMLDocuments_SaveDocuments_SaveHTMLToMarkdown {
    public static void main(String [] args) throws IOException {
        // START_SNIPPET WorkingWithHTMLDocuments_SaveDocuments_SaveHTMLToMarkdown
        // Prepare an output path for a document saving
        String documentPath = "save-to-MD.md";

        // Prepare HTML code
        String html_code = "<H2>Hello World!</H2>";

        // Initialize a document from the string variable
        com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(html_code, ".");

        // Save the document as a Markdown file
        document.save(documentPath, com.aspose.html.saving.HTMLSaveFormat.Markdown);
        // END_SNIPPET
    }
}

```
